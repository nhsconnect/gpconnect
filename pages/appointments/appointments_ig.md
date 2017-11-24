---
title: Information Governance
keywords: appointments ig
tags: [ig,appointments]
sidebar: appointments_sidebar
permalink: appointments_ig.html
summary: "Information Governance controls applicable to the Appointment Management capability."
---

## GP Connect Information Governance Principles##

The GP Connect core [Information Governance Principles](designprinciples_ig_principles.html) apply to the Appointment Management capability, with the application of the following specific controls:

## Organisational Data-Sharing ##

Currently, all organisations participating in a GP Connect deployment must have a Data-Sharing Agreement (DSA) covering the use of a specific GP Connect Capability API set.  This control was required and implemented to support the need for Data Controller confidence in the organisation having access to patient clinical information. It is intended to be a short/medium term solution given the strategic work underway to agree a national data-sharing model and its implementation.

This requirement is enforced via SSP, ensuring that GP Connect interactions are only forwarded from deployment-assured participating consuming to providing organisations for a specific capability.

### National Urgent Care Call Centres ###

To support Care Setting 2 FoT deployments, Urgent Care Consumers booking into and managing GP Practice In-Hours and Extended Hours appointments are required to be part of a Data-Sharing group with catchment GP Practices. 

This local UC call centre function is augmented by a national distributed call centre service whose organisations will need to be incorporated into the local DSA covering the GP Connect Appointment Management deployment. 

The local UC organisation is required to make the Data Controllers of the GP practices within its DSA aware of the participation of the other call-centres




{% include note.html content="Details of how to [Register a Patient](foundations_use_case_register_a_patient.html) can be found in the Foundations capability pack. " %}

