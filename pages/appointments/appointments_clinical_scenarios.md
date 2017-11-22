---
title: Appointments Clinical Scenarios
keywords: appointments
tags: [appointments,first_of_type]
sidebar: appointments_sidebar
permalink: appointments_clinical_scenarios.html
summary: "Potential clinical scenarios for the Appointments capability."
---

The Clinical Scenarios detailed for each main API user story give examples only of how the GP Connect APIs could technically be deployed now or in the future to improve access to GP Practice Appointment Diaries subject to the local GP Practice diary configuration.  

{% include note.html content="NB For actual FoT Care Setting deployments, refer to [Appointment Management Introduction](appointment.html)" %}.

Key:

<i class='fa fa-check'/> In scope for FoT.

<i class='fa fa-road'/> Out of scope for FoT.

## Search for free slots ##

<i class='fa fa-check'/> As a Healthcare Professional at a HealthCare Organisation I would like to be able to access all available appointments at an organisation so that a Patient can be directed to appropriate care

> 1. Appointments/Admin Hub – A Patient needs to see a GP quickly and her own GP has no available slots.  Calls are diverted to the  Hub, where the team have access to extended hours appointments.  These hubs serve a number of practices and their patients and allow for the sharing off the additional workload across the membership.
> 2. Overflow Cover - Overflow telephone cover - federated phone service which can redirect calls from small practice with only 1 receptionist, to larger practice with 4 receptionists, at busy times of the day, to avoid patients getting the engaged tone, or not being answered.  Access required to Appointments for all participating practices.
> 3. Evening services (e.g. Phlebotomy, Physio) - bookable across the federation, so all practices need to be able to access the appointments book

## Retrieve a Patient's Appointments ##

<i class='fa fa-check'/> As a HealthCare Professional at a HealthCare Organisation I would like to view for a Patient their current/future appointments so that I can arrange their care appropriately

> 1. When receiving a new referral for a Community team, the team will review other healthcare professionals that are providing care to the patient and look at the schedule of visits being provided by any other teams in order that they don’t arrange visits in a schedule that might clash with, or over-burden the patient.
> 2. As a Clinician, providing care for a patient, I want to see all appointments that are already booked or scheduled for my patient with a GP so that I have a full picture of the care that is planned for my patient.
> 3. As a Clinician, being able to view all booked and scheduled GP appointments and visits enables me to ensure that I am not duplicating visits, creating appointments or schedules that clash with other appointments,  or over burden my patient by arranging for multiple appointments or visits within too short a period of time.
> 4. As a Clinician, having a view of all booked and scheduled GP appointments and visits for my patient means that I could arrange a joint visit with other healthcare professionals if appropriate in order to reduce the number of separate visits my patient has.


<i class='fa fa-road'/> As a Patient I would like to view all my current/future appointments with any care organization so that I can arrange my time accordingly.

> 1. A Patient would like to view their current/future appointments so that they can manage their time appropriately, they can access Patient Facing Services online and view their booked appointments with any GP Practice

<i class='fa fa-check'/> As a HealthCare Professional at a HealthCare Organisation I would like to view for a Patient their historical appointments so that I can manage their care appropriately.

> 1. As a Clinician, I would like to see whether my patient has already had appointments with specific GP clinics/specialties as part of gaining better understanding of their condition and care

## Book an appointment ##
<i class='fa fa-check'/> As a HealthCare Professional at a HealthCare Organisation I would like to book an appointment for a Registered Patient so that I can manage their care appropriately

> 2. As a GP I want to make an appointment for my patient with one of my local practices which provides a coil fitting clinic. 
> 3. A&E triage nurses booking appointments for patients directly into GP systems - diverting patients to the most suitable contact type for their condition, and reducing the cost of inappropriate A&E attendances Service to be available 24/7 so may be an electronic on-line booking service.
> 5. As a healthcare professional in the Admin Hub of our Federation, I want to book a GP appointment for a patient to have a home visit by our Admissions Prevention team.
> 6. As a Practice Nurse, I want to make an appointment for my patient to have bloods taken at the local GP phlebotomy service. 
> 7. As a member of the Discharge Support team in the hospital, I want to book an appointment for my patient with the District Nurse for the removal of sutures the week after discharge.

