---
title: Consumer Testing
keywords: consumer testing
tags: [testing,integration,deployment]
sidebar: overview_sidebar
permalink: testing_api_consumer_testing.html
summary: "Details of what activities form the basis of testing for consumer applications."
---

Consumer systems SHALL undertake a three stage testing process:

- [Technical Accreditation](testing_api_provider_testing.html#technicalaccreditation) for Spine connectivity prerequisites.
- [Technical Conformance](testing_api_provider_testing.html#technicalconformance) for functional testing of Consumer API usage.
- [Solution Assurance](testing_api_provider_testing.html#solutionassurance) for functional, non-functional, ready-for-operation & clinical safety.

## Technical Accreditation ##

Consumer systems SHALL be (or have previously been) tested and accreditated to establish baseline Spine connectivity prerequisites:

 - N3 Connectivity / ASID / PKI Certificate
 - [PDS Integration](integration_personal_demographic_service.html)
 - [SDS Integration](integration_spine_directory_service.html)

## Technical Conformance ##

Consumer systems SHALL be tested for technical conformance of the following before they can be listed on the product catalogue:

 - [SSP Integration](integration_spine_security_proxy.html)
 - [Foundations](foundations.html)

Consumer systems SHALL be tested for conformance to one or more of the following capability packs:

 - [Access Record HTML](accessrecord.html)
 - [Access Record Structured](accessrecord_rest.html)
 - [Appointment Management](appointments.html)
 - [Task Management](tasks.html)

## Solution Assurance ##

Solution assurance ensures that the correct level of safety, governance, and security has been accepted, understood and signed off by the organisation consuming the APIs.