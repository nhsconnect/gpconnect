---
title: Overview and querying SDS
keywords: spine, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_directory_service.html
summary: "Overview of the role of the Spine Directory Services (SDS) within GP Connect"
---

## Spine Accredited Systems and Endpoints ##

Every system that connects to the Spine has one or more "Accredited System" entry in the Spine Directory, identified by an Accredited System Identifier (ASID).

This ASID is unique to a system deployed in a specific organisation, so the same application deployed into three NHS organisations would typically be represented as three unique ASIDs.

In addition, each endpoint that is registered with the Spine has one or more "interaction IDs" associated with the endpoint. These identify the types of Spine interaction that the endpoint has been assured to perform. These are used to control what functionality can be called by connecting systems - calls to interactions for which the accredited system has not been assured will be blocked.


## Spine Directory Service (SDS) ##

GP Connect consumer systems are expected to resolve the FHIR endpoint for a given GP provider organisation using [Spine Directory Service (SDS)](http://digital.nhs.uk/spine){:target="_blank"} Lightweight Directory Access Protocol (LDAP) directory lookups. SDS is the main information source about NHS-registered users and accredited systems and services.

{% include roadmap.html content="NHS Digital is considering the delivery of a simplified FHIR facade over the Spine Directory Service (SDS) to allow FHIR endpoint resolution to be achieved in a more streamlined (and FHIR compatible) way." %}

Information is provided below to clarify how this endpoint lookup functions.

1. Consuming system viewpoint

	From the perspective of a consuming system, an overview of the endpoint lookup process is given followed by a worked end-to-end example of a GP Connect request to retrieve the HTML view of a patient record.

2. Provider system viewpoint

	Guidance on how a provider system should set up endpoints in Spine Directory Services.

	
## Consuming Spine Services ##

A consuming system will interact with SDS in order to resolve the FHIR Endpoint Server Root URL to be used when constructing the request to be made to the Spine service it wishes to call (or another external endpoint when sending a brokered call through the [Spine Secure Proxy]()).

This is a two step process, as follows:

1. Lookup the Message Handling System (MHS)
2. Lookup the Accredited System ID (ASID)

Once the MHS record has been retrieved the fully qualified domain name (FQDN) and full endpoint of the FHIR server can be retrieved from returned attributes of the MHS record.

Systems **SHOULD** cache SDS query results giving details of consuming system, endpoints and endpoint capability on a per session basis.

Consuming systems **MUST NOT** cache and re-use consuming system endpoint information derived from SDS across multiple patient encounters or practitioner usage sessions. Each new patient encounter will result in new lookups to ascertain the most up-to-date consuming system, endpoint and endpoint capability.


### Step 1: Message Handling System (MHS) Lookup for an external service (brokered via SSP)  ###

Consumers **MUST** lookup the endpoint URL, FQDN and Party Key from the MHS record, as follows:

**Search criteria:**
- Organisational code
	- `nhsIDCode` = *[odsCode]* of the target organisation (for example, GP practice)
- Message Handling System type
	- `objectClass` = `nhsMHS`
- MHS Interaction ID
	- `nhsMhsSvcIA` = *[interactionId]* of the API operation required

**Result attributes:**
- Endpoint URL
	- `nhsMhsEndPoint` 
- Fully qualified domain name
	- `nhsMHSFQDN` * 
- Party Key
	- `nhsMhsPartyKey`

**ldapsearch query:**

```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsidcode=[odsCode]) (objectClass=nhsMhs) (nhsMhsSvcIA=[interactionId]))"
	nhsMhsEndPoint, nhsMHSFQDN, nhsMhsPartyKey	
```

{% include note.html content="The FHIR endpoint URL of the message handling system can then be extracted from the `nhsMhsEndPoint` attribute of the MHS record. <br/><br/><b>*</b> The attribute `nhsMhsFQDN` can be used to retrieve the FQDN of the endpoint, though this can be extracted from the nhsMhsEndPoint." %}

Please refer to the specification of the specific FHIR API you are using for details of the interaction ID to use:

- [GP Connect operation guidance](https://developer.nhs.uk/apis/gpconnect/development_fhir_operation_guidance.html) for details of the GPConnect interactionId appropriate for your use case.



### Step 2: Accredited System ID (ASID) Lookup for an external service (brokered via SSP) ###

When the client wants to query an external service brokered through the Spine Security Proxy (e.g. a GP Connect API), the client **MUST** use an organisation ODS code for the target organisation and the nhsMHSPartyKey (identified in step 1) to lookup the Accredited System ID (ASID) as follows:

**Search criteria:**
- Organisational code
	- `nhsIDCode` = *[odsCode]* of the target organisation (for example, GP practice)
- Accredited System type
	- `objectClass` = `nhsAs`
- MHS Party Key
	- `nhsMHSPartyKey` = *[partyKey]* as retrieved from the `nhsMhsPartyKey` attribute in step 1a
	
**Result attributes:**
- ASID
	- `uniqueIdentifier`

**ldapsearch query:**
	
```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsidcode=[odsCode]) (objectclass=nhsAs) (nhsMHSPartyKey=[nhsMHSPartyKey]))"
	uniqueIdentifier	
```

The ASID will be returned in the uniqueIdentifier attribute which is returned from the ldapsearch query above.

{% include note.html content="Note that ldapsearch is used to establish a TLS session rather than the StartTLS option. Also note that once the TLS session is established, SASL authentication is not used by SDS and is therefore disabled through the -x option." %}




## Worked example of the endpoint lookup process ##

**Given**
A consuming system which needs to get the HTML view of a patient record at the patient's registered practice. The consuming system has the following information about the patient:
- NHS number
- a set of demographic details about the patient

**When**
The consuming system interacts with GP Connect

**Then** 
The following steps **MUST** be followed:


### Step 0. PDS trace (pre-requisite step)

The consuming system is responsible for [performing a PDS trace](integration_personal_demographic_service.html) to both verify the identity of the patient and retrieve the ODS code of the patient's registered primary care practice. 

For this example, NHS number 9000000084 with demographic details Mr Anthony Tester, 19 Fictitious Avenue, Testtown returns the ODS code T99999.



### Step 1: MHS lookup on SDS to determine FHIR endpoint server root URL

Using the party key retrieved from Step 1, and the same interaction ID, the following ldapsearch query is executed:

	ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsIDCode=T99999) (objectClass=nhsMhs) (nhsMhsSvcIA=urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-1))" 
	nhsMhsEndPoint nhsMHSFQDN nhsMhsPartyKey
	
	
