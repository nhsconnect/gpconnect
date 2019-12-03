---
title: Registering GP Connect systems in SDS
keywords: spine, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_sds_registering_endpoints.html
summary: "Overview of the role of the Spine Directory Services (SDS) within GP Connect"
div: newheaders
---

{% include important.html content="SDS registration for consumer systems is normally handled by NHS Digital. Please contact the GP Connect programme if you are unsure." %}

## 1. Common SDS requirements ##

### 1.1 Unique ASID per organisation using a system ###

Every system using GP Connect **MUST** have a unique ASID for each organisation using it, so the same system deployed into three organisations would be represented by three unique ASIDs.

Conversely, if two different consumer systems are deployed in a single organisation, two unique ASIDs would be required.

Shared systems such as a *Regional portal* which are provisioned by a single organisation, but used by other organisations, **MUST** have a unique ASID per organisation using the system.

{% include note.html content="When sending GP Connect requests, the ASID of the organisation **making the GP Connect request** **MUST** be sent in the `Ssp-From` header to ensure the true 'originator' of the request is properly declared. Shared systems **MUST NOT** send the provisioning organisation's ASID." %}

### 1.2 Do not reuse GP Connect ASIDs and Party Keys for central Spine services ###

New GP Connect ASIDs and Party Keys must be registered for use with GP Connect; existing ASIDs and Party Keys for central Spine services **MUST NOT** be reused.

### 1.3 Maximum of one GP Connect provider system per organisation ###

Only one GP Connect provider system can be registered in SDS for an organisation; multiple provider systems for the same organisation are NOT supported.

### 1.4 Multiple GP Connect consumer systems per organisation to be supported ###

Only one consumer system per organisation is supported currently (as of March 2019). However, once all providers and consumers have migrated to version 0.7.2 of the GP Connect API specification - specifically uplifting their [SDS queries](integration_spine_directory_service.html) - more than one will be supported.

Examples:

- An urgent care centre with an Access Record HTML consumer system, and a separate Appointments consumer system
- A GP practice using a GP system with GP Connect enabled as provider and consumer, and a separate regional portal system with access to Access Record HTML as a consumer

