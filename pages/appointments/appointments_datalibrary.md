---
title: FHIR&reg; resources
keywords: development
sidebar: appointments_sidebar
toc: false
permalink: datalibraryappointment.html
summary: "The FHIR&reg; profiles and interactions required for the Appointment Management capability pack"
---

The following profiled FHIR&reg; resources are used in the current version of the Appointment Management capability - see 'API use cases' in the menu on the left. Full details of profiled FHIR resources and worked examples are available on the [FHIR Reference Server](https://fhir.nhs.uk/).

## Links between GP Connect FHIR resources ##

The FHIR resources are linked to each other by reference as highlighted in the diagram below:

![Diagram - Resource relationship structure](images/appointments/ResourceRelationshipsStructure.png)

---

## FHIR resources per GP Connect operation ##

## [Search for free slots](appointments_use_case_search_for_free_slots.html) ##

### Request ###

**Note:** No FHIR resource is sent within the request.

### Response ###

* [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html)
  * [GPConnect-Slot-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Slot-1) (based on [FHIR Slot](https://www.hl7.org/fhir/STU3/slot.html))
  * [GPConnect-Schedule-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Schedule-1) (based on [FHIR Schedule](https://www.hl7.org/fhir/STU3/schedule.html))
  * [CareConnect-GPC-Practitioner-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Practitioner-1?version=current) (based on [FHIR Practitioner](https://www.hl7.org/fhir/STU3/practitioner.html))
  * [CareConnect-GPC-Location-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Location-1?version=current) (based on [FHIR Location](https://www.hl7.org/fhir/STU3/location.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

---

## [Book an appointment](appointments_use_case_book_an_appointment.html) ##

### Request ###

* [GPConnect-Appointment-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Appointment-1?version=current) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

### Response ###

* [GPConnect-Appointment-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Appointment-1?version=current) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

---

## [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html) ##

### Request ###

**Note:** No FHIR resource is sent within the request.

### Response ###

* [GPConnect-Appointment-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Appointment-1?version=current) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

---

## [Read an appointment](appointments_use_case_read_an_appointment.html) ##

### Request ###

**Note:** No FHIR resource is sent within the request.

### Response ###

* [GPConnect-Appointment-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Appointment-1?version=current) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

---

## [Amend an appointment](appointments_use_case_amend_an_appointment.html) ##

### Request ###

* [GPConnect-Appointment-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Appointment-1?version=current) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

### Response ###

* [GPConnect-Appointment-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Appointment-1?version=current) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

---

## [Cancel an appointment](appointments_use_case_cancel_an_appointment.html) ##

### Request ###

* [GPConnect-Appointment-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Appointment-1?version=current) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

### Response ###

* [GPConnect-Appointment-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Appointment-1?version=current) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  * [CareConnect-GPC-Organization-1](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Organization-1?version=current) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

---

## Errors ##

If there is a problem with the request or an error occurs during processing of the request then the provider should return an HTTP error along with an "OperationOutcome" resource within the response payload. Details of the required error responses are available on the [Error handling guidance](/development_fhir_error_handling_guidance.html) page within the specification.

### Response ###

* [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html))
