---
title: Provider API Versioning Guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_versioning_provider_guidance.html
summary: "Details of the versioning requirements for GP Connect providers."
---

FHIR APIs SHALL be versioned according to  [Semantic Versioning](http://semver.org/spec/v2.0.0.html) in the server's Service Root URL to provide a clear distinction between API versions that are incompatible (i.e. contain breaking changes) vs. backwards-compatible (i.e. contain no breaking changes).

Provider systems are required to publish Service Root URLs for major versions of FHIR APIs in the Spine Directory Service in the following format:

{% include callout.html content="`https://[FQDN of FHIR Server]/[ODS Code]/[FHIR_VERSION_NAME]/{PROVIDER_MAJOR_VERSION}`" %}

- `[FQDN of FHIR Server]` is the fully qualified domain name where traffic will be routed to the logical FHIR server for the organisation in question

- `[ODS Code]` is the [Organisation Data Service](https://digital.nhs.uk/organisation-data-service) code which uniquely identifies the GP Practice organisation

- `[FHIR_VERSION_NAME]` refers to the textual name identifying the major FHIR version, examples being `DSTU2` and `STU3`. The FHIR Version name SHALL be specified in UPPERCASE characters.

- `{PROVIDER_VERSION}` identifies the major version number of the provider API. Where the provider version number is omitted, the major version SHALL be assumed to be 1.
  
- The FHIR Base URL SHALL NOT contain a trailing `/`

### Example Server Root URL ###

For example if a provider implements the "Access Record HTML 1.0.0-rc.5" and then implements "Access Record HTML 1.0.0-rc.6" which includes a breaking change and uplift of the InteractionID with a new major version, as specified in the [FHIR Capability Versioning Guidance](development_fhir_versioning_capability_guidance.html) page, the provider would create a new endpoint for the new version of the capability.

| Provider Registered endpoint | InteractionID Endpoint is registered against in SDS | Capability Version |
| --- | --- |
| https://provider.nhs.uk/GP0001/DSTU2/1 | urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord | Access Record HTML 1.0.0-rc.5 |
| https://provider.nhs.uk/GP0001/DSTU2/2 | urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-2 | Access Record HTML 1.0.0-rc.6 |


If a provider has developed a new version of their FHIR API for practice GP0001 which is running FHIR STU3. The provider would publish the server root URL to Spine Directory Services as follows:

| Provider Registered endpoint | InteractionID Endpoint is registered against in SDS |
| --- | --- |
| https://provider.nhs.uk/GP0001/STU3/1 | urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord-3 |
