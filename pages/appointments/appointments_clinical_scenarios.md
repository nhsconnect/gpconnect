---
title: Clinical scenarios
keywords: appointments
tags: [appointments,first_of_type]
sidebar: appointments_sidebar
permalink: appointments_clinical_scenarios.html
summary: "Potential clinical scenarios for the Appointment Management capability pack"
---

The clinical scenarios below detail the representative business use cases which the Appointment Management API specification supports for First of Type (FoT) scope and can potentially support in the longer term.

{% include note.html content="For First of Type (FoT) care setting deployments, refer to [Appointment Management Introduction](appointments.html)" %}

Key:

<i class='fa fa-check'/> In scope for FoT.

<i class='fa fa-road'/> Out of scope for FoT.

## Search for free slots ##

<i class='fa fa-check'/> As a Healthcare Professional at a HealthCare Organisation I would like to be able to access all available appointments at an organisation so that a Patient can be directed to appropriate care.

> 1. Appointments/Admin Hub – A Patient needs to see a GP quickly and her own GP has no available slots.  Calls are diverted to the  Hub, where the team have access to extended hours appointments.  These hubs serve a number of practices and their patients and allow for the sharing of the additional workload across the membership.
> 2. Overflow Cover - Overflow telephone cover - federated phone service which can redirect calls from small practice with only 1 receptionist, to larger practice with 4 receptionists, at busy times of the day, to avoid patients getting the engaged tone, or not being answered.  Access required to Appointments for all participating practices.
> 3. Evening services (for example, Phlebotomy, Physio) - bookable across the federation, so all practices need to be able to access the appointments book.

<i class='fa fa-check'/> As a GP Practice Manager, I would like to be able to manage and control access to the Practice's available appointments so that ultimately patients have access to the right appointment according to their requirement.

<i class='fa fa-check'/> As an Urgent Care Service Manager, I would like to have confidence that appointment slots agreed with GP Practices to be designated for the use of Urgent Care are not made available to other organisations so that our patients have access to the right appointment according to their requirement

## Retrieve a patient's appointments ##

<i class='fa fa-check'/> As a healthcare professional at a healthcare organisation I would like to view for a patient their future appointments so that I can arrange their care appropriately.

> 1. As a clinician, being able to view all booked and scheduled GP appointments and visits enables me to ensure that I am not duplicating visits, creating appointments or schedules that clash with other appointments or over burden my patient by arranging for multiple appointments or visits within too short a period of time.
> 2. As a clinician, having a view of all booked and scheduled GP appointments and visits for my patient means that I could arrange a joint visit with other healthcare professionals if appropriate in order to reduce the number of separate visits my patient has.

<i class='fa fa-road'/> When receiving a new referral for a community team, the team will review other healthcare professionals that are providing care to the patient and look at the schedule of visits being provided by any other teams in order that they don’t arrange visits in a schedule that might clash with other visits or over-burden the patient.

<i class='fa fa-road'/> As a patient I would like to view all my future appointments with any care organization so that I can arrange my time accordingly.

> 1. A patient would like to view their future appointments so that they can manage their time appropriately. They can access patient-facing services online and view their booked appointments with any GP practice.

## Book an appointment ##

<i class='fa fa-check'/> As a healthcare professional at a healthcare organisation I would like to book an appointment for a registered patient so that I can manage their care appropriately.

> 1. As an urgent care call centre handler requiring an in-hours or extended hours GP appointment for a patient, I would like to make an appropriate appointment directly from within my system.
> 2. As a GP I want to make an appointment for my patient with one of my local practices which provides a coil fitting clinic.
> 3. A&E triage nurses able to book appointments for patients 24/7 directly into GP systems - diverting patients to the most suitable contact type for their condition, and reducing the cost of inappropriate A&E attendances. Service to be available 24/7.
> 4. As a practice nurse, I want to make an appointment for my patient to have bloods taken at the local GP phlebotomy service.

