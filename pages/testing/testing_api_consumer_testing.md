---
title: Consumer testing
keywords: consumer testing
tags: [testing,integration,deployment]
sidebar: overview_sidebar
permalink: testing_api_consumer_testing.html
summary: "Details of what activities form the basis of testing for consumer applications"
---

Consumer systems **MUST** undertake a three stage testing process:

- [Technical accreditation](testing_api_provider_testing.html#technical-accreditation) for Spine connectivity prerequisites
- [Technical conformance](testing_api_provider_testing.html#technical-conformance) for functional testing of consumer API usage
- [Solution assurance](testing_api_provider_testing.html#solution-assurance) for functional, non-functional, ready-for-operation and clinical safety

## Technical accreditation ##

Consumer systems **MUST** be (or have previously been) tested and accredited to establish baseline Spine connectivity prerequisites:

 - N3 connectivity / ASID / PKI Certificate
 - [Personal Demographic Service (PDS) integration](integration_personal_demographic_service.html)
 - [Spine Directory Service (SDS) integration](integration_spine_directory_service.html)

## Technical conformance ##

Consumer systems **MUST** be tested for technical conformance of the following before they can be listed on the product catalogue:

 - [Spine Secure Proxy (SSP) integration](integration_spine_secure_proxy.html)
 - [Foundations](foundations.html)

Consumer systems **MUST** be tested for conformance to one or more of the following capability packs:

 - [Access Record HTML](accessrecord.html)
 - [Access Record Structured](accessrecord_rest.html)
 - [Appointment Management](appointments.html)

## Solution assurance ##

Solution assurance ensures that the correct level of safety, governance, and security has been accepted, understood and signed off by the organisation consuming the APIs.
