---
title: Provider API versioning guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_versioning_provider_guidance.html
summary: "Details of the versioning requirements for GP Connect providers"
---

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


#### Supported interactions ####

A Providers endpoint should support the current and the previous version of each supported interaction (n and n-1) as specified on the [FHIR Capability Versioning Guidance](development_fhir_versioning_capability_guidance.html) page.

