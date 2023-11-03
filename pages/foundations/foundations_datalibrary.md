---
title: FHIR&reg; resources
keywords: development
sidebar: foundations_sidebar
toc: false
permalink: datalibraryfoundation.html
summary: "The FHIR profiles and interactions required for the Foundations capability pack"
---

The following profiled FHIR resources are used in the current version of the Foundations capabilities (see "API Use Cases" in the menu on the left). Full details of profiled FHIR resources and worked examples are available on the [FHIR Reference Server](https://fhir.nhs.uk/).

---

## ***[Find a patient](foundations_use_case_find_a_patient.html) / [Read a patient](foundations_use_case_read_a_patient.html)*** ##

### Request ###

N/A - No FHIR resource is sent within the request.

### Response ###

* [CareConnect-GPC-Patient-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Patient-1?version=current) (based on [FHIR Patient](http://hl7.org/fhir/STU3/patient.html))

---

## ***[Find a practitioner](foundations_use_case_find_a_practitioner.html) / [Read a practitioner](foundations_use_case_read_a_practitioner.html)*** ##

### Request ###

N/A - No FHIR resource is sent within the request.

### Response ###

* [CareConnect-GPC-Practitioner-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Practitioner-1?version=current) (based on [FHIR Practitioner](http://hl7.org/fhir/STU3/practitioner.html))

---

## ***[Find an organisation](foundations_use_case_find_an_organisation.html) / [Read an organisation](foundations_use_case_read_an_organisation.html)*** ##

### Request ###

N/A - No FHIR resource is sent within the request.

### Response ###

* [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

---

## ***[Read a location](foundations_use_case_read_a_location.html)*** ##

### Request ###

N/A - No FHIR resource is sent within the request.

### Response ###

* [CareConnect-GPC-Location-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Location-1?version=current) (based on [FHIR Location](https://www.hl7.org/fhir/STU3/location.html))

---

## ***[Register a patient](foundations_use_case_register_a_patient.html)*** ##

### Request ###

* [GPConnect-RegisterPatient-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-RegisterPatient-Operation-1) (based on [FHIR Parameters](https://www.hl7.org/fhir/STU3/parameters.html))
  * [CareConnect-GPC-Patient-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Patient-1?version=current) (based on [FHIR Patient](https://www.hl7.org/fhir/STU3/patient.html))

### Response ###

* [GPConnect-Searchset-Bundle-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Searchset-Bundle-1?version=current) (based on [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html))
  * [CareConnect-GPC-Patient-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Patient-1?version=current) (based on [FHIR Patient](https://www.hl7.org/fhir/STU3/patient.html))

---

## ***Errors*** ##

If there is a problem with the request or an error occurs during processing of the request then the provider should return an HTTP error along with an "OperationOutcome" resource within the response payload. Details of the required error responses are available on the [Error handling guidance](development_fhir_error_handling_guidance.html) page within the specification.

### Response ###

* [GPConnect-OperationOutcome-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-OperationOutcome-1?version=current) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html))
