---
title: Foundations
keywords: foundations
tags: [foundations]
sidebar: foundations_sidebar
permalink: foundations.html
summary: "All about the common foundation capabilities"
---

## Purpose ##

The Foundations capability covers the basic API requirements and prerequisites needed to use the GP Connect APIs.

{% include important.html content="To use the GP Connect APIs, you need a level of pre-existing accredited Spine connectivity along with some FHIR foundation API capabilities." %}

{% include roadmap.html content="The necessity to have access to pre-existing Spine services (for example, Personal Demographics Service (PDS) and Spine Directory Service (SDS) integration) is likely to be replaced by GP Connect/FHIR based equivalents." %}

## Prerequisites ##

### PDS ###

You need to be able to provide a verified NHS Number to use an API. You can do this using a Spine accredited system, a Demographics Batch Service (DBS) batch-traced record (CSV), or using a Spine Mini Services Provider (HL7v3).

### SDS / ODS ###

To resolve a given GP Practice organisation to its URI you need to be able to do a Spine SDS query (LDAP) using the practice's Organisation Data Service (ODS) code to perform an [SDS End Point Lookup](integration_spine_directory_service.html).

### FHIR ###

In order to be a compliant FHIR server, provider systems need to expose a valid FHIR [CapabilityStatement](https://www.hl7.org/fhir/STU3/capabilitystatement.html) profile.

Refer to [Development Guidance - FHIR API Guidance - Common API Guidance](development_fhir_api_guidance.html) for full details on the common FHIR API patterns used throughout all the GP Connect APIs.

## Scenarios ##

- Search for a patient by `NHS Number`
- Search for an organisation by `ODS Code`
- Search for a practitioner by `SDS UserID`

## API use cases ##

The following individual API calls make up the Foundations capability and support the other capability packs:

- [Get the FHIR capability statement](foundations_use_case_get_the_fhir_capability_statement.html)
- [Find a patient](foundations_use_case_find_a_patient.html)
- [Read a patient](foundations_use_case_read_a_patient.html)
- [Find a practitioner](foundations_use_case_find_a_practitioner.html)
- [Read a practitioner](foundations_use_case_read_a_practitioner.html)
- [Find an organisation](foundations_use_case_find_an_organisation.html)
- [Read an organisation](foundations_use_case_read_an_organisation.html)
- [Read a location](foundations_use_case_read_a_location.html)
- [Register a patient](foundations_use_case_register_a_patient.html)


## Consumer application code examples

Consumer side code examples are available for each of GP Connect interactions within the following GitHub repositories. The repositories contain a different branch for each release of the specification, the code within these branches matches the requirements of the specification within that release.

[.NET](https://github.com/nhsconnect/gpconnect-dotnet-examples)

[JAVA](https://github.com/nhsconnect/gpconnect-java-examples)


## Spine interactions

The Foundations capability message set includes the following set of Spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Read Metadata](foundations_use_case_get_the_fhir_capability_statement.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata-1` |
| [Read Patient](foundations_use_case_read_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient-1` |
| [Patient Search](foundations_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient-1` |
| [Read Practitioner](foundations_use_case_read_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:practitioner-1` |
| [Practitioner Search](foundations_use_case_find_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:practitioner-1` |
| [Read Organisation](foundations_use_case_read_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:organization-1` |
| [Organisation Search](foundations_use_case_find_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization-1` |
| [Read Location](foundations_use_case_read_a_location.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:location-1` | 


The Register Patient API use case, which is included in the Foundations capability, has a separate "Register Patient" message set:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Register Patient](foundations_use_case_register_a_patient.html)          | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient-1`


## Implementation and testing ##

Below is the suggested order in which the Foundations capability should be implemented. The specified order has been recommended around the functionality of the GP Connect Automated Test Suite and any internal dependencies between the test scenarios for the different Foundations endpoints.

It is advisable to develop against the Automated Test Suite as this will assist with creating a GP Connect compliant product. By implementing the endpoints in the order below, this means that the automated test suite set of tests for that endpoint can be run during development without the developer seeing errors due to pre-test API calls or post-test validation API calls relevant to the test being run and failing as they have not been developed yet.

### 1. Foundations endpoints ###

| Order | API Endpoint | Test Suite Endpoint Dependencies | Reason For Dependency |
| ------------- | ------------- | ------------- | ------------- |
| #1 | Find an organisation | - | The find an organisation capability is not dependent on any other capability within the automated test suite. |
| #2 | Read an Organisation | Find an organisation | `Find an organisation` is a dependency for `Read an organisation` as it is used to lookup the local identifier from the organisation code which is setup in the test suite organisation mapping csv file. |
| #3 | Find a practitioner | Read an Organisation | The `Read an organisation` endpoint is required to validate the “managingOrganization” reference returned within the practitioner resource. |
| #4 | Read a practitioner | Find a practitioner / Read an organisation | `Find a practitioner` is required to lookup the logical identifier, from the practitioner user id setup in the test suite practitioner mapping csv file, to use for the read. The `Read an organisation` endpoint is required to validate the “managingOrganization” reference returned within the practitioner resource.|
| #5 | Find a patient | Read and organisation / Read a practitioner | The `Read an organisation` endpoint is required to validate the “managingOrganization” reference returned within the practitioner resource. The `Read a practitioner` endpoint is required to validate the “careProvider” reference if returned within the patient resource. |
| #6 | Read a patient | Find a patient / Read an organisation / Read a practitioner | `Find a patient` is required to lookup logical identifier from the patient from the NHS number set up in the test suite nhsNoMap csv file. The `Read an organisation` endpoint is required to validate the “managingOrganization” reference returned within the patient resource. The `Read a practitioner` endpoint is required to validate the “careProvider” reference if returned within the patient resource. |
| #7 | Read a location | Read an organisation | The `Read an organisation` endpoint is required to validate the “managingOrganization” reference returned within the location resource. |
| #8 | Register a patient | Find a patient / Read a patient / Read an organisation  |The register patient endpoint tests require a number of the Foundations search and read endpoints to be implemented and therefore it is advised that this is done as the last Foundations capability. The Foundations endpoints are used to create rich register patient requests as well as validating the registered patient resource is valid and retrievable on the providers system. |
