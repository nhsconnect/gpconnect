---
title: FHIR&reg; resources
keywords: development
sidebar: appointments_sidebar
permalink: datalibraryappointment.html
summary: "The FHIR resources used by Appointment Management"
---

## FHIR resources when searching for free slots ##

This diagram shows the relationships between FHIR resources used when searching for free slots to book.

![Diagram - Slot resource relationship structure](images/appointments/appointment-fhir-resources-slot.png)

<br />

The FHIR resources above are used in the following API interactions:

### Search for free slots ###

([*view API definition*](appointments_use_case_search_for_free_slots.html))

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html), populated with:
  - [GPConnect-Slot-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Slot-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html))
  - [GPConnect-Schedule-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Schedule-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/schedule.html))
  - [CareConnect-GPC-Location-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1) (based on [FHIR Location](https://www.hl7.org/fhir/STU3/location.html))
  - [CareConnect-GPC-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](https://www.hl7.org/fhir/STU3/appointment.html))
  - [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/appointment.html))

---

## FHIR resources when booking and managing booked appointments ##

This diagram shows the relationships between FHIR resources used when booking an appointment or managing a booked appointment.

![Diagram - Appointment resource relationship structure](images/appointments/appointment-fhir-resources-appointment.png)

<br/>

The Appointment resource and Organization resource (used to hold the booking organisation) are used in the request and/or response payloads of the API interactions below.  References to the other resources (such as Slot, Location, Patient etc) are populated in the relevant fields of the Appointment resource.

### Retrieve a patient's appointments ##

*([view API definition](appointments_use_case_retrieve_a_patients_appointments.html))*

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html), populated with:
	- [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)), with a contained resource of:
		- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

### Read an appointment ###

([*view API definition*](appointments_use_case_read_an_appointment.html))

##### Request #####

- *(No FHIR resource is sent within the request payload)*

##### Response #####

- [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)), with a contained resource of:
	- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))


### Book an appointment ###

([*view API definition*](appointments_use_case_book_an_appointment.html))

##### Request #####

- [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)), with a contained resource of:
	- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

##### Response #####

- [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)), with a contained resource of:
	- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))



### Amend an appointment ###

([*view API definition*](appointments_use_case_amend_an_appointment.html))

##### Request #####

- [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)), with a contained resource of:
	- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

##### Response #####

- [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)), with a contained resource of:
	- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))


### Cancel an appointment ###

([*view API definition*](appointments_use_case_cancel_an_appointment.html))

##### Request #####

- [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)), with a contained resource of:
	- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

##### Response #####

- [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)), with a contained resource of:
	- [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html))

---

## FHIR resources returned in error responses ##

If an error occurs during processing of the request in any of the above API interactions then the provider system will return an HTTP error code along with an OperationOutcome resource in the response payload. Details of the specific error responses are available on the [Error handling guidance](/development_fhir_error_handling_guidance.html) page within the specification.

##### Response #####

- [FHIR OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html)
