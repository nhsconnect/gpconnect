---
title: FHIR Capability Versioning Guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_versioning_capability_guidance.html
summary: "Details of the common versioning requirements for GP Connect FHIR APIs."
---

### Capability / Interaction Versioning ###

For each capability (e.g. "Find a patient", "Search for free slots", etc) there is an InteractionID associated with that capability. The InteractionID for each capability is specified within the relevant Capability Packs, for example the "Find a patient" interaction is listed in the [Spine Interactions for the Foundations Capability Pack](foundations.html#spine-interactions).

InteractionsIDs in early versions of the specification did not contain a version number, but going forward a major version number will now be added. A new version of the interaction will be issued when there is a breaking change made within the interaction, for example if a Profiled FHIR resources used as part of the interaction is changed but is not backwardly compatible with the previous versions of the profiled FHIR resources, this would result in a new major version of the interaction.

Example of InteractionID versioning:

| Interaction-ID | Reason for interaction version |
| --- | --- |
| urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord | Initial InteractionID used for "Access Record HTML 1.0.0-rc.5". |
| urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-2 | A Profiled FHIR Resource breaking change from "GPConnect-Patient-1" FHIR resource to "CareConnect-GPC-Patient-1" FHIR Resource, released in Access Record HTML 1.0.0-rc.6. |
| urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-3 | This will be the next InteractionID which will be used for the next breaking change to the Access Record HTML capability. |

Providers will register a new endpoint within the SDS for new interactions, therefore when "urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-2" is developed by the provider there would be two endpoints registered on the SDS, one for the old "urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord" Access Record interaction and one for the new "urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-2" interaction. Details relating to the specifics of provider endpoints and provider endpoint versioning is specified on the [Provider API Versioning Guidance](/development_fhir_versioning_provider_guidance.html) page.


#### Provider Supported Versions ####

Providers are expected to maintain both the current and previous version of each capability, ie. "n" and "n-1", to maintain interoperability between systems as each of the providers and all of the consumers uplift to the latest version of the capability.


### FHIR Resource Versioning ###

#### Major FHIR Resource Profile Versions ####

The versioning of profiled FHIR resources will follow the other versioning within the specification where a breaking change will result in a major version change and non-breaking changes will result in a minor version change. The FHIR Resource Profile names contain the major version number for the Profiled FHIR Resource, for example "CareConnect-GPC-Organization-2" is version two of the Organization resource profile. 

Example Profiled FHIR Resource version changes:

| FHIR resource profile name| Example reason for version change |
| --- | --- |
| CareConnect-GPC-Patient-1 | Starting Profiled FHIR resource. |
| CareConnect-GPC-Patient-2 | A change to add a mandatory field to the Profiled FHIR Resource. |
| CareConnect-GPC-Patient-3 | A change to restrict the cardinality of a field from "0..*" to "1..1". |

#### Minor FHIR Resource Profile Versions ####

Minor version changes will not result in a change to the FHIR Resource Profile name, major version changes will result in a new FHIR Resource Profile name. The FHIR Resource profiles are made available on the [FHIR Reference Server](https://fhir.nhs.uk/StructureDefinition), the minor version of the FHIR Resource Profile are available using the standard FHIR "_history" capability to specify the exact version of the resource definition that you wish to retrieve. For Example:

| URL to use for FHIR Reference Server | Version of profile which will be returned|
| --- | --- |
| https://fhir.nhs.uk/StructureDefinition/CareConnect-GPC-Organization-1/_history/1.1 | Minor Version 1.1 |
| https://fhir.nhs.uk/StructureDefinition/CareConnect-GPC-Organization-1/_history/1.2 | Minor Version 1.2 |

If the Profiled FHIR Resource is changed with a new major version this will probably also result in an uplift to the InteractionID  for that capability.


### Valueset Versioning ###
Valuesets are not currently versioned and GP Connect is aware there is a risk surrounding this and the affects it may have on the capabilities if valuesets are uplifted. If a valueset is altered or uplifted the risk will be managed at the time.