This query should again return a single endpoint. In this case, the ldapquery returns the following results:

	# 472b35d4641b76454b13, Services, nhs
	dn: uniqueIdentifier=472b35d4641b76454b13,ou=Services,o=nhs
	nhsMhsEndPoint: https://pcs.thirdparty.nhs.uk/T99999/DSTU2/1
	nhsMHSFQDN: pcs.thirdparty.nhs.uk
	nhsMhsPartyKey: T99999-9999999

	# search result
	search: 2
	result: 0 Success


### Step 2. Accredited system lookup on SDS

The ASID and party key is now looked up on SDS. The example below uses ldapsearch:

	
	ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsIDCode=T99999) (objectClass=nhsAS) (nhsMHSPartyKey=T99999-9999999))" 
	uniqueIdentifier 

	
This query should return a single matching accredited system object from SDS, the ASID being found in the uniqueIdentifier attribute. In the case, ldapsearch returns the following results:


	999999999999, Services, nhs
	dn: uniqueIdentifier=9999999999,ou=Services,o=nhs
	uniqueIdentifier: 999999999999

	# search result
	search: 1
	result: 0 Success

	

### Step 3: Consumer constructs full GP Connect request URL to be sent to the Spine Security Proxy

The format of the full URL which the consuming system is responsible for constructing is as follows:

`https://[URL of Spine Security Proxy]/[Provider Server Root URL]/[FHIR request]`

The value returned in the nhsMhsEndPoint attribute in Step 1 should be treated as the FHIR Server Root URL at the provider system.

In this example, to issue a GetCareRecord request, the following request would be made:

`POST https://testspineproxy.nhs.domain.uk/https://pcs.thirdparty.nhs.uk/T99999/DSTU2/1/Patient/$gpc.getcarerecord`



## ldapsearch configuration ##

SDS requires TLS Mutual Authentication. It is therefore necessary to configure ldapsearch in the examples above with the certificates necessary to verify the authenticity of the SDS LDAP server, and also to enable SDS to verify the spine endpoint making the LDAP request:

1. Root and SubCA spine development certificates available from Assurance Support
2. Obtain a client certificate by submitting a certificate signing request for your development endpoint to Assurance Support

## Server certificate setup ##
For the examples above, ldapsearch should be configured to find the RootCA and SubCA certificates using the TLS_CACERT option in the ldap.conf file. This should point to a file, in PEM format, which contains both root and subca certificates ensuring that the root certificate is placed after the subCA certificae. The LDAPCONF environment vairable can be used to define the location of the ldap.conf 

## Client certificate setup ##
The client certificate and encrypted private key should be defined in the .ldaprc file using the following directives.

`
TLS_CERT C:\mydir\cert.pem
TLS_KEY C:\mydir\key.pem
`

The location of the .ldaprc file can be defined using the LDAPRC environment variable.

See [Environments](test_environments.html) for details of where to find URLs for SDS.




