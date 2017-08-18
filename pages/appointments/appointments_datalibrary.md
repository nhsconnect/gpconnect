---
title: Appointment Management Resources
keywords: development
sidebar: appointments_sidebar
toc: false
permalink: datalibraryappointment.html
summary: "The fhir prifles and interactions required for the Appointment Management capability"
---

The following profiled FHIR resources are used in the current version of the Appointment Management capability, see "API Use Cases" in the menu on the left. Full details of profiled FHIR resources and worked examples are available on the [FHIR Reference Server](https://fhir-test.nhs.uk/).

---
## Search for free slots ##
### Request ###
* [gpconnect-schedule-operation-1](https://fhir-test.nhs.uk/OperationDefinition/gpconnect-schedule-operation-1) (based on [FHIR Parameters](https://www.hl7.org/fhir/DSTU2/parameters.html))

### Response ###
* [gpconnect-getschedule-bundle-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-getschedule-bundle-1) (based on [FHIR Bundle](https://www.hl7.org/fhir/DSTU2/bundle.html))
  * [gpconnect-slot-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-slot-1) (based on [FHIR Slot](https://www.hl7.org/fhir/DSTU2/slot.html))
  * [gpconnect-schedule-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-schedule-1) (based on [FHIR Schedule](https://www.hl7.org/fhir/DSTU2/schedule.html))
  * [gpconnect-practitioner-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-practitioner-1) (based on [FHIR Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html))
  * [gpconnect-organization-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/DSTU2/organization.html))
  * [gpconnect-location-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-location-1) (based on [FHIR Location](https://www.hl7.org/fhir/DSTU2/location.html))

  
---
## Book an appointment ##
### Request ###
* [gpconnect-appointment-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html))

### Response ###
* [gpconnect-appointment-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html))


---
## Retrieve a patients appointments ##
### Response ###
* [gpconnect-appointment-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html))


---
## Read an appointment ##
### Response ###
* [gpconnect-appointment-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html))


---
## Amend an appointment ##
### Request ###
* [gpconnect-appointment-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html))

### Response ###
* [gpconnect-appointment-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html))


---
## Cancel an appointment ##
### Request ###
* [gpconnect-appointment-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html))

### Response ###
* [gpconnect-appointment-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html))

---
## Errors ##
### Response ###
* [gpconnect-operationoutcome-1](https://fhir-test.nhs.uk/StructureDefinition/gpconnect-operationoutcome-1) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html))