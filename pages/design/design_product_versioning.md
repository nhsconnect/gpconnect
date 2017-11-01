---
title: GP Connect API Versioning
keywords: development, versioning
tags: [development]
sidebar: overview_sidebar
permalink: design_product_versioning.html
summary: An overview of GP Connect API versioning.
---

## Specification Versioning ##

The GP Connect API specification consists of the following sub sections outlining specific capabilities within the GP Connect API but the GP Connect API specification is versioned by an overarching single version which is shown above the sidebar, below the NHS Digital logo.

| Specification Section | What is included in the specification section |
| --- | --- |
| [GP Connect](/index.html) | This section of the specification is targeted at the cross cutting requirements and guidance common to all capabilities. Also included are overarching principles used by the GP Connect project when creating and implementing any aspect of the GP Connect specification and project. |
| [Access Record HTML](/accessrecord.html) | This section contains requirements and details for development specific to the Access Record HTML capability. |
| [Access Record REST](/accessrecord_rest.html) |This section contains the requirements and details relating to the Access Record REST capability for access to structured data. |
| [Foundations](/foundations.html) | This section of the specification relates to the requirements and details required for implementing the Foundation capabilities. |
| [Appointment Management](/appointments.html) | This section of the specification relates to the requirements and implementation details specifically relating to the Appointment Management capabilities. |
| [Task Management](/tasks.html) | This section of the specification relates to the requirements and details needed to implement the Task Management capability. |


### Versioning Style ###