<i class='fa fa-road'/> As a HealthCare Professional at a HealthCare Organisation I would like to book an appointment for a Registered Patient with a Pharmacy so that I can manage their care appropriately

> 1. Triage to pharmacy - Primary Care Pharmacy projects - GP Triage leads to GP making appointment for patient directly into the Pharmacy system as the patient has a minor ailment or requires a Medication Review. 
> 4. As a triage nurse at A&E I want to book an appointment with a local pharmacist, for the patient who has walked into A&E with a minor illness.

<i class='fa fa-check'/> As a HealthCare Professional at a HealthCare Organisation I would like to book an appointment for an Unregistered Patient so that I can manage their care appropriately.

> 1. As an administrator at a Hub, I want to book an appointment for a patient who is not registered at a local practice in one of the Hub Appointment Sessions.  

<i class='fa fa-road'/> As a Patient I would like to book an appointment for myself so that I can manage my own care appropriately.

> 1. A Patient decides that they would like to make an appointment so that they can be seen by their GP; the Patient is able to access Patient facing Services online, search for available appointments so they can book themselves in to see their GP.

<i class='fa fa-road'/> As a Carer I would like to book for an appointment for a Patient so that the Patient can have their care managed appropriately.

> 1. A Carer who is acting on behalf of a Patient decides that they would like to make an appointment so that they can be seen by their GP; the carer is able to access patient facing Services online, search for available appointments and book the Patient in to see their GP.

## Amend Appointment ##

<i class='fa fa-check'/>As a HealthCare Professional at a HealthCare Organisation I would like to update the reason for an appointment with additional information or to correct errors without having to cancel and rebook the appointment so that the Patients appointment is not taken by another patient.

> 1.	A nurse realises that an appointment that has been made for a Patient does not highlight that the Patient is a wheelchair user and will require to be seen in a room in the surgery on the ground floor. The nurse is able to update the appointment with this information so that the Patient can be accommodated for their appointment.

## Cancel Appointment ##

<i class='fa fa-check'/>As a HealthCare Professional at a HealthCare Organisation I would like to cancel an appointment that I have made at any HealthCare Organisation so that Appointment lists are kept up to date and accurate.

> 1. A Patient realises that she isn’t going to be able to make her GP appointment the next morning but it is already 6pm.  Previously there would have been no way of letting the Surgery know but now she can call the Surgery because there is someone on the phone at the local admin hub from 7am until 8pm.  She is able to cancel her appointment, thus freeing it up for someone else to book.

<i class='fa fa-check'/> As a HealthCare Professional at a HealthCare Organisation I would like to cancel an appointment made by another HealthCare Organisation so that an appointment can be made available at the earliest opportunity .

> 1. It’s an extended-hours appointment and the GP is seeing a patient who is not registered at his Practice.  Whilst treating the patient the GP notices that she has an appointment the following week for her quarterly BP check.  To save her coming in again the following week, the GP measures and records her BP there and then and as it is stable, he cancels the appointment next week.

<i class='fa fa-road'/> As a Patient I would like to cancel an appointment that I have made at any HealthCare Organisation so that my Appointment list is kept up to date and accurate

> 1. A patient realises that she isn’t going to be able to make her GP appointment the next morning but it is already 6pm.  Previously there would have been no way of letting the Surgery know but now she can call the Surgery because there is someone on the phone at the local admin hub from 7am until 8pm.  She is able to cancel her appointment, thus freeing it up for someone else to book.
> 2. A Patient decides that they would like to cancel their appointment as the Patient is no longer able to attend; the Patient is able to access Patient Facing Services online, view their booked appointments and then cancel the relevant appointment thus freeing it for someone else to book.

<i class='fa fa-road'/> As a Carer for a Patient I would like to cancel an appointment that I have made at any HealthCare Organisation for a Patient so that the Patients' Appointment lists is kept up to date and accurate
	
> 1. A Carer who is acting on behalf of a Patient decides that they would like to cancel a Patients appointment as they are no longer able to attend; the carer is able to access Patient Facing Services online on behalf of the appointment, view the Patients’ booked appointments and then cancel the relevant appointment thus freeing it for someone else to book.




