---
title: Appointment Management
keywords: appointments
tags: [appointments]
sidebar: appointments_sidebar
permalink: appointments.html
summary: "All about the appointment management capability."
---

[<i class="fa fa-arrow-left" aria-hidden="true"/> Back to GP Connect - Getting Started.](index.html)

{% include todo.html content="This capability pack is published as a **work in progress** version and as such is subject to change. It has been published to show the direction of travel and to serve as a discussion document for parties involved with the implementation and consumption of GP Connect FHIR based APIs." %}

## Purpose ##

Demonstrates the ability to provide service users (and patients) with the ability to book and manage appointments in a timely fashion and to provide better, quicker access to primary care.

## Scenarios ##

- A service user at a GP practice can book an appointment on behalf of a patient.
- A service user at an extended access Hub can book an appointment at the GP practice on behalf of a patient.
- A patient can book, cancel or view their existing appointments (extended access hubs or GP practice) through the organisations on-line service.
- Enable a service user at 111 to book, cancel or view appointments for a patient at the patients’ own GP and extended access Hub sites.
- Enable a range of other care settings to book, view or cancel an appointment on behalf of the patient. Any of; A+E, Physio, Acute, Social, Community etc.

## Use Cases ##

- [Retrieve a patients appointments](appointments_use_case_retrieve_a_patients_appointments.html)
- [Search for free slots](appointments_use_case_search_for_free_slots.html)
- [Read an appointment](appointments_use_case_read_an_appointment.html)
- [Book an appointment](appointments_use_case_book_an_appointment.html)
- [Amend an appointment](appointments_use_case_amend_an_appointment.html)
- [Cancel an appointment](appointments_use_case_cancel_an_appointment.html)

{% include tip.html content="Creation of `Schedule` and `Slot` resources is out of scope for the GP Connect FoT as these resources are expected to be managed from within an organisation's principal IT system." %}

### Domain Message Specification ###

Please refer to the Domain Message Specification (DMS) bundle for details of the FHIR profiles utilised:

{% include dms.html link="http://data.developer.nhs.uk/fhir/candidaterelease-250816-appts/" content="Appointment Management." %}