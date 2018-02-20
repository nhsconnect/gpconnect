---
title: Information governance
keywords: appointments ig
tags: [ig,appointments]
sidebar: appointments_sidebar
permalink: appointments_ig.html
summary: "Information governance controls applicable to the Appointment Management capability pack."
---

## GP Connect information governance principles ##

The GP Connect core [Information Governance Principles](designprinciples_ig_principles.html) govern the Appointment Management capability, with the following capability-specific application:

## Organisational data sharing ##

Currently, all organisations participating in a GP Connect deployment must have a data-sharing agreement (DSA) covering the use of a specific GP Connect capability API set.  This control was required and implemented to support the need for data controller confidence in the organisation having access to patient clinical information. It is intended to be a short/medium term solution given the strategic work underway to agree a national data-sharing model and its implementation.

The list of participating organisations and data controllers who have signed the supporting DSA will be submitted as part of the NHS Digital Solutions Assurance conformance requirements.

The participating organisation interoperability relationship is then enforced via the Spine Security Proxy (SSP), ensuring that GP Connect interactions are only forwarded from deployment-assured participating consuming to providing organisations for a specific capability.

### Urgent care - national call centres ###

To support Care Setting 2 FoT deployments, urgent care consumers booking into and managing GP Practice In-Hours and Extended Hours appointments are required to be part of a Data-Sharing group with catchment GP Practices. 

This local UC call centre function is augmented by a national distributed call centre service whose organisations will need to be incorporated into the local DSA covering the GP Connect Appointment Management deployment. 

The local UC organisation is required to make the Data Controllers of the GP practices within its DSA aware of the participation of the other call-centres.

## Patient Dissent To Share ##

This flag must NOT be applied by Provider systems based on the following:

   -  the objective of the Appointment Management capability is primarily to support administrative cross-organisational workflow whereas this flag currently represents the patient's dissent from sharing their registered GP medical record
   -  the flag only potentially exists at the patient's registered GP practice, whereas the aim of this capability is to support Appointment Booking and Management at practices other than the registered one
   -  Fair Processing communications at participating GP Practices must make clear to patients that limited clinical information may be released in the Appointment Reason, Description or Comment to support the shared Appointment availability services operated within the Federation
   -  At the point of Appointment Booking, Amending or Cancellation, the patient must be given clear communication regarding potential clinical information being visible as part of the activity, so that they have the opportunity then to decline

## PDS Sensitive Flag (S-Flag) ##

The Provider System is expected, when identifying an 'S-flagged' Patient, to substitute their location and contact details with those of the GP Practice.  

## Legally-Restricted Data ##

Whilst it is expected that GP Practices will configure their appointment book to ensure appropriate restriction of appointments being available to external organisation, it is possible that such information may be exposed in the Appointment Reason, Description, and Comment elements, which cannot necessarily be prevented technically.  The privacy impact to be mitigated by participating organisation (consumer and provider) end-user policies, procedures, registration and regulation.




