---
title: Appointment Management
keywords: appointments
tags: [appointments]
sidebar: appointments_sidebar
permalink: appointments.html
summary: "All about the appointment management capability."
---

{% include todo.html content="This capability pack is published as a **work in progress** version and as such is subject to change. It has been published to show the direction of travel and to serve as a discussion document for parties involved with the implementation and consumption of GP Connect FHIR based APIs." %}

## Purpose ##

The Appointment Management Capability APIs will enable consumer system service users initially (subsequently patients ) to more effectively book and manage appointments held in any of the four GP Principal Practice systems, improving access to GP care.

## Example Scenarios ##

- Administrative staff at a GP practice can book an appointment on behalf of a patient.
- Administrative staff at a GP Extended Access Hub can book an appointment on behalf of a patient at any of its federated GP practices 
- An Urgent Care 111 Call Centre handler or Triage Clinician can book, cancel or view appointments on behalf of a patient at the patient's registered or federated GP Practices or Extended Access Hubs
- A patient will be able to book, cancel or view their GP appointments via a GPConnect-enabled App
- Administrative staff and Clinicians at a range of other care settings, eg A&E, Physio, Social and Community services,  will be able to book, view or cancel a GP appointment on behalf of the patient

## API Use Cases ##

The following individual API calls are used by consumers to implement the appointment management capability.

- [Retrieve a patients appointments](appointments_use_case_retrieve_a_patients_appointments.html)
- [Search for free slots](appointments_use_case_search_for_free_slots.html)
- [Read an appointment](appointments_use_case_read_an_appointment.html)
- [Book an appointment](appointments_use_case_book_an_appointment.html)
- [Amend an appointment](appointments_use_case_amend_an_appointment.html)
- [Cancel an appointment](appointments_use_case_cancel_an_appointment.html)

{% include tip.html content="Creation of `Schedule` and `Slot` resources is out of scope for the GP Connect FoT as these resources are expected to be managed from within an organisation's principal IT system." %}

## Examples of Consumer Appointment Management Sessions

The use of the individual API calls listed above by consumers to fulfill business processes is illustrated, with particular focus on the booking of an appointment.  See [Appointment Consumer Sessions Illustrated](appointments_consumer_sessions.html)

## Profiled FHIR Resources ##

Please refer to the [Appointment Management FHIR Resources](datalibraryappointment.html) page for details of the FHIR profiles utilised for the Appointment Management capability.

## SPINE Interactions ##

The Appointment Management capability message set includes the following set of Spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Get Organisation Schedule](appointments_use_case_search_for_free_slots.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot` |
| [Read Appointment](appointments_use_case_read_an_appointment.html)          | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment` |
| [Create Appointment](appointments_use_case_book_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment` |
| [Amend Appointment](appointments_use_case_amend_an_appointment.html)         | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` |
| [Cancel Appointment](appointments_use_case_cancel_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` |
| [Get Patient Appointments](appointments_use_case_retrieve_a_patients_appointments.html)  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments` |