{% include important.html content="**Distinguishing provider and consumer SDS records**<br/>
Providers have GP Connect [interaction IDs](integration_interaction_ids.html) on their SDS MHS record; consumers do not.  This distinction enables the [SDS queries](integration_spine_directory_service.html) to look up a GP Connect provider endpoint to function correctly." %}

---

## 2. Consumer specific SDS requirements ##

{% include important.html content="If a system is both a consumer and provider (e.g. a GP principal system), please refer to [Provider requirements below](#3-provider-specific-sds-requirements) instead" %}

### 2.1 Use separate MHS and AS endpoint records; not CMA style endpoints ###

Consumers **MUST NOT** register entries in SDS as CMA (combined MHS and AS) style endpoints.  This is because the MHS record for a consumer system **MUST NOT** have GP Connect interactions on the endpoint, whereas the AS record MUST - creating a CMA style endpoint will not allow this distinction to be made.

### 2.2 GP Connect Interactions IDs on AS records only ###

GP Connect [interaction IDs](integration_interaction_ids.html) on AS records indicate the system is permitted to send GP Connect messages as a consumer.

GP Connect [interaction IDs](integration_interaction_ids.html) on an MHS record indicate the Messaging Handling Server is a GP Connect provider, therefore this **MUST NOT** be done for consumer (only) systems.

### 2.3 Shared Party Key may be used depending on topology ##

Consumer systems MAY use a single GP Connect Party Key for multiple organisations, if they connect to Spine via a single shared message handling server.

However, as per [1.1 Unique ASID per system used by an organisation](#11-unique-asid-per-organisation-using-a-system) each consumer organisation **MUST** have its own unique ASID.

Please see [System topologies](integration_system_topologies.html) for more information.

---

## 3. Provider specific SDS requirements ##

{% include important.html content="These requirements apply to provider systems, including those that offer provider and consumer functionality within the same system" %}

### 3.1 Use CMA type endpoints ###

In order to allow for practice specific routing using endpoint, all systems **MUST** have a unique GP Connect Party Key and ASID per practice, registered in SDS as a "CMA type" endpoint.

A CMA type endpoint refers to an endpoint which is a combined MHS system and accredited system endpoint. There will be a 1-1 mapping between an Accredited System (uniquely identified by an ASID) record and a Message Handling System (MHS) record. A single MHS record **MUST** be associated with a given ASID and interaction ID.

### 3.2 GP Connect Interaction IDs on MHS and AS records  ###

GP Connect Interaction IDs **MUST** be registered on both MHS and AS records (using a CMA type endpoint).

GP Connect [interaction IDs](integration_interaction_ids.html) on an MHS record indicate the Messaging Handling Server is a GP Connect provider.

### 3.3 Provider systems who are also consumers use the same ASID and Party Key for both roles ###

Provider systems which also offer consumer functionality **MUST** use the same GP Connect Party Key and ASID for both provider and consumer roles.

### 3.4 Format of Service Root URL ###

The *Service Root URL* for a given ASID **MUST** be defined in the `nhsMhsEndPoint` attribute of the MHS record (i.e. the LDAP object of type nhsMhs). This URL **MUST** be in the format described in [Service Root URL versioning](development_general_api_guidance.html#service-root-url) guidance.

As described in the [API versioning](development_general_api_guidance.html#fhir-api-versioning) guidance, the practice's ODS code  **MUST** be placed in the FHIR server root URL, and this **MUST** match the value in the `nhsidcode` elements on the MHS and associated AS records.  ODS codes which refer to clinical systems as a single entity **MUST NOT** be used to provide routing. Practice specific ODS codes **MUST** be used for routing purposes in the FHIR Server Root URL found in the `nhsMhsEndPoint` attribute of the MHS record.

### 3.5 nhsMhsEndPoint attribute **MUST** contain the FHIR service root URL only ###

The `nhsMhsEndPoint` attribute in the MHS record **MUST** contain the [FHIR Service Root URL](development_general_api_guidance.html#service-root-url). It is the responsibility of the consuming system to construct the FHIR operation or RESTful resource request which will be postfixed to this base URL.

An example of a FHIR server root URL for a [Retrieve a care record section](accessrecord_use_case_retrieve_a_care_record_section.html) interaction at practice GP0001 is:

`https://provider.thirdparty.nhs.uk/GP0001/STU3/1`

Note that the `/Patient/$gpc.getscarerecord` is NOT added.

In line with this, provider systems **SHOULD** perform checks that the FHIR request received is a reasonable means to request the resource in view given the specified interaction. 

### 3.6 FHIR service root URLs associated with a given product set **MUST** use same FHIR version ###

Where a provider moves in future to a later version of FHIR, it will be necessary to define a new product set to accommodate the set of interactions provided by this. FHIR server root URLs defined for a specific product set **MUST** all reference the same FHIR version. This ensures that FHIR resources references returned in FHIR responses are locally resolvable. 

For example, all interactions associated with the Appointment Management capability pack in a given product set must refer to the same FHIR server, so that the resource references for 'Read Appointment' and 'Amend' appointment would be locally resolvable to the same resource on the same FHIR Server. 

### 3.7 Acceptable use of ASID information in HTTP Headers ###

Source and destination ASID information is passed to the provider system from the Spine Security Proxy. Providers **MUST** use this information for audit and debugging purposes only, and **MUST NOT** use these headers to perform routing or lookups. 

It is the responsibility of the SSP to perform lookups to determine consumer accreditation status. Routing shall be carried out as described above through practice-specific ODS codes present in the FHIR server root URL. 


---

## SDS terminology ##

{% include sds_terminology.html %}
