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

You need to be able to provide a verified NHS number to use an API. You can do this using a Spine accredited system, a Demographics Batch Service (DBS) batch-traced record (CSV), or using a Spine Mini Services Provider (HL7v3).

### SDS / ODS ###

To resolve a given GP Practice organisation to its URI you need to be able to do a Spine SDS query (LDAP) using the practice's ODS code to perform an [SDS End Point Lookup](integration_spine_directory_service.html).

### FHIR ###

In order to be a compliant FHIR server, provider systems need to expose a valid FHIR [CapabilityStatement](https://www.hl7.org/fhir/STU3/capabilitystatement.html) profile.

Refer to [Development Guidance - FHIR API Guidance - Common API Guidance](development_fhir_api_guidance.html) for full details on the common FHIR API patterns used throughout all the GP Connect APIs.

## API definition ##

The following individual API calls make up the Foundations capability and support the other capability packs:

- [Get the FHIR capability statement](foundations_use_case_get_the_fhir_capability_statement.html)
- [Find a patient](foundations_use_case_find_a_patient.html)
- [Read a patient](foundations_use_case_read_a_patient.html)
- [Find a practitioner](foundations_use_case_find_a_practitioner.html)
- [Read a practitioner](foundations_use_case_read_a_practitioner.html)
- [Find an organisation](foundations_use_case_find_an_organisation.html)
- [Read an organisation](foundations_use_case_read_an_organisation.html)
- [Find a healthcare service](foundations_use_case_find_a_healthcareservice.html)
- [Read a healthcare service](foundations_use_case_read_a_healthcareservice.html)
- [Read a location](foundations_use_case_read_a_location.html)
- [Register a patient](foundations_use_case_register_a_patient.html)

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
| [Read Healthcare Service](foundations_use_case_read_a_healthcareservice.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:healthcareservice-1` |
| [Healthcare Service Search](foundations_use_case_find_a_healthcareservice.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:healthcareservice-1` |
| [Read Location](foundations_use_case_read_a_location.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:location-1` | 
| [Register Patient](foundations_use_case_register_a_patient.html)          | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient-1`