<i class='fa fa-check'/> As a healthcare professional at a healthcare organisation I would like to book an appointment for an unregistered patient so that I can manage their care appropriately.

> 1. As an administrator at a hub, I want to book an appointment for a patient who is not registered at a local practice in one of the hub appointment sessions.

<i class='fa fa-road'/>  As a healthcare professional in the admin hub of our federation, I want to book a GP appointment for a patient to have a home visit by our admissions prevention team.

<i class='fa fa-road'/>  As a member of the discharge support team in the hospital, I want to book an appointment for my patient with the district nurse for the removal of sutures the week after discharge.

<i class='fa fa-road'/> As a healthcare professional at a healthcare organisation I would like to book an appointment for a registered patient with a pharmacy so that I can manage their care appropriately.

> 1. Triage to pharmacy - primary care pharmacy projects - GP triage leads to GP making appointment for patient directly into the Pharmacy system as the patient has a minor ailment or requires a medication review.

> 2. As a triage nurse at A&E, I want to book an appointment with a local pharmacist for the patient who has walked into A&E with a minor illness.

<i class='fa fa-road'/> As a patient, I would like to book an appointment for myself so that I can manage my own care appropriately.

> 1. A patient decides that they would like to make an appointment so that they can be seen by their GP; the patient is able to access patient-facing services online and search for available appointments so they can book themselves in to see their GP.

<i class='fa fa-road'/> As a carer, I would like to book for an appointment for a patient so that the patient can have their care managed appropriately.

> 1. A carer who is acting on behalf of a patient decides that they would like to make an appointment so that they can be seen by their GP; the carer is able to access patient-facing services online, search for available appointments and book the patient in to see their GP.

## Amend appointment ##

<i class='fa fa-check'/>As a healthcare professional at a healthcare organisation I would like to update the appointment description and/or comment on behalf of the patient with additional information or to correct errors without having to cancel and rebook the appointment and potentially losing the slot in the process.

> 1. A nurse realises that an appointment that has been made for a patient does not highlight that the patient is a wheelchair user and will require to be seen in a room in the surgery on the ground floor. The nurse is able to update the appointment with this information so that the patient can be accommodated for their appointment.

## Cancel appointment ##

<i class='fa fa-check'/>As a healthcare professional at a healthcare organisation I would like to cancel a patient's appointment on their behalf so that missed appointments are reduced and appointment lists are kept up to date and accurate.

> 1. A patient realises that she isn’t going to be able to make her GP appointment the next morning, but it is already 6pm. Previously there would have been no way of letting the surgery know, but now she can call the surgery because there is someone on the phone at the local admin hub from 7am until 8pm who can cancel her appointment via their system, thus freeing it up for someone else to book.

<i class='fa fa-check'/> As a healthcare professional at a healthcare organisation, I would like to cancel an appointment made by another healthcare organisation so that the patient can be seen at the earliest or more convenient time, and the original appointment made available for re-booking.

> 1. It’s an extended-hours appointment and the GP is seeing a patient who is not registered at his practice. Whilst treating the patient the GP notices that she has an appointment the following week for her quarterly blood pressure (BP) check. To save her coming in again the following week, the GP measures and records her BP there and then and, as it is stable, he cancels the appointment next week.

<i class='fa fa-road'/> As a patient, I would like to cancel an appointment that I have made at any healthcare organisation so that my appointment list is kept up to date and accurate.

> 1. A patient decides that they would like to cancel their appointment as the patient is no longer able to attend; the patient is able to access patient-facing services online, view their booked appointments and then cancel the relevant appointment - thus freeing it for someone else to book.

<i class='fa fa-road'/> As a carer for a patient, I would like to cancel an appointment that I have made at any healthcare organisation for a patient so that the patients' appointment list is kept up to date and accurate.

> 1. A carer who is acting on behalf of a patient decides that they would like to cancel a patient's appointment as they are no longer able to attend; the carer is able to access patient-facing services online on behalf of the appointment, view the patient's booked appointments and then cancel the relevant appointment - thus freeing it for someone else to book.
