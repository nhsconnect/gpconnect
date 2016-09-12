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

GP Connect Consumer systems are expected to resolve the FHIR endpoint for a given GP Provider organisation using the [Spine Directory Service (SDS)](http://systems.digital.nhs.uk/ddc/spine-directory-service){:target="_blank"} LDAP:

This is a two step process, as follows:

1. Lookup the Accredited System ID (ASID)
2. Lookup the Message Handling System (MHS)

Once the MHS record has been retrieved the fully qualified domain name (FQDN) of the FHIR server can be extracted.

{% include roadmap.html content="NHS Digital is considering the delivery of a simplified FHIR façade over the Spine Directory Service (SDS) to allow FHIR endpoint resolution to be achieved in a more streamlined (and FHIR compatible) way." %}

### Accredited System ID (ASID) Lookup ###

Using an organisation ODS code client's SHALL lookup the Accredited System ID (ASID) as follows:

- Accredited System type
	- objectClass = `nhsAs`
- Organisational code
	- nhsIDCode = *[odsCode]* of the GP organisation.
- Interaction ID
	- nhsAsSvcIA = *[interactionId]* of the GP Connect API operation required.

```bash
ldapsearch -h ldap.spine.nhs.uk –b "ou=services, o=nhs" 
	"(&(nhsIDCode=[odsCode]) (objectClass=nhsAS)(nhsAsSvcIA=[interactionId]))" 
	uniqueIdentifier nhsMhsPartyKey
```

### Message Handling System (MHS) Lookup ###

Clients SHALL lookup the Party Key / Message Handling System (MHS) as follows:

- Message Handling System type
	- objectClass = `nhsMHS`
- MHS Part Key
	- nhsMHSPartyKey = *[partKey]* as extracted from the ASID record.
- MHS Interaction ID
	- nhsMhsSvcIA = *[interactionId]* as extracted from the ASID record.

The fully qualified domain name of the message handling system can then be extract from the `nhsMhsFQDN` field of the MHS record (e.g. [system].[vendor].nme.ncrs.nhs.uk).

```bash
ldapsearch -h ldap.spine.nhs.uk -b "ou=services, o=nhs" 
	"(&(nhsMhsPartyKey=[partKey]) (objectClass=nhsMhs) (nhsMhsSvcIA=[interactionId]))" 
	nhsMhsEndPoint nhsMhsIsAuthenticated
```

The FHIR endpoint URL of the message handling system can then be extracted from the `nhsMhsEndPoint` field of the MHS record.

{% include links.html %}