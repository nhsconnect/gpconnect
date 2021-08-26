---
title: FHIR&reg; resources
keywords: development
sidebar: foundations_sidebar
permalink: datalibraryfoundation.html
summary: "The FHIR profiles and interactions required for the Foundations capability pack"
---

## FHIR resources ##

The following FHIR resource profiles are used in the Foundations capability:

- [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](http://hl7.org/fhir/STU3/patient.html))
- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](http://hl7.org/fhir/STU3/organization.html))
- [CareConnect-GPC-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](http://hl7.org/fhir/STU3/practitioner.html))
- [CareConnect-GPC-HealthcareService-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-HealthcareService-1) (based on [FHIR HealthcareService](http://hl7.org/fhir/STU3/healthcareservice.html))
- [CareConnect-GPC-Location-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1) (based on [FHIR Location](http://hl7.org/fhir/STU3/location.html))
- [FHIR CapabilityStatement](http://hl7.org/fhir/STU3/capabilitystatement.html)
- [FHIR Bundle](http://hl7.org/fhir/STU3/bundle.html)
- [FHIR Parameters](http://hl7.org/fhir/STU3/parameters.html)

## Common identifier systems ##

The following business identifier systems are used in the above resources (in the `identifier` field), and when searching for a resource in the Foundations capability:

| Identifier | Resource | System |
| ---------- | -------- | ------ |
| NHS number | Patient | `https://fhir.nhs.uk/Id/nhs-number` |
| ODS organisation code | Organization | `https://fhir.nhs.uk/Id/ods-organization-code` |
| ODS site code | Location | `https://fhir.nhs.uk/Id/ods-site-code` |
| SDS user ID | Practitioner | `https://fhir.nhs.uk/Id/sds-user-id` |
| SDS role profile ID | Practitioner | `https://fhir.nhs.uk/Id/sds-role-profile-id` |
| UEC DOS service ID | HealthcareService | `https://fhir.nhs.uk/Id/uec-dos-service-id` |

{% include note.html content="ODS site code is not currently supported by provider systems." %}

## FHIR resources by interaction ##

### Find a patient ##

*([view API definition](foundations_use_case_find_a_patient.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html), populated with:
  - [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](http://hl7.org/fhir/STU3/patient.html))

### Read a patient ##

*([view API definition](foundations_use_case_read_a_patient.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](http://hl7.org/fhir/STU3/patient.html))

---

### Find a practitioner ##

*([view API definition](foundations_use_case_find_a_practitioner.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html), populated with:
  - [CareConnect-GPC-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](http://hl7.org/fhir/STU3/practitioner.html))

### Read a practitioner ##

*([view API definition](foundations_use_case_read_a_practitioner.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [CareConnect-GPC-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](http://hl7.org/fhir/STU3/practitioner.html))

---

### Find an organisation ##

*([view API definition](foundations_use_case_find_an_organisation.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html), populated with:
  - [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](http://hl7.org/fhir/STU3/organization.html))

### Read an organisation ##

*([view API definition](foundations_use_case_read_an_organization.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](http://hl7.org/fhir/STU3/organization.html))

---

### Find a healthcare service ##

*([view API definition](foundations_use_case_find_a_healthcareservice.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html), populated with:
  - [CareConnect-GPC-HealthcareService-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-HealthcareService-1) (based on [FHIR HealthcareService](http://hl7.org/fhir/STU3/healthcareservice.html))

### Read a healthcare service ##

*([view API definition](foundations_use_case_read_a_healthcareservice.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [CareConnect-GPC-HealthcareService-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-HealthcareService-1) (based on [FHIR HealthcareService](http://hl7.org/fhir/STU3/healthcareservice.html))

---

### Read a location ##

*([view API definition](foundations_use_case_read_a_location.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [CareConnect-GPC-Location-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1) (based on [FHIR Location](http://hl7.org/fhir/STU3/location.html))

---

### Register a patient ##

*([view API definition](foundations_use_case_register_a_patient.html))*

##### Request #####

- [FHIR Parameters](https://www.hl7.org/fhir/STU3/parameters.html) according to the input parameters of [GPConnect-RegisterPatient-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-RegisterPatient-Operation-1), populated with:
  - [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/STU3/patient.html))

##### Response #####

- [GPConnect-Searchset-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1) (based on [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html)), populated with:
  - [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/STU3/patient.html))

---

## FHIR resources returned in error responses ##

If an error occurs during processing of the request in any of the above API interactions then the provider system will return an HTTP error code along with an OperationOutcome resource in the response payload. Details of the specific error responses are available on the [Error handling guidance](/development_fhir_error_handling_guidance.html) page within the specification.

##### Response #####

- [FHIR OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html)