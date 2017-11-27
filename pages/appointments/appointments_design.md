---
title: Appointments Design
keywords: appointments design
tags: [design,appointments]
sidebar: appointments_sidebar
permalink: appointments_design.html
summary: "Overview of the design decisions made in relation to the Appointment Management capability."
---

## Appointment API Scope ##

The scope of appointment management is to deliver:

- <span class="label label-success">SELECTED</span> Functionality required to manage appointments in the context of a patient.
- Functionality to view or manage an entire diary/appointment book.
- Functionality to create, amend, update diaries and/or schedules.

## New/unknown patients booking ##

The ability to create appointments for Patients not known to the GP practice/diary owner:

- If a patient is not known to the local system the appointment booking will be rejected by booking system. It will not be possible to register the patient.
- <span class="label label-success">SELECTED</span> If a patient is not known to the local system the appointment booking will be rejected by booking system. It will be possible to register the patient via a separate patient registration end point.
- If a patient is not known to the local system the appointment booking will be accepted and a patient record will be created with basic details about the patient (identifier).

{% include note.html content="Details of how to [Register a Patient](foundations_use_case_register_a_patient.html) can be found in the Foundations capability pack. " %}

## Access to Available Slots ##

When requesting the schedule of a particular diary, the level of detail returned should:

- Include all booked appointments and available slots.
- Only slots that are available (all types).
- <span class="label label-success">SELECTED</span> Only slots that are available and have been marked/flagged as externally bookable via GP Connect.

{% include roadmap.html content="Richer GP Appointment Slot access control functionality within Provider systems is being progressed recognising requirements such as access to slots by organisation type." %}

## Search parameters ##

The following search parameters will be initially included:

- All available common (across all four systems) slot defining criteria such as Gender, Slot Type, Slot Length, complex date/time ranges.
- <span class="label label-success">SELECTED</span> Date Range,  Urgent Care (UC) Disposition Code & Service ID, and Requesting Organisation Type are accommodated to support potential available appointment slot filtering (consumers can then apply further filtering, sorting at client side).  The last 3 are required to support the use of GP Connect APIs by UC Services.  

{% include note.html content="The Search Filter specification is flexible to allow for further search parameters to be defined. Value sets will be defined for these to be used by subsequent Provider system slot access control functionality." %}


## Maximum time span of diaries returned ##

When searching for diaries, the results will be:

- Unlimited based on any time span provided as part of the search.
- <span class="label label-success">SELECTED</span> Always be limited to a pre-defined maximum time period.

{% include note.html content="A 2 week window was agreed with system suppliers as a reasonable trade off between performance and usefulness initially, with the team seeking feedback from wider industry." %}

## Do we need to use the 'AppointmentResponse' resource? ##

As per the suggested FHIR workflow in the [FHIR Appointment](https://www.hl7.org/fhir/STU3/appointment.html) should the booking of an appointment utilise the 'AppointmentResponse' FHIR resource, or are HTTP response codes sufficient for GP Connect use cases?

- AppointmentResponse resource will be provided in response to a booking request.
- <span class="label label-success">SELECTED</span> HTTP codes will be used to convey success/failure of a booking request.

## Cancelling and Amending booked appointments ##

What provision will be made for making changes to existing appointments?

- Only cancellation will be allowed (must cancel and re-book).
- <span class="label label-success">SELECTED</span> Cancellation and Amendments to the Appointment Reason, Description and Comment are accommodated.
- Cancel and comprehensive amendments will be provisioned for (allowing appointments to move between slots/rescheduled).

## Can appointments be re-scheduled? ##

The API will not make provision for re-scheduling of appointments in a single interaction as a result of the limitation on which data elements of an appointment can be amended.

Therefore, a consumer wishing to re-schedule an appointment can do this through two API calls - firstly to cancel the existing appointment, then secondly to create a new appointment at the new date/time.

## Responsibilities in a federated booking context

Where there is a requirement for an implementation to provide an appointment management capability in a federated context, the GP Connect consumer implementation has the responsibility for defining the set of organisations which make up the federation. This consumer configuration will enable the consumer to make API calls to the relevent organisation set of endpoints in order to gain a federated view of appointments.

Neither Spine Security Proxy, nor the GP Connect Provider will expose such federation configuration or expose any aggregated view of appointments for a federation.

Please refer to the [glossary](overview_glossary.html) for a definition of a federation in this context.
