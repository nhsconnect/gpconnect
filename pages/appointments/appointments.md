---
title: Appointment Management
keywords: appointments
tags: [appointments]
sidebar: appointments_sidebar
permalink: appointments.html
summary: "Overview of the Appointment Management capability pack"
---

## Overview ##

## Purpose ##

To meet strategic objectives to improve access to GP care, the Appointment Management (AM) APIs enable consumer system administrative and clinical end users to book and manage GP practice appointments held in any of the four GP principal practice systems. The implementation of the APIs within patient apps (to support patient direct access) is out of scope for initial deployment. Some API specification items may be uplifted in the future to reflect the requirements identified by related Appointment Management initiatives within the GP IT and Interoperability domains.

## Problem Statement ##

## Scope ##

The GPConnect Appointments Management capability allows Organisations with data sharing agreement in place to do the following functions:
1. Search for free GPConnect Bookable Slots
2. Book Appointment(GPConnect Bookable)
3. Amend Appointment
4. Cancel Appointment
5. Retrieve Appointments

## Example scenarios ##

- administrative staff at a GP practice can book, view, amend or cancel appointments on behalf of a patient
- administrative staff at a GP extended access hub can book, view, amend or cancel appointments on behalf of a patient at any of its federated GP practices
- an urgent care (UC) 111 call centre handler or triage clinician can book, view, amend or cancel appointments on behalf of a patient at the patient's registered or federated GP practices or extended access hubs
- administrative staff and clinicians at a range of other care settings (for example, A&amp;E, physio, social and community services) will be able to book, view or cancel a GP appointment on behalf of the patient

## Versioning ##

To Do

## GP practice appointment slot availability ##

GP practices need to control access by external organisations to their appointment book. Provider systems will enable practice users to designate their schedules/slots as bookable by GP Connect, and by Organisation Type and/or specific Organisations ensuring that only slots matching the booking Organisation/Type are returned in response to a request.

The Appointment slots available via GP Connect will also be categorised by the end-user according to standardised values representing the role of the practitioner delivering the appointment, and the channel by which the appointment is to be delivered - for example, 'telephone', 'in-person'. This provides more information to the user booking the appointment on behalf of the patient, thereby reducing the risk of inappropriate appointment booking. The requirements are described in more detail in the [Slot availability management](appointments_slotavailabilitymanagement.html) page.


## First of Type (FoT) care setting deployments ##

The following FoT deployments are being progressed:

### Care Setting 1: Within GP federations ###

Enabling a GP practice or appointment hub to book, view, amend or cancel a patient’s in-hours or extended hours appointments at the patient’s registered GP practice or another GP practice within the same <a href="overview_glossary.html" data-toggle="tooltip" data-original-title="{{site.data.glossary.Federation}}">federation</a>.  

### Care Setting 2: From UC call centres to GP practices – in-hours, extended hours appointments ###
The requirement to support the use of the GP Connect capability for unscheduled care by UC services (UC call centres booking and managing appointments into GP practices) has been accommodated where possible in the API design. 
The call centre will retrieve and select in-hours or extended hours appointments for booking/managing at either: 

   - the patient’s registered GP practice

   - GP practices federated with the patient’s registered GP practice

   - a GP practice within the vicinity of the patient’s geographic location; for example, when the patient is on holiday

{% include note.html content="While the GP Connect programme primarily assumes that the appointment-hosting (provider) systems are the GP principal systems, the API technical design has accommodated the minimum viable features required to support booking and managing of appointments at UC providers such as Minor Injuries Units and GP out-of-hours services. This means that UC consumers will not need to use different APIs depending on the type of organisation they are targeting. **This deployment care setting is currently out of scope for the GP Connect programme FoT deployments, which only incorporates assurance of the API fulfilment by the GP principal provider systems. The assurance and deployment of the APIs by UC provider systems will be progressed by NHS Digital Integrated Urgent Care programmes.**" %}  


## Examples of consumer Appointment Management sessions

The use of the individual API calls listed above by consumers to fulfil business processes is illustrated with focus on the booking of an appointment. See [Appointment Management consumer sessions illustrated](appointments_consumer_sessions.html).

## Consumer code examples

Consumer side code examples are available for each of GP Connect interactions within the following GitHub repositories. The repositories contain a different branch for each release of the specification, the code within these branches matches the requirements of the specification within that release.

[.NET](https://github.com/nhsconnect/gpconnect-dotnet-examples)

[JAVA](https://github.com/nhsconnect/gpconnect-java-examples)





