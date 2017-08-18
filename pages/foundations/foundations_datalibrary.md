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
* [gpconnect-practitioner-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-practitioner-1) (based on [FHIR Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html))
  
---
## Find an organisation / Read an organisation ##
### Response ###
* [gpconnect-organization-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/DSTU2/organization.html))
  
---
## Find a location / Read a location ##
### Response ###
* [gpconnect-location-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-location-1) (based on [FHIR Location](https://www.hl7.org/fhir/DSTU2/location.html))

---
## Register a patient ##

### Request ###
* [gpconnect-registerpatient-operation-1](https://fhir-test.nhs.uk/OperationDefinition/gpconnect-registerpatient-operation-1) (based on [FHIR Parameters](https://www.hl7.org/fhir/DSTU2/parameters.html))
  * [gpconnect-register-patient-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-register-patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/DSTU2/patient.html))

### Response ###
* [gpconnect-registerpatient-bundle-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-registerpatient-bundle-1) (based on [FHIR Bundle](https://www.hl7.org/fhir/DSTU2/bundle.html))
  * [gpconnect-register-patient-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-register-patient-1) (based on [FHIR Patient](https://www.hl7.org/fhir/DSTU2/patient.html))
  * [gpconnect-practitioner-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-practitioner-1) (based on [FHIR Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html))
  * [gpconnect-organization-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/DSTU2/organization.html))

---
## Errors ##
### Response ###
* [gpconnect-operationoutcome-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-operationoutcome-1) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html))
