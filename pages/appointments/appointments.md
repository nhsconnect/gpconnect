---
title: Appointment Management
keywords: appointments
tags: [appointments]
sidebar: appointments_sidebar
permalink: appointments.html
summary: "All about the Appointment Management capability pack."
---

## Purpose ##

To meet strategic objectives to improve access to GP care, the Appointment Management (AM) APIs enable consumer system administrative and clinical end-users to book and manage GP practice appointments held in any of the four GP principal practice systems.  The deployment of the APIs within patient apps (to support patient direct access) is envisaged for a later phase.

## Example scenarios ##

- Administrative staff at a GP practice can book an appointment on behalf of a patient
- Administrative staff at a GP extended access hub can book an appointment on behalf of a patient at any of its federated GP practices 
- An urgent care (UC) 111 call centre handler or triage clinician can book, cancel or view appointments on behalf of a patient at the patient's registered or federated GP practices or extended access hubs
- A patient will be able to book, cancel or view their GP appointments via a GP Connect-enabled app
- Administrative staff and clinicians at a range of other care settings (for example, A&amp;E, physio, social and community services)  will be able to book, view or cancel a GP appointment on behalf of the patient

## GP practice appointment slot control ##

GP practices need to control access to their appointment book by external organisations and it is therefore expected that provider systems will in the first instance enable practice users to designate their schedules/slots as bookable by GP Connect, ensuring that only these slots are returned in response to a request.

More granular access control will be required to match the appointment slot filtering support included in the specification and as value sets are defined, so that slots are made available for example dependent on requesting organisation type.

## First of Type (FoT) care setting deployments  ##

The following FoT deployments are being progressed:

### Care Setting 1: Within GP federations ###

Enabling a GP practice or appointment hub to book, amend, cancel, or view a patient’s in-hours or extended hours appointments at the patient’s registered GP practice or another GP practice within the same federation.  

### Care Setting 2: From UC call centres to GP practices – in-hours, extended hours appointments ###
The requirement to support the use of the GP Connect capability for unscheduled care by urgent care (UC) services (UC call centres booking and managing appointments into GP practices) has been accommodated where possible in the API design. 
The call centre will retrieve and select in-hours or extended hours appointments for booking/managing at either: 

   - the patient’s registered GP practice

   - GP practices federated with the patient’s registered GP practice

   - a GP practice within the vicinity of the patient’s geographic location; for example, when the patient is on holiday

{% include note.html content="While the GP Connect programme primarily assumes that the appointment-hosting (provider) systems are the GP principal systems, the API technical design has accommodated the minimum viable features required to support booking and managing of appointments at UC providers such as minor injuries units and GP out of hours services.  This means that UC consumers will not need to use different APIs depending on the type of organisation they are targeting.  **This deployment care setting is currently out of scope for GP Connect FoT deployments.**" %}  

## API use cases ##

The following individual API calls are used by consumers to implement the appointment management capability:

- [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html)
- [Search for free slots](appointments_use_case_search_for_free_slots.html)
- [Read an appointment](appointments_use_case_read_an_appointment.html)
- [Book an appointment](appointments_use_case_book_an_appointment.html)
- [Amend an appointment](appointments_use_case_amend_an_appointment.html)
- [Cancel an appointment](appointments_use_case_cancel_an_appointment.html)

{% include tip.html content="Creation of `schedule` and `slot` resources is out of scope for the GP Connect FoT as these resources are expected to be managed from within an organisation's principal IT system." %}

## Examples of consumer appointment management sessions

The use of the individual API calls listed above by consumers to fulfil business processes is illustrated, with focus on the booking of an appointment.  See [Appointment Consumer Sessions Illustrated](appointments_consumer_sessions.html).

## Profiled FHIR resources ##

See the [Appointment Management FHIR Resources](datalibraryappointment.html) page for details of the FHIR profiles used for the Appointment Management capability pack.

## Spine interactions ##

The Appointment Management capability message set includes the following set of Spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Get organisation schedule](appointments_use_case_search_for_free_slots.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot` |
| [Read appointment](appointments_use_case_read_an_appointment.html)          | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment` |
| [Create appointment](appointments_use_case_book_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment` |
| [Amend appointment](appointments_use_case_amend_an_appointment.html)         | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` |
| [Cancel appointment](appointments_use_case_cancel_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` |
| [Get patient appointments](appointments_use_case_retrieve_a_patients_appointments.html)  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments` |


## Implementation And Testing ##

Below is the suggested order in which the appointment capabilities should be implemented. The specified order has been recomended around the functionality of the GP Connect Automated Test Suite and any internal dependancies between the test scenarios for the different appointment management endpoints. The appointment management capability test scenarios are dependant on the foundation capabilities and therefore the foundation endpoints should be developed and tested before implementing the appointment management capabilities.

It is advisable to develop against the Automated Test Suite as this will assist with creating a GP Connect compliant product. By implementing the endpoints in the order below, this means that the automated test suite set of tests for that endpoint can be run during development without the developer seeing errors due to pre-test api calls or post test validation api calls relevant to the test being run and failing as they have not been developed yet.

| Order | API Endpoint | Test Suite Endpoint Dependencies | Reason For Dependency |
| ------------- | ------------- | ------------- | ------------- |
| #1 | Search for free slots | Read an organization / Read a practitioner / Read a location | The `Search for free slots` test scenarios requires a number of the foundation endpoints in order to validate references within returned resources contained within the response bundle. |
| #2 | Book an appointment | Register a patient / Find a paitent / Search for free slots / Read an organization / Read a location / Read a practitioner / Read a patient | The `Book an appointment` endpoint finds a slot which it then uses to book an appointment for a known patient. To find the logical id's of the elements required to book an appointment it requires the `Find a patient` and `Search for free slots` endpoints to have been implemented and working. Some of the tests also require the `Register a patient` endpoint to have been implemented as it tests booking an appointment against a GP Connect temp patient. |
| #3 | Retrieve a patient appointments | Search for free slots / Find a patient / Book an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test suite builds the appointments for a patient before testing the `Find a patients appointments` capability to make sure appointments exist to find. This requires the endpoints to find free slots, find a patients logical identifier, book an appointment and in some tests create a temporary patient against which to book the appointment. |
| #4 | Amend an appointment | Search for free slots / Find a patient / Book an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for the `Amend an appointment` capability require most of the  foundation endpoints and most of the other appointment endpoints to be implemented in order to find or create the appointments which the tests are going to update as part of the `Amend an appointment` tests. |
| #5 | Cancel an appointment | Search for free slots / Find a patient / Book an appointment / Amend an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for the `Cancel an appointment` capability require most of the  foundation endpoints and the other appointment management endpoints to be implemented in order to find, create and amend the appointments required for the test scenarios and validation of the returned response. |
| #6 | Read an appointment | Search for free slots / Find a patient / Book an appointment / Amend an appointment / Cancel an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for `Read an appointment` require a number of different foundation and all the other appointment endpoints to be implemented as the tests need to create appointments with different statuses if they are not available and the test has to find the local identifiers for both the appointment it is trying to read and any steps it may need to do to create or validate the appointment. |
