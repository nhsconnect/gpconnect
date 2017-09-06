---
title: Appointments Release Notes
keywords: appointments, release notes
tags: []
sidebar: appointments_sidebar
permalink: appointments_release_notes.html
summary: "Release notes for the various versions of the Appointment Management capability."
---

#### 1.0.0-beta.2
  - Removed practitioner participant as a mandatory element within the appointment resource (Page - Book an appointment).
  - Added location participant as a mandatory element within the appointment resource (Page - Book an appointment).
  - Updated datalibrary to be capability specific, moving it to reside under the "Development" menu within the capability. This is to allow the Profiled FHIR Resources to be referenced per capability and updated independantly. For Appointment Management we have updated specification to reference FHIR profiles stored on FHIR reference server rather than those on the old DMS capability pack.
  - Updated book appointment with guidance on use of the comment and description elements within the resource.
  - Updated search prefixes listed on "Retrieve a patient's appointments" page, within Appointment Management API Use Case section, to align with common API guidance, removed "ne" search prefix and added the "eq" search prefix. Also updated the link to the Common API Guidance page to directly link to the search section.
  - Corrected examples on API Use Cases pages to include FHIR Resource Profile in the returned FHIR resources.
  - Added clarification on the expected response when the [Search for free slots](appointments_use_case_search_for_free_slots.html) API use case does not return any free slots for the requested time period.
  - Updated API Use Case pages to make clear the expectations around the FHIR Resource Metadata Profile element, along with updates to examples to show new profile definitions.
  - Added clarification around GP Connect "FHIR Resource Profile" and "Metadata Profile" requirements on the request/consumer side of the [Book an Appointment](appointments_use_case_book_an_appointment.htm), [Amend  an Appointment](appointments_use_case_amend_an_appointment.html) and [Cancel an appointment](appointments_use_case_cancel_an_appointment.html) API use cases. 
  - Added clarification on the expected response content for the [Retrieve a Patient's Appointments](appointments_use_case_retrieve_a_patients_appointments.html) API use case.
  - Additional detail on error conditions for [Read an appointment](appointments_use_case_read_an_appointment.html)
  - [Cancel an appointment](appointments_use_case_cancel_an_appointment.html) API use case associated with cancel an appointment interaction
  - [Book an appointment](development_fhir_api_guidance.html#create-resource) emphasised requirement for provider to return Location header describing details of the newly created resource.
  - Updated identifier system within examples to match identifiers within new fhir profiles (Pages - appointments_use_case_search_for_free_slots.html)
  
#### 1.0.0-beta.1
  - Initial release of the Appointment Management capability pack on Github in early August 2016.
  
#### 1.0.0-alpha.1
  - Initial release for feedback/comments as part of the late May 2016 release.
  