---
title: Foundation Resources
keywords: development
sidebar: foundations_sidebar
toc: false
permalink: datalibraryfoundation.html
summary: "The fhir profiles and interactions required for the Foundation capability"
---

The following profiled FHIR resources are used in the current version of the Foundation capabilities, see "API Use Cases" in the menu on the left. Full details of profiled FHIR resources and worked examples are available on the [FHIR Reference Server](https://fhir-test.nhs.uk/).

{% include important.html content="The profiled FHIR Resources are currently being updated to align with the CareConnect FHIR profiles used by other NHSDigital projects. Currently this section of the specification references the updated profiles for Practitioner, Organization and Location, other Resource profiles will be updated shortly." %}

---
## ***[Find a patient](foundations_use_case_find_a_patient.html) / [Read a patient](foundations_use_case_read_a_patient.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [CareConnect-GPC-Patient-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/DSTU2/patient.html))

---
## ***[Find a practitioner](foundations_use_case_find_a_practitioner.html) / [Read a practitioner](foundations_use_case_read_a_practitioner.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [CareConnect-GPC-Practitioner-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html))
  
---
## ***[Find an organisation](foundations_use_case_find_an_organisation.html) / [Read an organisation](foundations_use_case_read_an_organisation.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [CareConnect-GPC-Organization-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/DSTU2/organization.html))
  
---
## ***[Read a location](foundations_use_case_read_a_location.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [CareConnect-GPC-Location-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Location-1) (based on [FHIR Location](https://www.hl7.org/fhir/DSTU2/location.html))

---
## ***[Register a patient](foundations_use_case_register_a_patient.html)*** ##

### Request ###
* [gpconnect-registerpatient-operation-1](https://fhir-test.nhs.uk/OperationDefinition/gpconnect-registerpatient-operation-1) (based on [FHIR Parameters](https://www.hl7.org/fhir/DSTU2/parameters.html))
  * [CareConnect-GPC-Patient-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/DSTU2/patient.html))

### Response ###
* [gpconnect-searchset-bundle-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-searchset-bundle-1) (based on [FHIR Bundle](https://www.hl7.org/fhir/DSTU2/bundle.html))
  * [CareConnect-GPC-Patient-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/DSTU2/patient.html))

---
## ***Errors*** ##

If there is a problem with the request or an error occurs during processing of the request then the provider should return a http error along with an "OperationOutcome" Resource within the response payload. Details of the required error responses are available on the [Error Handling Guidance](/development_fhir_error_handling_guidance.html) page within the specification.

### Response ###
* [gpconnect-operationoutcome-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-operationoutcome-1) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html))
