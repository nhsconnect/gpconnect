---
title: Provider testing
keywords: provider testing
tags: [testing,integration,deployment]
sidebar: overview_sidebar
permalink: testing_api_provider_testing.html
summary: "Details of what activities form the basis of testing for API provider systems"
---

Provider systems SHALL undertake a three-stage testing process:

- [Technical accreditation](testing_api_provider_testing.html#technicalaccreditation) for Spine connectivity prerequisites
- [Technical conformance](testing_api_provider_testing.html#technicalconformance) for functional testing of provider APIs
- [Solution assurance](testing_api_provider_testing.html#solutionassurance) for functional, non-functional, ready-for-operation and clinical safety

## Technical accreditation ##

Provider systems SHALL be (or have previously been) tested and accredited to establish baseline Spine connectivity prerequisites:

 - N3 connectivity / ASID / PKI Certificate
 - [Personal Demographic Service (PDS) integration](integration_personal_demographic_service.html)
 - [Spine Directory Service (SDS) integration](integration_spine_directory_service.html)

## Technical conformance ##

Provider systems SHALL be tested for technical conformance of the following before they can be listed on the product catalogue:

 - [Spine Secure Proxy (SSP) integration](integration_spine_secure_proxy.html)
 - [Foundations](foundations.html)

Provider systems SHALL be tested for conformance to one or more of the following capability packs:

 - [Access Record HTML](accessrecord.html)
 - [Access Record Structured](accessrecord_structured.html)
 - [Appointment Management](appointments.html)

{% include download.html content="Download the [GP Connect Provider Test Suite](https://github.com/nhsconnect/gpconnect-provider-testing) to help validate the technical conformance of your provider API implementation." %}

## Solution assurance ##

Solution assurance ensures that the correct level of safety, governance, and security has been accepted, understood and signed off by the organisation providing the APIs.

{% include important.html content="Suppliers are responsible for their own testing and the clinical safety of the delivered system. Supplier-authored tests must be traceable back to the published specification. NHS Digital's automated test suite is non-exhaustive and does not cover all test cases/scenarios required to pass solution assurance. NHS Digital expects to see evidence of more supplier authored tests in addition to the NHS Digital authored tests." %}

### Witness testing ###

Provider systems SHALL undergo witness testing to validate conformance to requirements which can't easily be automated.