The GP Connect API is versioned using [Semantic Versioning 2.0.0](http://semver.org/){:target="_blank"}, using the format "***MAJOR.MINOR.PATCH***".

The separate components of the version will be updated as per below for each update of the specification:

- MAJOR version when you make incompatible API changes.
- MINOR version when you add functionality in a backwards-compatible manner.
- PATCH version when you make backwards-compatible bug fixes.

In addition a pre-release version MAY be denoted by appending a hyphen (refer to [Semantic Versioning - Item 9](http://semver.org/#spec-item-9){:target="_blank"}) along with a pre-release label for the type of release.

### Pre-release Labels ###

The following pre-release labels will be used:

| Pre-release Label | Lifecycle | Description |
|-------------------|-----------|-------------|
| `alpha` | &nbsp; | Complete enough for internal testing. |
| `beta` | early | Complete enough for external testing. |
| `beta` | late | Complete enough for external testing. Usually feature complete. |
| `rc` | &nbsp; | Release Candidate - Almost ready for final release. No new feature enhancements. |

Example: 1.0.0-alpha.1 is an example of a valid pre-release version.


### Specification Versioning Maturity Levels ###

Taking a similar approach to the [FHIR Maturity Model](http://wiki.hl7.org/index.php?title=FHIR_Maturity_Model){:target="_blank"} GP Connect will only freeze / master a technical specification once it has been independently implemented in at least three commercial systems and demonstrated to interoperate.

| Level | Version | Description | 
|-------|---------|-------------| 
| 1 | `X.Y.Z-alpha.n` | Alpha; rapid interactions, fail fast, exploration, proof of concepts, approach flexible. | Draft may not have been implemented at all but has been published. |
| 2 | `X.Y.Z-beta.n` | Early Beta; rapid iterations, community engaged, scope flexible, high-level approach agreed in principle. | Draft partially implemented in one or more prototype systems. |
| 3 | `X.Y.Z-beta.n` | Late Beta; slower iterations, community engaged, scope largely agreed, high-level approach fixed. | Draft partially implemented two or more commercial systems. |
| 4 | `X.Y.Z-rc.n` | Release Candidate; slower iterations, community engaged, scope fixed, detailed approach fixed, no new features, bug fixes and amendments for clinical safety & IG only. | Draft implemented in at least two commercial systems. |
| 5 | `X.Y.Z` | Stable; release version. | Draft implemented in at least three commercial systems with full accreditation and assurance mechanisms in place. |



### Interaction versioning ###

For each of the five capability packs (`Foundations`, `Access Record HTML`, `Access Record REST`, `Appointment Management`, `Task Management`) there are a number of `API Use Cases` which make up the capability pack, for example "Find a patient" and "Read an organization" are two of the API Use Cases within the Foundation capability pack.

Each API Use Case has an associated InteractionID. The InteractionID for each API Use Case is specified within the relevant Capability Packs, for example the "Find a patient" interaction is listed in the [Spine Interactions for the Foundations Capability Pack](foundations.html#spine-interactions).

InteractionsIDs in early versions of the specification did not contain a version number, but going forward the interactionID will contain the major GP Connect API version number. A new version of the interaction will be issued with each major change to the GP Connect API.


### FHIR resource versioning ###

#### Major FHIR resource profile versions ####

The versioning of profiled FHIR resources will follow semantic versioning where a breaking change will result in a major version change and non-breaking changes will result in a minor version change. The FHIR Resource Profile names contain the major version number for the Profiled FHIR Resource, for example "CareConnect-GPC-Organization-2" is version two of the Organization resource profile. A breaking change within the profile will result in a new major version and therefore new FHIR Resource Profile will be created.

Example Profiled FHIR Resource version changes:

| FHIR resource profile name| Example reason for version change |
| --- | --- |
| CareConnect-GPC-Patient-1 | Starting Profiled FHIR resource. |
| CareConnect-GPC-Patient-2 | A change to add a mandatory field to the Profiled FHIR Resource. |
| CareConnect-GPC-Patient-3 | A change to restrict the cardinality of a field from "0..*" to "1..1". |

#### Minor FHIR resource profile versions ####

Minor version changes will not result in a change to the FHIR Resource Profile name as the different versions of the FHIR Resource Profiles should be interoprable. All the FHIR Resource profiles are made available on the [FHIR Reference Server](https://fhir.nhs.uk/StructureDefinition), the minor version of the FHIR Resource Profile are available using the standard FHIR "_history" capability to specify the exact version of the resource definition that you wish to retrieve. For Example:

| URL to use for FHIR Reference Server | Version of profile which will be returned|
| --- | --- |
| https://fhir.nhs.uk/StructureDefinition/CareConnect-GPC-Organization-1/_history/1.1 | Minor Version 1.1 |
| https://fhir.nhs.uk/StructureDefinition/CareConnect-GPC-Organization-1/_history/1.2 | Minor Version 1.2 |


### Valueset versioning ###
Valuesets are not currently versioned and GP Connect is aware there is a risk surrounding this and the affects it may have on the capabilities if valuesets are uplifted. If a valueset is altered or uplifted the risk will be managed at the time.


## Provider versioning ##

### Provider supported versions ###

Providers are expected to maintain both the current and previous major version of the GP Connect API, ie. "n" and "n-1" where n is the currently major version of the GP Connect API and n-1 is the previous major version of the GP Connect API. The requirement for a provider to maiantain both the latest version and the previous version is to maintain interoperability between systems as each of the providers and consumers uplift their product to support the latest version of GP Connect API.

Minor uplifts to the GP Connect API should retain interopable with other minor versions within the same major version of the GP Connect API. Providers and consumers should update to the latest minor version of the GP Connect API for each of their supported major API versions to make available improvements and fixes to the GP Connect API.


### Provider endpoint registration ###

Provider systems are required to publish a Service Root URL in the Spine Directory Service in the following format:

{% include callout.html content="`https://[FQDN of FHIR Server]/[ODS Code]/[FHIR_VERSION_NAME]/{PROVIDER_MAJOR_VERSION}`" %}

- `[FQDN of FHIR Server]` is the fully qualified domain name where traffic will be routed to the logical FHIR server for the organisation in question

- `[ODS Code]` is the [Organisation Data Service](https://digital.nhs.uk/organisation-data-service) code which uniquely identifies the GP Practice organisation

- `[FHIR_VERSION_NAME]` refers to the textual name identifying the major FHIR version, examples being `DSTU2` and `STU3`. The FHIR Version name SHALL be specified in UPPERCASE characters.

- `{PROVIDER_VERSION}` identifies the version of the provider API. The version is required in the url to aid with error investigation if problems occur when a consumers tries to call a providers endpoint.
  
- The FHIR Base URL SHALL NOT contain a trailing `/`


#### Example server root URL ####

``` https://provider.nhs.uk/GP0001/DSTU2/3 ```

``` https://provider.nhs.uk/GP0001/STU3/1 ```


Providers SHALL register an endpoint within the SDS for each IntereactionId supported by the FHIR server on the Principal GP system. Information on registering endpoints can be found on the [Spine Directory Services](integration_spine_directory_service.html#provider-system-viewpoint) page.


## Consumer versioning ##

As the providers will register on the SDS an endpoint for each InteractionId and the InteractionId contains the specification major version of the interaction, if a consumer wishes to find the endpoint which supports a specific version of an interaction they support, the consumer needs to perform a sequence of query operations against the existing Spine services as described in [Spine Integration Illustrated](integration_illustrated.html). 
