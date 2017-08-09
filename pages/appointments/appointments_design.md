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

## Content of diaries ##

When requesting the schedule of a particular diary, the level of detail returned should:

- Include all booked appointments and available slots.
- Only slots that are available (all types).
- <span class="label label-success">SELECTED</span> Only slots that are available and have been marked/flagged as externally bookable.

## Search parameters ##

The following search parameters will be initially included:

- All available common (across all four systems) slot defining criteria such as Gender, Slot Type, Slot Length, complex date/time ranges.
- <span class="label label-success">SELECTED</span> Only date ranges will be available to set as part of a diary search (consumers can then apply further filtering, sorting at client side).

{% include roadmap.html content="Greater flexibility in available available search parameters is desirable to support finer grained searching, e.g. by gender, by type." %}

## Maximum time span of diaries returned ##

When searching for diaries, the results will be:

- Unlimited based on any time span provided as part of the search.
- <span class="label label-success">SELECTED</span> Always be limited to a pre-defined maximum time period.

{% include note.html content="A 2 week window was agreed with system suppliers as a reasonable trade off between performance and usefulness initially, with the team seeking feedback from wider industry." %}

## Do we need to use the 'AppointmentResponse' resource? ##

As per the suggested FHIR workflow in the [FHIR DSTU2 Appointment](https://www.hl7.org/fhir/DSTU/appointment.html) Should the booking of an appointment utilise the 'AppointmentResponse' FHIR resource, or are HTTP response codes sufficient for GP Connect use cases?

- AppointmentResponse resource will be provided in response to a booking request.
- <span class="label label-success">SELECTED</span> HTTP codes will be used to convey success/failure of a booking request.

## Cancelling and Amending booked appointments ##

What provision will be made for making changes to existing appointments?

- Only cancellation will be allowed (must cancel and re-book).
- <span class="label label-success">SELECTED</span> Cancel and basic amendments will be provisioned for (i.e. only allowed to the comment/description fields).
- Cancel and comprehensive amendments will be provisioned for (allowing appointments to move between slots/rescheduled).

{% comment %}

## Schedule usage ##

- A schedule resource should only be one encounter set of slots. For example the schedule could have two practitioner references such as a practitioner and a nurse but any slots in that schedule will be attended by both the practitioner and the nurse.
- To represent two practitioner working independently there should be two schedules, one for each practitioner, referenced and the practitioner extension within the schedules.
- If a practitioner is going to be in one location but then move to another location they should have one schedule with one actor (location) for the first location. This schedule should stop before another schedule with the changed location starts for the same practitioner.

{% endcomment %}
