---
title: Foundation Resources
keywords: development
sidebar: foundations_sidebar
toc: false
permalink: datalibraryfoundation.html
summary: "The fhir prifles and interactions required for the Foundation capability"
---

The following profiled FHIR resources are used in the current version of the Foundation capabilities, see "API Use Cases" in the menu on the left. Full details of profiled FHIR resources and worked examples are available on the [FHIR Reference Server](https://fhir-test.nhs.uk/).

---
## Find a patient / Read a patient ##
### Response ###
* [gpconnect-patient-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/DSTU2/patient.html))

---
## Find a practitioner / Read a practitioner ##
### Response ###
* [CareConnect-GPC-Practitioner-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html))
  
---
## Find an organisation / Read an organisation ##
### Response ###
* [CareConnect-GPC-Organization-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/DSTU2/organization.html))
  
---
## Find a location / Read a location ##
### Response ###
* [CareConnect-GPC-Location-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Location-1) (based on [FHIR Location](https://www.hl7.org/fhir/DSTU2/location.html))

---
## Register a patient ##

### Request ###
* [gpconnect-registerpatient-operation-1](https://fhir-test.nhs.uk/OperationDefinition/gpconnect-registerpatient-operation-1) (based on [FHIR Parameters](https://www.hl7.org/fhir/DSTU2/parameters.html))
  * [gpconnect-register-patient-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-register-patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/DSTU2/patient.html))

### Response ###
* [gpconnect-registerpatient-bundle-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-registerpatient-bundle-1) (based on [FHIR Bundle](https://www.hl7.org/fhir/DSTU2/bundle.html))
  * [gpconnect-register-patient-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-register-patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/DSTU2/patient.html))
  * [CareConnect-GPC-Practitioner-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html))
  * [CareConnect-GPC-Organization-1](https://fhir-test.nhs.uk/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/DSTU2/organization.html))

---
## Errors ##
### Response ###
* [gpconnect-operationoutcome-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-operationoutcome-1) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html))
