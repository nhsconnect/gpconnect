---
title: Spine Directory Service
keywords: spine, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_directory_service.html
summary: "Overview of the role of the Spine Directory Services (SDS) within GP Connect."
---

## Spine Directory Service (SDS) ##

GP Connect Consumer systems are expected to resolve the FHIR endpoint for a given GP Provider organisation using [Spine Directory Service (SDS)](http://digital.nhs.uk/spine){:target="_blank"} LDAP directory lookups. SDS is the main information source about NHS registered users and accredited systems and services.


{% include roadmap.html content="NHS Digital is considering the delivery of a simplified FHIR façade over the Spine Directory Service (SDS) to allow FHIR endpoint resolution to be achieved in a more streamlined (and FHIR compatible) way." %}

Information is provided below to clarity how this endpoint lookup functions.

1. Consuming system lookup

From the perspective of a consuming system, an overview of the endpoint lookup process is given followedby a worked end-to-end example of a GPConnect request to retrieve the HTML View of a patient record.

2. Provider system endpoint setup

Guidance on how a provider system should set up endpoints in Spine Directory Services.


### Consumer System Endpoint Lookup ###

This is a two step process, as follows:

1. Lookup the Accredited System ID (ASID)
2. Lookup the Message Handling System (MHS)

Once the MHS record has been retrieved the fully qualified domain name (FQDN) and full endpoint of the FHIR server can be retrieved from returned attributes of the MHS record.

#### Step 1: Accredited System ID (ASID) Lookup ####

Using an organisation ODS code clients SHALL lookup the Accredited System ID (ASID) as follows:

- Accredited System type
	- objectClass = `nhsAs`
- Organisational code
	- nhsIDCode = *[odsCode]* of the GP organisation.
- Interaction ID
	- nhsAsSvcIA = *[interactionId]* of the GP Connect API operation required.

```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsIDCode=[odsCode]) (objectClass=nhsAS)(nhsAsSvcIA=[interactionId]))" 
	uniqueIdentifier nhsMhsPartyKey
```

The ASID will be returned in the uniqueIdentifier attribute which is returned from the ldaps query above.

Note that ldaps is used to establish a TLS session rather than the StartTLS option. Also note that once the TLS session is established, SASL authentication is not used by SDS and is therefore disabled through the -x option.

Please refer to https://nhsconnect.github.io/gpconnect/development_fhir_operation_guidance.html for details of the GPConnect interactionId appropriate for your use case.

#### Step 2: Message Handling System (MHS) Lookup ####

Clients SHALL lookup the FHIR endpoint from the MHS record using the Party Key retrieved in step 1, as follows:

- Message Handling System type
	- objectClass = `nhsMHS`
- MHS Party Key
	- nhsMHSPartyKey = *[partyKey]* as retrieved from the nhsMhsPartyKey attribute in step 1
- MHS Interaction ID
	- nhsMhsSvcIA = *[interactionId]* of the GP Connect API operation required(?)


```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsMhsPartyKey=[partyKey]) (objectClass=nhsMhs) (nhsMhsSvcIA=[interactionId]))" 
	nhsMhsEndPoint
```

The FHIR endpoint URL of the message handling system can then be extracted from the `nhsMhsEndPoint` attribute of the MHS record. The attribute nhsMhsFQDN could also be retrieved in the above query to retrieve the FQDN of the endpoint, though this can be extracted from the nhsMhsEndPoint.

#### ldapsearch configuration ####

SDS requires TLS Mutual Authentication. It is therefore necessary to configure ldapsearch with the certificates necessary to verify the authenticity of the SDS LDAP server, and also to enable SDS to verify the spine endpoint making the LDAP request:

1. Root and SubCA spine development certificates available from Assurance Support
2. Obtain a client certificate by submitting a certificate signing request for your development endpoint to Assurance Support

##### Server certificate setup #####
For the examples above, ldapsearch should be configured to find the RootCA and SubCA certificates using the TLS_CACERT option in the ldap.conf file. This should point to a file, in PEM format, which contains both root and subca certificates ensuring that the root certificate is placed after the subCA certificae. The LDAPCONF environment vairable can be used to define the location of the ldap.conf 

##### Client certificate setup #####
The client certificate and encrypted private key should be defined in the .ldaprc file using the following directives.

`
TLS_CERT C:\mydir\cert.pem
TLS_KEY C:\mydir\key.pem
`
The location of the .ldaprc file can be defined using the LDAPRC environment variable.

Please contact [Assurance Support service desk (sa.servicedesk@nhs.net)] for certificates and details of the ldap server for your environment.

### Worked example of the endpoint lookup process ###

**Given** 
A consuming system which needs to get the HTML View of a patient record at the patient's registered practice. The consuming system has the following information about the patient:
- NHS Number
- A set of demographic details about the patient

**When** the consuming system interfacts with GP Connect

**Then** the following steps MUST be followed:

#### Step 0. PDS Trace (pre-requisite step)

The Consuming system is responsible for performing a PDS Trace to both verify the identity of the patient and retrieve the ODS code of the patient's registered primary care practice. See https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html

For this example, NHS Number 9000000084 with demographic details Mr Anthony Tester, 19 Ficticious Avenue, Testtown returns the ODS code T99999


#### Step 1. Accredited System Lookup on SDS

The ASID and Party Key is now looked up on SDS. The example below uses ldapsearch:

```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsIDCode=T99999) (objectClass=nhsAS)(nhsAsSvcIA=urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord))" 
	uniqueIdentifier nhsMhsPartyKey
```
This query should return a single matching accredited system object from SDS, the ASID being found in the uniqueIdentifier attribute. In the case, ldapsearch returns the following results:

```bash
# 999999999999, Services, nhs
dn: uniqueIdentifier=9999999999,ou=Services,o=nhs
uniqueIdentifier: 999999999999
nhsMhsPartyKey: T99999-9999999

# search result
search: 1
result: 0 Success
```


#### Step 2: MHS lookup on SDS to determine FHIR base endpoint URL

Using the Party Key retrieved from Step 1, and the same interaction ID, the following ldapsearch query is executed:

```bash
ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsMhsPartyKey=T99999-9999999) (objectClass=nhsMhs) (nhsMhsSvcIA=urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord))" 
	nhsMhsEndPoint nhsMHSFQDN
```

This query should again return a single endpoint. In this case, the ldapquery returns the following results:

```bash
# 472b35d4641b76454b13, Services, nhs
dn: uniqueIdentifier=472b35d4641b76454b13,ou=Services,o=nhs
nhsMhsEndPoint: https://pcs.thirdparty.nhs.uk/T99999/1.0.2/
nhsMHSFQDN: Test14-A20076.EMIS.thirdparty.nhs.uk

# search result
search: 2
result: 0 Success
```


#### Step 3: Consumer constructs full GP Connect request URL to be sent to the Spine Security Proxy

The format of the full URL which the consuming sytem is responsible for constructing is as follows:

`
https://[URL of Spine Security Proxy]/[PCS FHIR Base URL]/[FHIR request]
`

The value returned in the nhsMhsEndPoint attribute in Step 2 should be treated as the FHIR base URL at the Principle Clinical System.

In this example, to issue a GetCareRecord request, the following request would be made:

```bash
POST https://testspineproxy.nhs.domain.uk/https://pcs.thirdparty.nhs.uk/T99999/1.0.2/Patient/$gpc.getcarerecord
```


### Provider System Endpoint Setup ###

The provider system is responsible for populating SDS with the necessary information to enable reliable endpoint lookup by consuming system.

In order to ensure that endpoint lookup is reliable, the following design guidelines must be followed for First of Type implementations:

