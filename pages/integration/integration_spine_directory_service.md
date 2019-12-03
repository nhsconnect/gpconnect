---
title: Overview and querying SDS
keywords: spine, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_directory_service.html
summary: "Overview of the role of the Spine Directory Services (SDS) within GP Connect"
---

## Overview ##

Spine Directory Service (SDS) is an endpoint and identifier directory for Spine and Spine connected systems, containing information on accredited systems, services and NHS registered users.  It is accessed via the Lightweight Directory Access Protocol (LDAP).

GP Connect provider and consumer systems are registered in SDS in order to enable:

- consumer systems to look up provider system's ASID and endpoint information
- the Spine Secure Proxy to allow or deny requests based on known identifier and endpoint information
<br/>

**AS records**

Every system that connects to the Spine has one or more "Accredited System" (AS) records in SDS, identified by an Accredited System Identifier (ASID).

This ASID is unique to a system deployed in a specific organisation, so the same application deployed into three NHS organisations would typically be represented as three unique ASIDs.

**MHS records and endpoints**

Every GP Connect system also has one or more "MHS" records (or message handling server record), identified by Party Key and [Interaction ID](integration_interaction_ids.html).

MHS records of GP Connect provider systems contain the endpoint of the target practice, as defined by the [FHIR service root URL](development_fhir_api_guidance.html#service-root-url).

Please see [System topologies](integration_system_topologies.html) for more details on the allocation of ASIDs and Party Keys.

{% include important.html content="**Distinguishing GP Connect provider and consumer SDS records**<br/>
Providers have GP Connect [interaction IDs](integration_interaction_ids.html) on their MHS records; consumers do not. This distinction enables the SDS queries below to return the correct record, where a provider organisation has separate consumer systems in addition to their main provider system." %}

## Querying SDS ##

GP Connect consumer systems are expected to resolve the [FHIR service root URL](development_fhir_api_guidance.html#service-root-url) and ASID for a given GP provider organisation using [Spine Directory Service (SDS)](http://digital.nhs.uk/spine) LDAP directory lookups.

This is a two-step process, as follows:

> 1. Lookup the Message Handling System (MHS) record
> 2. Lookup the Accredited System (AS) record

The process allows a consumer system to retrieve the following details for a target GP provider organisation:

- FHIR service root URL, retrieved from the `nhsMhsEndpoint` element in step 1
- and the ASID, retrieved from `uniqueIdentifier` element in step 2

The FHIR service root URL is used to [construct the full target URL for a GP Connect request](#step-3-consumer-constructs-full-gp-connect-request-url-to-be-sent-to-the-spine-security-proxy). The provider's ASID is sent in the  `Ssp-To` HTTP header.

Please see below for more detail on the process.

Systems **SHOULD** cache SDS query results giving details of consuming system, endpoints and endpoint capability on a per session basis.

Systems **MUST NOT** cache and re-use consuming system endpoint information derived from SDS across multiple patient encounters or practitioner usage sessions. Each new patient encounter will result in new lookups to ascertain the most up-to-date consuming system, endpoint and endpoint capability.

{% include important.html content="**Why have SDS queries changed in GP Connect API 0.7.2?**<br/>
The SDS queries in this version of the specification allow consumers to return the correct endpoint and ASID for a provider GP practice where the practice has multiple GP Connect ASIDs - this occurs where the practice is running one or more separate GP Connect consumer systems (with their own ASIDs), in addition to their principal clinical system acting as a provider and consumer.<br/>
The SDS queries in GP Connect API 0.7.1 and prior versions do not support this configuration, hence existing consumer systems **MUST** update their queries to to this version of the specification." %}


### Step 1: Message Handling System (MHS) record lookup  ###

Consumer systems **MUST** lookup the FHIR service root URL and Party Key from the MHS record, using the ODS code of the target practice, as follows:

**Search criteria:**
- Organisation code
	- `nhsIDCode` = *ODS code* of the target organisation (for example, GP practice)
- Message Handling System type
	- `objectClass` = `nhsMHS`
- MHS Interaction ID
	- `nhsMhsSvcIA` = *Interaction ID*, please see GP Connect [Interaction IDs](integration_interaction_ids.html)

**Result attributes:**
- Target organisation's FHIR service root URL
	- `nhsMhsEndPoint` 
- Target organisation's Party Key
	- `nhsMhsPartyKey`

**ldapsearch query:**

```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsidcode=[odsCode]) (objectClass=nhsMhs) (nhsMhsSvcIA=[interactionId]))"
	nhsMhsEndPoint nhsMhsPartyKey	
```

### Step 2: Accredited System record lookup ###

Consumer systems **MUST** use the Party Key retrieved in Step 1 along with the practice's ODS code, in order to determine the ASID of the target practice, as follows:

**Search criteria:**
- Organisational code
	- `nhsIDCode` = *ODS code* of the target organisation (for example, GP practice)
- Accredited System type
	- `objectClass` = `nhsAs`
- MHS Party Key
	- `nhsMHSPartyKey` = Target organisation's *Party key* as retrieved from the `nhsMhsPartyKey` attribute in step 1
	
**Result attributes:**
- Target organisation's ASID
	- `uniqueIdentifier`

**ldapsearch query:**
	
```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsidcode=[odsCode]) (objectclass=nhsAs) (nhsMHSPartyKey=[nhsMHSPartyKey]))"
	uniqueIdentifier	
```

## Worked example of the endpoint lookup process ##

**Given**
A consuming system which needs to get the HTML record of a patient record at the patient's registered practice. The consuming system has the following information about the patient:
- NHS number
- a set of demographic details about the patient

**When**
The consuming system interacts with GP Connect

**Then** 
The following steps **MUST** be followed:


### Step 0: PDS trace (pre-requisite step)

The consuming system is responsible for [performing a PDS trace](integration_personal_demographic_service.html) to both verify the identity of the patient and retrieve the ODS code of the patient's registered primary care practice. 

For this example, NHS number 9000000084 with demographic details Mr Anthony Tester, 19 Fictitious Avenue, Testtown returns the ODS code T99999.



### Step 1: MHS record lookup on SDS to determine FHIR endpoint server root URL

Using the ODS code retrieved from Step 0, and the interaction ID of the required service, the following ldapsearch query is executed:

	ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsIDCode=T99999) (objectClass=nhsMhs) (nhsMhsSvcIA=urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord))" 
	nhsMhsEndPoint nhsMhsPartyKey
	
	
This query should return a single endpoint. In this case, the ldapquery returns the following results:

	# 472b35d4641b76454b13, Services, nhs
	dn: uniqueIdentifier=472b35d4641b76454b13,ou=Services,o=nhs
	nhsMhsEndPoint: https://pcs.thirdparty.nhs.uk/T99999/STU3/1
	nhsMhsPartyKey: T99999-9999999

	# search result
	search: 1
	result: 0 Success


### Step 2: AS record lookup on SDS to determine the provider’s ASID

The ASID is now looked up on SDS. The example below uses ldapsearch:

	
	ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsIDCode=T99999) (objectClass=nhsAS) (nhsMHSPartyKey=T99999-9999999))" 
	uniqueIdentifier 

	
This query should return a single matching accredited system object from SDS, the ASID being found in the uniqueIdentifier attribute. In this case, the ldapquery returns the following results:


	999999999999, Services, nhs
	dn: uniqueIdentifier=9999999999,ou=Services,o=nhs
	uniqueIdentifier: 999999999999

	# search result
	search: 1
	result: 0 Success



### Step 3: Consumer constructs full GP Connect request URL to be sent to the Spine Security Proxy

The format of the full URL which the consuming system is responsible for constructing is as follows:

`https://[Spine Secure Proxy URL]/[Provider Service Root URL]/[FHIR request]`

The value returned in the `nhsMhsEndPoint` attribute in Step 1 should be treated as the `[Provider Server Root URL]` at the provider system.

{% include sds_ssp_warning.html %}

In this example, to issue a Get Care Record request, the following request would be made:

`POST https://testspineproxy.nhs.domain.uk/https://pcs.thirdparty.nhs.uk/T99999/STU3/1/Patient/$gpc.getcarerecord`

## SDS TLS configuration ##

SDS requires TLS Mutual Authentication. It is therefore necessary to configure ldapsearch in the examples above with the certificates necessary to verify the authenticity of the SDS LDAP server, and also to enable SDS to verify the spine endpoint making the LDAP request:

1. Root and SubCA Spine development certificates available from Assurance Support
2. Obtain a client certificate by submitting a certificate signing request for your development endpoint to Assurance Support

## Looking up a consumer's own ASID ##

{% include important.html content="This LDAP query is for a consumer system to lookup their *own* ASID. To determine the provider's ASID and endpoint, please see the queries above." %}

A consumer is required to populate their ASID in the `Ssp-From` HTTP header when sending a GP Connect request.

Consumer systems deployed at many sites may prefer to dynamically query their own ASID instead of holding as local configuration.

Consumer system suppliers wishing to do this should be aware that there may be more than one GP Connect consumer system deployed at an organisation, and hence multiple AS records for a given ODS code.

In order to ensure the right AS record and ASID is retrieved, an additional search field should be used - `nhsMhsManufacturerOrg` is recommended - which will filter out AS records from other suppliers.

AS record lookup on SDS to determine the consumer's ASID.

**Search criteria:**
- Organisational code
	- `nhsIDCode` = *ODS code* of the consumer organisation
- Accredited System type
	- `objectClass` = `nhsAs`
- AS Interaction ID
	- `nhsAsSvcIA` = *Interaction ID*, please see GP Connect [Interaction IDs](integration_interaction_ids.html)
- Manufacturer of the consumer system (the *ODS code* of the manufacturer of the consumer system)
	- `nhsMhsManufacturerOrg` = *ODS code* of the consumer system supplier
	
**Result attributes:**
- Consumer's ASID
	- `uniqueIdentifier`

**ldapsearch query:**

```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs"
	"(&(nhsIDCode=[odsCode]) (objectClass=nhsAS) (nhsaASvcIA=[interactionId]) (nhsMhsManufacturerOrg=[odsCode]))"
	uniqueIdentifier 
```
