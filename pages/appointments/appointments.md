---
title: Appointment Management
keywords: appointments
tags: [appointments]
sidebar: appointments_sidebar
permalink: appointments.html
summary: "All about the appointment management capability."
---

## Purpose ##

To meet strategic objectives to improve access to GP care, the Appointment Management(AM) APIs enable consumer system administrative and clinical end-users to more effectively book and manage GP Practice-designated externally-bookable appointments held in any of the four GP Principal Practice systems.  The deployment of the APIs within Patient Apps, to support Patient direct access, is envisaged for a later Phase.

## Example Scenarios ##

- Administrative staff at a GP practice can book an appointment on behalf of a patient
- Administrative staff at a GP Extended Access Hub can book an appointment on behalf of a patient at any of its federated GP practices 
- An Urgent Care 111 Call Centre handler or Triage Clinician can book, cancel or view appointments on behalf of a patient at the patient's registered or federated GP Practices or Extended Access Hubs
- A patient will be able to book, cancel or view their GP appointments via a GPConnect-enabled App
- Administrative staff and Clinicians at a range of other care settings, eg A&E, Physio, Social and Community services,  will be able to book, view or cancel a GP appointment on behalf of the patient

## FoT Care Setting Deployments  ##

The following FoT deployments are being progressed:

### Care Setting 1: Within GP Federations ###

Enabling a GP practice or Appointment Hub, to book, amend, cancel, or view a patient’s in-hours or extended hours appointments at the patient’s registered GP Practice or another GP practice within the same federation.  

### Care Setting 2: From UC Call Centres to GP Practices – In-Hours, Extended Hours Appointments ###
The requirement to support the use of the GP Connect capability for Unscheduled Care by Urgent Care (UC) Services - ie UC Call Centres booking and managing appointments into GP practices –  has been accommodated where possible in the API design. 
The Call Centre will retrieve and select In-Hours or Extended Hours appointments for booking/managing at either 

   - the Patient’s registered GP Practice

   - GP Practices federated with the Patient’s registered GP Practice

   - a GP Practice within the vicinity of the Patient’s geographic location – eg when the Patient is on holiday

{% include note.html content="Whilst the GP Connect programme primarily assumes that the appointment-hosting (provider) systems are the GP Principal Systems, the API technical design has accommodated the minimum viable features required to support Booking and Managing of Appointments at UC Providers such as Minor Injuries Units and GP Out of Hours services.  This means that UC consumers will not need to use different APIs depending on the type of organisation they are targeting.  **This deployment care setting is currently out of scope for GP Connect FoT deployments.**" %}  

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
