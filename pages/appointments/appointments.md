---
title: Appointment Management
keywords: appointments
tags: [appointments]
sidebar: appointments_sidebar
permalink: appointments.html
summary: "Overview of the Appointment Management capability pack"
---

## Purpose ##

To meet strategic objectives to improve access to GP care, the Appointment Management (AM) APIs enable consumer system administrative and clinical end users to book and manage GP practice appointments held in any of the four GP principal practice systems. The implementation of the APIs within patient apps (to support patient direct access) is out of scope for initial deployment. Some API specification items may be uplifted in the future to reflect the requirements identified by related Appointment Management initiatives within the GP IT and Interoperability domains.

## Example scenarios ##

- administrative staff at a GP practice can book, view, amend or cancel appointments on behalf of a patient
- administrative staff at a GP extended access hub can book, view, amend or cancel appointments on behalf of a patient at any of its federated GP practices
- an urgent care (UC) 111 call centre handler or triage clinician can book, view, amend or cancel appointments on behalf of a patient at the patient's registered or federated GP practices or extended access hubs
- administrative staff and clinicians at a range of other care settings (for example, A&amp;E, physio, social and community services) will be able to book, view or cancel a GP appointment on behalf of the patient

## GP practice appointment slot availability ##

GP practices need to control access by external organisations to their appointment book. Provider systems will enable practice users to designate their schedules/slots as bookable by GP Connect, and by Organisation Type and/or specific Organisations ensuring that only slots matching the booking Organisation/Type are returned in response to a request.

The Appointment slots available via GP Connect will also be categorised by the end-user according to standardised values representing the role of the practitioner delivering the appointment, and the channel by which the appointment is to be delivered - for example, 'telephone', 'in-person'. This provides more information to the user booking the appointment on behalf of the patient, thereby reducing the risk of inappropriate appointment booking. The requirements are described in more detail in the [Slot availability management](appointments_slotavailabilitymanagement.html) page.


## First of Type (FoT) care setting deployments ##

The following FoT deployments are being progressed:

### Care Setting 1: Within GP federations ###

