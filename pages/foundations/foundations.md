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

In order to be a compliant FHIR server, provider systems need to expose a valid FHIR [Conformance](https://www.hl7.org/fhir/DSTU2/conformance.html) profile.

Please also refer to [Development Guidance - FHIR API Guidance - Common API Guidance](development_fhir_api_guidance.html) for full details on the common FHIR API patterns used throughout all the GP Connect APIs.

## Scenarios ##

- Search for a patient by `NHS Number`.
- Search for an organisation by `ODS Code`.
- Search for a practitioner by `SDS UserID`.

### Use Cases ###

- [Get the FHIR conformance profile](foundations_use_case_get_the_fhir_conformance_profile.html)
- [Find a patient](foundations_use_case_find_a_patient.html)
- [Find a practitioner](foundations_use_case_find_a_practitioner.html)
- [Find an organisation](foundations_use_case_find_an_organisation.html)

## SPINE Interactions

The Foundation capability message set includes the following set of spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Read Metadata](foundations_use_case_get_the_fhir_conformance_profile.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata` |
| [Read Patient](foundations_use_case_read_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient` |
| [Patient Search](foundations_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient` |
| [Read Practitioner](foundations_use_case_read_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:practitioner` |
| [Practitioner Search](foundations_use_case_find_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:practitioner` |
| [Read Organization](foundations_use_case_read_an_organization.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:organization` |
| [Organisation Search](foundations_use_case_find_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization` |
| [Read Location](foundations_use_case_read_a_location.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:location` | 


The Register Patient API Use Case, which is included in the Foundations capabilty has a seperate "Register Patient" message set:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Register Patient](foundations_use_case_register_a_patient.html)          | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient`
