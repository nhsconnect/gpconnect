---
title: Appointments Release Notes
keywords: appointments, release notes
tags: []
sidebar: appointments_sidebar
permalink: appointments_release_notes.html
summary: "Release notes for the various versions of the Appointment Management capability."
---

- 1.0.0-beta.2
  - Removed practitioner participant as a mandatory element within the appointment resource (Page - Book an appointment).
  - Added location participant as a mandatory element within the appointment resource (Page - Book an appointment).
  - Updated datalibrary to be capability specific, moving it to reside under the "Development" menu within the capability. This is to allow the Profiled FHIR Resources to be referenced per capability and updated independantly. For Appointment Management we have updated specification to reference FHIR profiles stored on FHIR reference server rather than those on the old DMS capability pack.
  - Updated book appointment with guidance on use of the comment and description elements within the resource.
  - Updated search prefixes listed on "Retrieve a patient's appointments" page, within Appointment Management Api Use Case section, to align with common api guidance, removed "ne" search prefix and added the "eq" search prefix. Also updated the link to the Common Api Guidance page to directly link to the search section.
  - Corrected examples on Api Use Cases pages to include Fhir Resource Profile in the returned Fhir resources.
  - Added clarification on the expected response when the "Search for free slots" capability does not return any free slots for the requested time period (Page - appointments_use_case_search_for_free_slots.html)
  - Updated Api Use Case pages to make clear the expectations around the Fhir Resource Metadata Profile element, along with updates to examples to show new profile definitions.
  - Added clarification around GP Connect "Fhir Resource Profile" and "Metadata Profile" requirements on the request/consumer side of the "Book Appointment", "Amend Appointment" and "Cancel appointment" capabilities. (Pages - appointments_use_case_amend_an_appointment.html, appointments_use_case_cancel_an_appointment.html, appointments_use_case_book_an_appointment.html)
  
- 1.0.0-beta.1
  - Initial release of the Appointment Management capability pack on Github in early August 2016.
  
- 1.0.0-alpha.1
  - Initial release for feedback/comments as part of the late May 2016 release.
  