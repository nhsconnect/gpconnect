---
title: Appointment Management information governance
keywords: appointments ig
tags: [ig,appointments]
sidebar: appointments_sidebar
permalink: appointments_ig.html
summary: "Information governance controls applicable to the Appointment Management capability pack."
---

## GP Connect information governance principles ##

The GP Connect core [information governance principles](designprinciples_ig_principles.html) govern the Appointment Management capability pack, with the following capability-specific application:

## Organisational data sharing ##

Currently, all organisations participating in a GP Connect deployment must have a data-sharing agreement (DSA) covering the use of a specific GP Connect capability API set. This control was required and implemented to support the need for data controller confidence in the organisation having access to patient clinical information. It is intended to be a short/medium term solution given the strategic work underway to agree a national data-sharing model and its implementation.

The list of participating organisations and data controllers who have signed the supporting DSA will be submitted as part of the NHS Digital Solutions Assurance conformance requirements.

The participating organisation interoperability relationship is then enforced via the Spine Security Proxy (SSP), ensuring that GP Connect interactions are only forwarded from deployment-assured participating consuming to providing organisations for a specific capability.

### Urgent care (UC) - national call centres ###

To support Care Setting 2 FoT deployments, urgent care consumers booking into and managing GP practice in-hours and extended hours appointments are required to be part of a data-sharing group with catchment GP practices. 

This local UC call centre function is augmented by a national distributed call centre service whose organisations will need to be incorporated into the local DSA covering the GP Connect Appointment Management deployment. 

The local UC organisation is required to make the data controllers of the GP practices within its DSA aware of the participation of the other call centres.

## Patient Dissent To Share ##

This flag must NOT be applied by provider systems based on the following:

   -  the objective of the Appointment Management capability is primarily to support administrative cross-organisational workflow, whereas this flag currently represents the patient's dissent from sharing their registered GP medical record
   -  the flag only potentially exists at the patient's registered GP practice, whereas the aim of this capability is to support appointment booking and management at practices other than the registered one
   -  fair processing communications at participating GP Practices must make clear to patients that limited clinical information may be released in the Appointment Description or Comment to support the shared appointment availability services operated within the federation
   -  At the point of Appointment Booking, Amending or Cancellation, the patient must be given clear communication regarding potential clinical information being visible as part of the activity, so that they have the opportunity then to decline

## PDS sensitive flag (S-Flag) ##

The provider system is expected, when identifying an 'S-flagged' patient, to substitute their location and contact details with those of the GP practice.  

## Legally-restricted data ##

Whilst it is expected that GP practices will configure their appointment book to ensure appropriate restriction of appointments being available to external organisations, it is possible that such information may be exposed in the Appointment Description and Comment elements, which cannot necessarily be prevented technically. The privacy impact shall be mitigated by participating organisation (consumer and provider) end-user policies, procedures, registration and regulation.




