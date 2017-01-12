---
title: Spine Directory Service
keywords: spine, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_directory_service.html
summary: "Overview of the role of the Spine Directory Services (SDS) within GP Connect."
---

{% include warning.html content="This page is a preliminary working draft and hence is subject to change." %}

## Spine Directory Service (SDS) ##

GP Connect Consumer systems are expected to resolve the FHIR endpoint for a given GP Provider organisation using [Spine Directory Service (SDS)](http://digital.nhs.uk/spine){:target="_blank"} LDAP directory lookups. SDS is the main information source about NHS registered users and accredited systems and services.

This is a two step process, as follows:

1. Lookup the Accredited System ID (ASID)
2. Lookup the Message Handling System (MHS)

Once the MHS record has been retrieved the fully qualified domain name (FQDN) and full endpoint of the FHIR server can be retrieved from returned attributes of the MHS record.

{% include roadmap.html content="NHS Digital is considering the delivery of a simplified FHIR façade over the Spine Directory Service (SDS) to allow FHIR endpoint resolution to be achieved in a more streamlined (and FHIR compatible) way." %}





### Accredited System ID (ASID) Lookup ###

Using an organisation ODS code clients SHALL lookup the Accredited System ID (ASID) as follows:

- Accredited System type
	- objectClass = `nhsAs`
- Organisational code
	- nhsIDCode = *[odsCode]* of the GP organisation.
- Interaction ID
	- nhsAsSvcIA = *[interactionId]* of the GP Connect API operation required.

```bash
ldapsearch -H ldaps://ldap.vn03.national.ncrs.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsIDCode=[odsCode]) (objectClass=nhsAS)(nhsAsSvcIA=[interactionId]))" 
	uniqueIdentifier nhsMhsPartyKey
```

The ASID will be returned in the uniqueIdentifier attribute which is returned from the ldaps query above.

### Message Handling System (MHS) Lookup ###

Clients SHALL lookup the FHIR endpoint from the MHS record using the Party Key retrieved in step 1, as follows:

- Message Handling System type
	- objectClass = `nhsMHS`
- MHS Party Key
	- nhsMHSPartyKey = *[partyKey]* as retrieved from the nhsMhsPartyKey attribute in step 1
- MHS Interaction ID
	- nhsMhsSvcIA = *[interactionId]* of the GP Connect API operation required(?)


```bash
ldapsearch -H ldaps://ldap.vn03.national.ncrs.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsMhsPartyKey=[partyKey]) (objectClass=nhsMhs) (nhsMhsSvcIA=[interactionId]))" 
	nhsMhsEndPoint
```

The FHIR endpoint URL of the message handling system can then be extracted from the `nhsMhsEndPoint` attribute of the MHS record. The attribute nhsMhsFQDN could also be retrieved in the above query to retrieve the FQDN of the endpoint, though this can be extracted from the nhsMhsEndPoint.

### ldapsearch configuration ###

SDS requires TLS Mutual Authentication. It is therefore necessary to install the following certificates:

1. Root and SubCA spine development certificates
2. Obtain a client certificate by submitting a certificate signing request for your development endpoint to Assurance Support

For the examples above, ldapsearch should be configured to find the RootCA and SubCA certificates using the TLS_CACERT option in the ldap.conf file. This should point to a file which contains both root and subca certificates ensuring that the root certificate is placed after the subCA certificae.

The client certificate should be defined in the .ldaprc using the TLS_CERT option. This should again point to a file which contains the client certificate followed by the subCA certificate, then finally the root certificate.

Please contact [Assurance Support service desk (sa.servicedesk@nhs.net)] for certificates and details of the ldap server for your environment.

