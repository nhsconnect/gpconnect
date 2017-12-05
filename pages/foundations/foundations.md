---
title: Foundations
keywords: foundations
tags: [foundations]
sidebar: foundations_sidebar
permalink: foundations.html
summary: "All about the common foundation capabilities."
---

{% include todo.html content="This capability pack is published as a **work in progress** version and as such is subject to change. It has been published to show the direction of travel and to serve as a discussion document for parties involved with the implementation and consumption of GP Connect FHIR based APIs." %}

## Purpose ##

The foundations capability cover the basic API requirements and prerequisites to utilise the GP Connect APIs.

{% include important.html content="In order to successfully make use of the GP Connect APIs, initially a level of pre-existing accredited Spine connectivity will be required along with some FHIR foundation API capabilities." %}

{% include roadmap.html content="Over time the necessity to have access to pre-existing spine services (i.e. PDS and SDS integration) is likely to be replaced by GP Connect/FHIR based equivalents." %}

## Prerequisites ##

### PDS ###

You'll need to be able to provide a verified NHS Number to use an API. This can be achieved using a spine accredited system, a DBS batch-traced record (CSV), or using a Spine Mini Services Provider (HL7v3).

### SDS / ODS ###

In order to resolve a given GP Practice organisation to their URI you'll need to be able to do a spine SDS query (LDAP) using the practice's ODS Code to perform an [SDS End Point Lookup](integration_spine_directory_service.html).

### FHIR ###

In order to be a compliant FHIR server, provider systems need to expose a valid FHIR [CapabilityStatement](https://www.hl7.org/fhir/STU3/capabilitystatement.html) profile.

Please also refer to [Development Guidance - FHIR API Guidance - Common API Guidance](development_fhir_api_guidance.html) for full details on the common FHIR API patterns used throughout all the GP Connect APIs.

## Scenarios ##

- Search for a patient by `NHS Number`.
- Search for an organisation by `ODS Code`.
- Search for a practitioner by `SDS UserID`.

### Use Cases ###

- [Get the FHIR capability statement](foundations_use_case_get_the_fhir_capability_statement.html)
- [Find a patient](foundations_use_case_find_a_patient.html)
- [Find a practitioner](foundations_use_case_find_a_practitioner.html)
- [Find an organisation](foundations_use_case_find_an_organisation.html)

## SPINE Interactions

The Foundation capability message set includes the following set of spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Read Metadata](foundations_use_case_get_the_fhir_capability_statement.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata` |
| [Read Patient](foundations_use_case_read_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient` |
| [Patient Search](foundations_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient` |
| [Read Practitioner](foundations_use_case_read_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:practitioner` |
| [Practitioner Search](foundations_use_case_find_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:practitioner` |
| [Read Organisation](foundations_use_case_read_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:organization` |
| [Organisation Search](foundations_use_case_find_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization` |
| [Read Location](foundations_use_case_read_a_location.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:location` | 


The Register Patient API Use Case, which is included in the Foundations capabilty has a seperate "Register Patient" message set:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Register Patient](foundations_use_case_register_a_patient.html)          | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient`


## Implementation And Testing ##

Below is the suggested order in which the foundation capabilities should be implemented. The specified order has been recomended around the functionality of the GP Connect Automated Test Suite and any internal dependancies between the test scenarios for the different foundation endpoints.

It is advisable to develop against the Automated Test Suite as this will assist with creating a GP Connect compliant product. By implementing the endpoints in the order below, this means that the automated test suite set of tests for that endpoint can be run during development without the developer seeing errors due to pre-test api calls or post test validation api calls relevant to the test being run and failing as they have not been developed yet.

### 1. Foundation Endpoints ###

| Order | API Endpoint | Test Suite Endpoint Dependencies | Reason For Dependency |
| ------------- | ------------- | ------------- | ------------- |
| #1 | Find an organization | - | The find an organization capability is not dependent on any other capablitiy within the automated test suite. |
| #2 | Read an Organization | Find an organization | `Find an organization` is a dependancy for `Read an organization` as it is used to lookup the local identifier from the organization code which is setup in the test suite organization mapping csv file. |
| #3 | Find a practitioner | Read an Organization | The `Read an organization` endpoint is required to validate the “managingOrganization” reference returned within the practitioner resource. |
| #4 | Read a practitioner | Find a practitioner / Read an organization | `Find a practitioner` is required to lookup the logical identifier, from the practitioner user id setup in the test suite practitioner mapping csv file, to use for the read. The `Read an organization` endpoint is required to validate the “managingOrganization” reference returned within the practitioner resource.|
| #5 | Find a patient | Read and organization / Read a practitioner | The `Read an organization` endpoint is required to validate the “managingOrganization” reference returned within the practitioner resource. The `Read a practitioner` endpoint is required to validate the “careProvider” reference if returned within the patient resource. |
| #6 | Read a patient | Find a patient / Read an organization / Read a practitioner | `Find a patient` is required to lookup logical identifier from the patient from the nhs number set up in the test suite nhsNoMap csv file. The `Read an organization` endpoint is required to validate the “managingOrganization” reference returned within the patient resource. The `Read a practitioner` endpoint is required to validate the “careProvider” reference if returned within the patient resource. |
| #7 | Read a location | Read an organization | The `Read an organization` endpoint is required to validate the “managingOrganization” reference returned within the location resource. |
| #8 | Register a patient | Find a patient / Read a patient / Read an organization  |The register patient endpoint tests require a number of the foundation search and read endpoints to be implemented and therefore it is advised that this is done as the last foundation capability. The foundation endpoints are used to create rich register patient requests as well as validating the registered patient resource is valid and retrievable on the providers system. |