Enabling a GP practice or appointment hub to book, view, amend or cancel a patient’s in-hours or extended hours appointments at the patient’s registered GP practice or another GP practice within the same [Federation](overview_glossary.html#federation).  

### Care Setting 2: From UC call centres to GP practices – in-hours, extended hours appointments ###
The requirement to support the use of the GP Connect capability for unscheduled care by UC services (UC call centres booking and managing appointments into GP practices) has been accommodated where possible in the API design. 
The call centre will retrieve and select in-hours or extended hours appointments for booking/managing at either: 

   - the patient’s registered GP practice

   - GP practices federated with the patient’s registered GP practice

   - a GP practice within the vicinity of the patient’s geographic location; for example, when the patient is on holiday

{% include note.html content="While the GP Connect programme primarily assumes that the appointment-hosting (provider) systems are the GP principal systems, the API technical design has accommodated the minimum viable features required to support booking and managing of appointments at UC providers such as Minor Injuries Units and GP out-of-hours services. This means that UC consumers will not need to use different APIs depending on the type of organisation they are targeting. **This deployment care setting is currently out of scope for the GP Connect programme FoT deployments, which only incorporates assurance of the API fulfilment by the GP principal provider systems. The assurance and deployment of the APIs by UC provider systems will be progressed by NHS Digital Integrated Urgent Care programmes.**" %}  

## API use cases ##

The following individual API calls are used by consumers to implement the Appointment Management capability:

- [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html)
- [Search for free slots](appointments_use_case_search_for_free_slots.html)
- [Read an appointment](appointments_use_case_read_an_appointment.html)
- [Book an appointment](appointments_use_case_book_an_appointment.html)
- [Amend an appointment](appointments_use_case_amend_an_appointment.html)
- [Cancel an appointment](appointments_use_case_cancel_an_appointment.html)

## Examples of consumer Appointment Management sessions

The use of the individual API calls listed above by consumers to fulfil business processes is illustrated with focus on the booking of an appointment. See [Appointment Management consumer sessions illustrated](appointments_consumer_sessions.html).

## Consumer code examples

Consumer side code examples are available for each of GP Connect interactions within the following GitHub repositories. The repositories contain a different branch for each release of the specification, the code within these branches matches the requirements of the specification within that release.

[.NET](https://github.com/nhsconnect/gpconnect-dotnet-examples)

[JAVA](https://github.com/nhsconnect/gpconnect-java-examples)


## Profiled FHIR resources ##

See the [Appointment Management FHIR&reg; resources](datalibraryappointment.html) page for details of the FHIR profiles used for the Appointment Management capability pack.

## Spine interactions ##

The Appointment Management capability message set includes the following set of Spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Get organisation schedule](appointments_use_case_search_for_free_slots.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot-1` |
| [Read appointment](appointments_use_case_read_an_appointment.html)          | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment-1` |
| [Create appointment](appointments_use_case_book_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment-1` |
| [Amend appointment](appointments_use_case_amend_an_appointment.html)         | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment-1` |
| [Cancel appointment](appointments_use_case_cancel_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:cancel:appointment-1` |
| [Get patient appointments](appointments_use_case_retrieve_a_patients_appointments.html)  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments-1` |


## Implementation and testing ##

Below is the suggested order in which the appointment capabilities should be implemented. The specified order has been recommended around the functionality of the GP Connect Automated Test Suite and any internal dependencies between the test scenarios for the different Appointment Management endpoints. The Appointment Management capability test scenarios are dependent on the foundation capabilities and therefore the foundation endpoints should be developed and tested before implementing the Appointment Management capabilities.

It’s recommended that you develop against the Automated Test Suite as this will help with creating a GP Connect compliant product. By implementing the endpoints in the order below, the Automated Test Suite set of tests for that endpoint can be run during development without you seeing errors due to pre-test API calls or post-test validation API calls relevant to the test being run and failing as they have not been developed yet.

| Order | API endpoint | Test suite endpoint dependencies | Reason for dependency |
| ------------- | ------------- | ------------- | ------------- |
| #1 | Search for free slots | Read an organization / Read a practitioner / Read a location | The `Search for free slots` test scenarios require some of the foundation endpoints to validate references within returned resources contained within the response bundle. |
| #2 | Book an appointment | Register a patient / Find a patient / Search for free slots / Read an organization / Read a location / Read a practitioner / Read a patient | The `Book an appointment` endpoint finds a slot which it then uses to book an appointment for a known patient. To find the logical IDs of the elements required to book an appointment it requires the `Find a patient` and `Search for free slots` endpoints to have been implemented and working. Some of the tests also require the `Register a patient` endpoint to have been implemented as it tests booking an appointment against a GP Connect temporary patient. |
| #3 | Retrieve a patient’s appointments | Search for free slots / Find a patient / Book an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test suite builds the appointments for a patient before testing the `Find a patient’s appointments` capability to make sure appointments exist to find. This requires the endpoints to find free slots, find a patient’s logical identifier, book an appointment and, in some tests, create a temporary patient against which to book the appointment. |
| #4 | Amend an appointment | Search for free slots / Find a patient / Book an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for the `Amend an appointment` capability require most of the foundation endpoints and most of the other appointment endpoints to be implemented to find or create the appointments which the tests are going to update as part of the `Amend an appointment` tests. |
| #5 | Cancel an appointment | Search for free slots / Find a patient / Book an appointment / Amend an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for the `Cancel an appointment` capability require most of the  foundation endpoints and the other Appointment Management endpoints to be implemented in order to find, create and amend the appointments required for the test scenarios and validation of the returned response. |
| #6 | Read an appointment | Search for free slots / Find a patient / Book an appointment / Amend an appointment / Cancel an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for `Read an appointment` require different foundation endpoints and all the other appointment endpoints to be implemented as the tests need to create appointments with different statuses if they are not available. The test must find the local identifiers for both the appointment it is trying to read and any steps it may need to do to create or validate the appointment. |

