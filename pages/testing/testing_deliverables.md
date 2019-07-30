---
title: Testing assets
keywords: testing deliverables
tags: [testing]
sidebar: overview_sidebar
permalink: testing_deliverables.html
summary: "Details of what test resources have been made available to support the holistic <br/>testing of provider APIs and consumer applications."
---

## Provider testing (SIT) ##

An automated provider test harness has been made publicly available to allow standardised testing of the FHIR APIs prior to any formal assurance activities being undertaken. This approach aims to streamline the end-to-end assurance process by ensuring that a common baseline level of technical conformance has been achieved, and thus fewer issues are surfaced during formal assurance.

{% include download.html content="Download the [GP Connect Provider Test Suite](https://github.com/nhsconnect/gpconnect-provider-testing) to help validate the technical conformance of your provider API implementation." %}

### Provider testing layers ###

| Category | Layer  | Details  |
|----------|--------|----------|
| Provider capability      | API orchestration | Use cases |
| Provider terminology     | API data layer    | Test cases |
| Technical      | API payload(s)    | FHIR profile conformance, valueset usage, constraint rules   |
| Technical      | API conformance   | URL format, URL parameters, HTTP error handling |
| Standards      | FHIR DSTU2 conformance  | metadata, RESTful, identifier handling, search patterns |
| Technical      | Spine integration | SSL certificate handling, URL format, SSP headers |
| Standards      | HTTP conformance  | accept encodings, transfer encodings, ETags compression |
| Standards      | JWT conformance  | authentication, claims, auditing |
| Standards      | SSL conformance  | TLS versions, supported ciphers, client authentication, certificate revocation |

Please see the [GP Connect Provider Testing Wiki](https://github.com/nhsconnect/gpconnect-provider-testing/wiki) for further details.

{% include note.html content="Generic FHIR test harness such as [Crucible](http://www.projectcrucible.org/), [Sprinklr](https://github.com/furore-fhir/sprinkler) and [TouchStone](http://www.aegis.net/touchstone.html) may also be of interest to implementers." %}

### Non functional ###

| Category       | Layer               | Details          |
|----------------|---------------------|------------------|
| Security       | Penetration testing | OSWASP top 10    |
| Performance    | API performance     | Response times   |
| Volumetrics    | API TPS             | LOAD, RAMP, SOAK |

## Consumer testing (SIT) ##

### Consumer testing layers ###

An additional UI testing layer is required for consumer systems.

| Category            | Layer         | Details                |
|---------------------|---------------|------------------------|
| Consumer capability | UI behaviours | UI use case automation |

### Non functional ###

| Category       | Layer               | Details          |
|----------------|---------------------|------------------|
| Security       | Penetration testing | OSWASP top 10    | 

{% include note.html content="Formal V&P testing is not required for consumer applications." %}
