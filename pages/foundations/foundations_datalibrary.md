---
title: Foundation Resources
keywords: development
sidebar: foundations_sidebar
toc: false
permalink: datalibraryfoundation.html
summary: "The fhir profiles and interactions required for the Foundation capability"
---

The following profiled FHIR resources are used in the current version of the Foundation capabilities, see "API Use Cases" in the menu on the left. Full details of profiled FHIR resources and worked examples are available on the [FHIR Reference Server](https://fhir.nhs.uk/).

---
## ***[Find a patient](foundations_use_case_find_a_patient.html) / [Read a patient](foundations_use_case_read_a_patient.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](http://hl7.org/fhir/STU3/patient.html)) ![STU3](images/stu3.png)

---
## ***[Find a practitioner](foundations_use_case_find_a_practitioner.html) / [Read a practitioner](foundations_use_case_read_a_practitioner.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [CareConnect-GPC-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](http://hl7.org/fhir/STU3/practitioner.html)) ![STU3](images/stu3.png)
  
---
## ***[Find an organisation](foundations_use_case_find_an_organisation.html) / [Read an organisation](foundations_use_case_read_an_organisation.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html)) ![STU3](images/stu3.png)
  
---
## ***[Read a location](foundations_use_case_read_a_location.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [CareConnect-GPC-Location-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1) (based on [FHIR Location](https://www.hl7.org/fhir/STU3/location.html)) ![STU3](images/stu3.png)

---
## ***[Register a patient](foundations_use_case_register_a_patient.html)*** ##

### Request ###
* [gpconnect-registerpatient-operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/gpconnect-registerpatient-operation-1) (based on [FHIR Parameters](https://www.hl7.org/fhir/STU3/parameters.html)) ![STU3](images/stu3.png)
  * [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/STU3/patient.html)) ![STU3](images/stu3.png)

### Response ###
* [GPConnect-Searchset-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1) (based on [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html)) ![STU3](images/stu3.png)
  * [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/STU3/patient.html)) ![STU3](images/stu3.png)

---
## ***Errors*** ##

If there is a problem with the request or an error occurs during processing of the request then the provider should return a http error along with an "OperationOutcome" Resource within the response payload. Details of the required error responses are available on the [Error Handling Guidance](/development_fhir_error_handling_guidance.html) page within the specification.

### Response ###
* [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html)) ![STU3](images/stu3.png)
