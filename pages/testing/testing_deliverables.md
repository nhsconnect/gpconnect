---
title: Testing assets
keywords: testing deliverables
tags: [engagement,testing]
sidebar: overview_sidebar
permalink: testing_deliverables.html
summary: "Details of what test resources have been made available to support the holistic testing of provider APIs and consumer applications."
---

## Provider testing (SIT) ##

An automated provider test harness has been made publically available to allow standardised testing of the FHIR APIs prior to any formal assurance activities being undertaken. This approach aims to streamline the end-to-end assurance process by ensuring that a common baseline level of technical conformance has been achieved and, thus, fewer issues are surfaced during formal assurance.

{% include download.html content="Download the [GP Connect Provider Test Suite](https://github.com/nhsconnect/gpconnect-provider-testing) to help validate the technical conformance of your provider API implementation." %}

### Provider Testing Layers ###

| Category | Layer  | Details  |
|----------|--------|----------|
| Provider Capability      | API Orchestration | Use Cases |
| Provider Terminology     | API Data Layer    | Test Cases |
| Technical      | API Payload(s)    | FHIR Profile Conformance, ValueSet Usage, Constraint Rules   |
| Technical      | API Conformance   | URL Format, URL Parameters, HTTP Error Handling |
| Standards      | FHIR Conformance  | Metadata, RESTful, Identifier Handling, Search Patterns |
| Technical      | Spine Integration | SSL Certificate Handling, URL Format, SSP Headers |
| Standards      | HTTP Conformance  | Accept Encodings, Transfer Encodings, ETags Compression |
| Standards      | JWT Conformance  | Authentication, Claims, Auditing |
| Standards      | SSL Conformance  | TLS Versions, Supported Ciphers, Client Authentication, Certificate Revocation |

Please see the [GP Connect Provider Testing Wiki](https://github.com/nhsconnect/gpconnect-provider-testing/wiki) for further details.

{% include note.html content="Generic FHIR test harness such as [Crucible](https://www.projectcrucible.org/), [Sprinklr](https://github.com/furore-fhir/sprinkler) and [TouchStone](http://www.aegis.net/touchstone.html) may also be of interest to implementers." %}

### Non Functional ###

| Category       | Layer               | Details          |
|----------------|---------------------|------------------|
| Security       | Penetration Testing | OSWASP Top 10    |
| Performance    | API Performance     | Response Times   |
| Volumetrics    | API TPS             | LOAD, RAMP, SOAK |

## Consumer Testing (SIT) ##

### Consumer Testing Layers ###

An additional UI testing layer is required for consumer systems.

| Category            | Layer         | Details                |
|---------------------|---------------|------------------------|
| Consumer Capability | UI Behaviours | UI Use Case Automation |

### Non Functional ###

| Category       | Layer               | Details          |
|----------------|---------------------|------------------|
| Security       | Penetration Testing | OSWASP Top 10    | 

{% include note.html content="Formal V&P testing is not required for consumer applications." %}
