---
title: Overview and querying SDS
keywords: spine, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_directory_service.html
summary: "Overview of the role of the Spine Directory Services (SDS) within GP Connect"
---

## Spine Directory Service (SDS) ##

GP Connect consumer systems are expected to resolve the FHIR endpoint for a given GP provider organisation using [Spine Directory Service (SDS)](http://digital.nhs.uk/spine){:target="_blank"} Lightweight Directory Access Protocol (LDAP) directory lookups. SDS is the main information source about NHS-registered users and accredited systems and services.


{% include roadmap.html content="NHS Digital is considering the delivery of a simplified FHIR facade over the Spine Directory Service (SDS) to allow FHIR endpoint resolution to be achieved in a more streamlined (and FHIR compatible) way." %}

Information is provided below to clarify how this endpoint lookup functions.

1. Consuming system viewpoint

	From the perspective of a consuming system, an overview of the endpoint lookup process is given followed by a worked end-to-end example of a GP Connect request to retrieve the HTML view of a patient record.

2. Provider system viewpoint

	Guidance on how a provider system should set up endpoints in Spine Directory Services.


### Consuming system viewpoint ###

The consuming system will interact with SDS to discover the Accredited System ID (ASID) of the target system endpoint, and to resolve the FHIR endpoint server root URL to be used when constructing the request to be made to the Spine Security Proxy. 

This is a two-step process, as follows:

1. Look up the Accredited System ID (ASID)
2. Look up the Message Handling System (MHS)

Once the MHS record has been retrieved the fully qualified domain name (FQDN) and full endpoint of the FHIR server can be retrieved from returned attributes of the MHS record.

GP Connect consuming systems SHOULD cache SDS query results giving details of consuming system, endpoints and endpoint capability on a per session basis. 

Consuming systems SHALL NOT cache and re-use consuming system, endpoint information derived from SDS across multiple patient encounters or practitioner usage sessions. Each new patient encounter will result in new lookups to ascertain the most up-to-date consuming system, endpoint and endpoint capability.


#### Step 1: Accredited System ID (ASID) lookup ####

Using an organisation ODS code, clients SHALL look up the ASID as follows:

- Accredited system type
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

The ASID will be returned in the uniqueIdentifier attribute returned from the LDAPS query above. This ASID will be used as the value for the `Ssp:To` header in the request to the [Spine Security Proxy](https://nhsconnect.github.io/gpconnect/integration_spine_security_proxy_implementation_guide.html#consumer).

Note that ldaps is used to establish a TLS session rather than the StartTLS option. Also note that once the TLS session is established, SASL authentication is not used by SDS and is therefore disabled through the -x option.

Please refer to [FHIR operation guidance](development_fhir_operation_guidance.html) for details of the GP Connect interactionId appropriate for your use case.


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

SDS requires Transport Layer Security (TLS) Mutual Authentication. It is therefore necessary to configure ldapsearch in the examples above with the certificates necessary to verify the authenticity of the SDS LDAP server, and to enable SDS to verify the Spine endpoint making the LDAP request:

1. RootCA and SubCA Spine development certificates available from Assurance Support.
2. Obtain a client certificate by submitting a certificate signing request for your development endpoint to Assurance Support.

##### Server certificate setup #####
For the examples above, ldapsearch should be configured to find the RootCA and SubCA certificates using the TLS_CACERT option in the ldap.conf file. This should point to a file, in Privacy Enhanced Mail (PEM) format, which contains both RootCA and SubCA certificates ensuring that the root certificate is placed after the SubCA certificate. The LDAPCONF environment variable can be used to define the location of the ldap.conf 

##### Client certificate setup #####
The client certificate and encrypted private key should be defined in the .ldaprc file using the following directives.

`
TLS_CERT C:\mydir\cert.pem
TLS_KEY C:\mydir\key.pem
`

The location of the .ldaprc file can be defined using the LDAPRC environment variable.

Please contact [Assurance Support service desk](mailto:sa.servicedesk@nhs.net) for certificates and details of the LDAP server for your environment.

### Worked example of the endpoint lookup process ###

**Given**
A consuming system which needs to get the HTML view of a patient record at the patient's registered practice. The consuming system has the following information about the patient:
- NHS number
- a set of demographic details about the patient

**When**
The consuming system interacts with GP Connect

**Then** 
The following steps MUST be followed:


#### Step 0. PDS trace (pre-requisite step)

The consuming system is responsible for [performing a PDS trace](integration_personal_demographic_service.html) to both verify the identity of the patient and retrieve the ODS code of the patient's registered primary care practice. 

For this example, NHS number 9000000084 with demographic details Mr Anthony Tester, 19 Fictitious Avenue, Testtown returns the ODS code T99999.


#### Step 1. Accredited system lookup on SDS

The ASID and party key is now looked up on SDS. The example below uses ldapsearch:

	
	ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsIDCode=T99999) (objectClass=nhsAS)(nhsAsSvcIA=urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-1))" 
	uniqueIdentifier nhsMhsPartyKey
	
This query should return a single matching accredited system object from SDS, the ASID being found in the uniqueIdentifier attribute. In the case, ldapsearch returns the following results:


	999999999999, Services, nhs
	dn: uniqueIdentifier=9999999999,ou=Services,o=nhs
	uniqueIdentifier: 999999999999
	nhsMhsPartyKey: T99999-9999999

	# search result
	search: 1
	result: 0 Success

	
#### Step 2: MHS lookup on SDS to determine FHIR endpoint server root URL

Using the party key retrieved from Step 1, and the same interaction ID, the following ldapsearch query is executed:

	ldapsearch -x -H ldaps://ldap.vn03.national.ncrs.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsMhsPartyKey=T99999-9999999) (objectClass=nhsMhs) (nhsMhsSvcIA=urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-1))" 
	nhsMhsEndPoint nhsMHSFQDN
	

This query should again return a single endpoint. In this case, the ldapquery returns the following results:

	# 472b35d4641b76454b13, Services, nhs
	dn: uniqueIdentifier=472b35d4641b76454b13,ou=Services,o=nhs
	nhsMhsEndPoint: https://pcs.thirdparty.nhs.uk/T99999/DSTU2/1
	nhsMHSFQDN: pcs.thirdparty.nhs.uk

	# search result
	search: 2
	result: 0 Success
	


#### Step 3: Consumer constructs full GP Connect request URL to be sent to the Spine Security Proxy

The format of the full URL which the consuming system is responsible for constructing is as follows:

`https://[URL of Spine Security Proxy]/[Provider Server Root URL]/[FHIR request]`

The value returned in the nhsMhsEndPoint attribute in Step 2 should be treated as the FHIR Server Root URL at the provider system.

In this example, to issue a GetCareRecord request, the following request would be made:

`POST https://testspineproxy.nhs.domain.uk/https://pcs.thirdparty.nhs.uk/T99999/DSTU2/1/Patient/$gpc.getcarerecord`

## Code examples

Code examples for the interaction with the SDS are available in the following github repositories. The respositories contain a `SpineDirectoryService` folder which holds the code examples for interacting with the SDS.

[.NET](https://github.com/nhsconnect/gpconnect-dotnet-examples)

[JAVA](https://github.com/nhsconnect/gpconnect-java-examples)

