---
title: FHIR&reg; resources
keywords: development
sidebar: appointments_sidebar
toc: false
permalink: datalibraryappointment.html
summary: "The FHIR&reg; profiles required for the Appointment Management capability"
---

The following profiled FHIR&reg; resources are used in the the Appointment Management capability, and are grouped by API use case.

The [FHIR Reference Server](https://fhir.nhs.uk/) contains all NHS Digital profiled FHIR&reg; resources, including worked examples.

---
## [Search for free slots](appointments_use_case_search_for_free_slots.html) ##

### Request ###

*(No FHIR&reg; resource is sent within the request)*

### Response ###
* [Bundle](https://www.hl7.org/fhir/STU3/bundle.html), containing:
  * [GPConnect-Slot-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Slot-1) (based on [Slot](https://www.hl7.org/fhir/STU3/slot.html))
  * [GPConnect-Schedule-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Schedule-1) (based on [Schedule](https://www.hl7.org/fhir/STU3/schedule.html))
  * [CareConnect-GPC-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [Practitioner](https://www.hl7.org/fhir/STU3/practitioner.html))
  * [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [Organization](https://www.hl7.org/fhir/STU3/organization.html))
  * [CareConnect-GPC-Location-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1) (based on [Location](https://www.hl7.org/fhir/STU3/location.html))

---
## [Book an appointment](appointments_use_case_book_an_appointment.html) ##

### Request ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [Appointment](https://www.hl7.org/fhir/STU3/appointment.html))

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [Appointment](https://www.hl7.org/fhir/STU3/appointment.html))

---
## [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html) ##

### Request ###
*(No FHIR&reg; resource is sent within the request)*

### Response ###
* [Bundle](https://www.hl7.org/fhir/STU3/bundle.html), containing:
  * [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [Appointment](https://www.hl7.org/fhir/STU3/appointment.html))

---
## [Read an appointment](appointments_use_case_read_an_appointment.html) ##

### Request ###
*(No FHIR&reg; resource is sent within the request)*

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [Appointment](https://www.hl7.org/fhir/STU3/appointment.html))

---
## [Amend an appointment](appointments_use_case_amend_an_appointment.html) ##
### Request ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [Appointment](https://www.hl7.org/fhir/STU3/appointment.html))

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [Appointment](https://www.hl7.org/fhir/STU3/appointment.html))

---
## [Cancel an appointment](appointments_use_case_cancel_an_appointment.html) ##
### Request ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [Appointment](https://www.hl7.org/fhir/STU3/appointment.html))

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [Appointment](https://www.hl7.org/fhir/STU3/appointment.html))

---
## Errors ##

If there is a problem with the request or an error occurs during processing of the request then the provider **SHALL** return an HTTP error along with an OperationOutcome resource instead of the response above. Details of the required error responses are available on the [Error handling guidance](/development_fhir_error_handling_guidance.html) page within the specification.

### Response ###
* [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) (based on [OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html))
