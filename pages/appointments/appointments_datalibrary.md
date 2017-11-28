---
title: Appointment Management Resources
keywords: development
sidebar: appointments_sidebar
toc: false
permalink: datalibraryappointment.html
summary: "The fhir prifles and interactions required for the Appointment Management capability"
---

The following profiled FHIR resources are used in the current version of the Appointment Management capability, see "API Use Cases" in the menu on the left. Full details of profiled FHIR resources and worked examples are available on the [FHIR Reference Server](https://fhir.nhs.uk/).

---
## ***[Search for free slots](appointments_use_case_search_for_free_slots.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [FHIR Bundle](https://www.hl7.org/fhir/STU3/bundle.html) ![STU3](images/stu3.png)
  * [GPConnect-Slot-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Slot-1) (based on [FHIR Slot](https://www.hl7.org/fhir/STU3/slot.html)) ![STU3](images/stu3.png)
  * [GPConnect-Schedule-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Schedule-1) (based on [FHIR Schedule](https://www.hl7.org/fhir/STU3/schedule.html)) ![STU3](images/stu3.png)
  * [CareConnect-GPC-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1) (based on [FHIR Practitioner](https://www.hl7.org/fhir/STU3/practitioner.html)) ![STU3](images/stu3.png)
  * [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) (based on [FHIR Organization](https://www.hl7.org/fhir/STU3/organization.html)) ![STU3](images/stu3.png)
  * [CareConnect-GPC-Location-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1) (based on [FHIR Location](https://www.hl7.org/fhir/STU3/location.html)) ![STU3](images/stu3.png)

  
---
## ***[Book an appointment](appointments_use_case_book_an_appointment.html)*** ##
### Request ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)) ![STU3](images/stu3.png)

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)) ![STU3](images/stu3.png)


---
## ***[Retrieve a patients appointments](appointments_use_case_retrieve_a_patients_appointments.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)) ![STU3](images/stu3.png)


---
## ***[Read an appointment](appointments_use_case_read_an_appointment.html)*** ##
### Request ###
N/A - No fhir resource is sent within the request

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)) ![STU3](images/stu3.png)


---
## ***[Amend an appointment](appointments_use_case_amend_an_appointment.html)*** ##
### Request ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)) ![STU3](images/stu3.png)

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)) ![STU3](images/stu3.png)


---
## ***[Cancel an appointment](appointments_use_case_cancel_an_appointment.html)*** ##
### Request ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)) ![STU3](images/stu3.png)

### Response ###
* [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) (based on [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html)) ![STU3](images/stu3.png)

---
## ***Errors*** ##

If there is a problem with the request or an error occurs during processing of the request then the provider should return a http error along with an "OperationOutcome" Resource within the response payload. Details of the required error responses are available on the [Error Handling Guidance](/development_fhir_error_handling_guidance.html) page within the specification.

### Response ###
* [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/STU3/operationoutcome.html)) ![STU3](images/stu3.png)