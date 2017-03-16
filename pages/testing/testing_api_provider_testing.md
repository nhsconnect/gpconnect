---
title: Provider Testing
keywords: provider testing
tags: [testing,integration,deployment]
sidebar: overview_sidebar
permalink: testing_api_provider_testing.html
summary: "Details of what activities form the basis of testing for API provider systems."
---

Provider systems SHALL undertake a three stage testing process:

- [Technical Accreditation](testing_api_provider_testing.html#technicalaccreditation) for Spine connectivity prerequisites.
- [Technical Conformance](testing_api_provider_testing.html#technicalconformance) for functional testing of Provider APIs.
- [Solution Assurance](testing_api_provider_testing.html#solutionassurance) for functional, non-functional, ready-for-operation & clinical safety.

## Technical Accreditation ##

Provider systems SHALL be (or have previously been) tested and accreditated to establish baseline Spine connectivity prerequisites:

 - N3 Connectivity / ASID / PKI Certificate
 - [PDS Integration](integration_personal_demographic_service.html)
 - [SDS Integration](integration_spine_directory_service.html)

## Technical Conformance ##

Provider systems SHALL be tested for technical conformance of the following before they can be listed on the product catalogue:

 - [SSP Integration](integration_spine_security_proxy.html)
 - [Foundations](foundations.html)

Provider systems SHALL be tested for conformance to one or more of the following capability packs:

 - [Access Record HTML](accessrecord.html)
 - [Access Record REST](accessrecord_rest.html)
 - [Appointment Management](appointments.html)
 - [Task Management](tasks.html)

{% include download.html content="Download the [GP Connect Provider Test Suite](https://github.com/nhsconnect/gpconnect-provider-testing) to help validate the technical conformance of your provider API implementation." %}

## Solution Assurance ##

Solution assurance ensures that the correct level of safety, governance, and security has been accepted, understood and signed off by the organisation providing the APIs.

{% include important.html content="Suppliers are responsible for there own testing and the clinical safety of the delivered system. Supplier authored tests must be traceable back to the published specification. NHS Digital's automated test suite is non-exhaustive and does not cover all test cases/scenarios required to pass solution assurance. NHS Digital expects to see evidence of more supplier authored tests in addition to the NHS Digital authored tests." %}

### Witness Testing ###

Provider systems SHALL undergo witness testing to validate conformance to requirements which can't easily be automated.