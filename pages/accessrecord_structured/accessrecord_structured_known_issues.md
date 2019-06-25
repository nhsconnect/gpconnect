---
title: Access Record Structured Known Issues
keywords: structured, design, known issues, bugs
tags: [structured,design]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_known_issues.html
summary: "Known issues related to the Access Record Structured capability pack."
---

## Allergy interoperability and clinical safety ##

Allergies are currently recorded using multiple schemes across general practice systems and therefore may not be understood or fully interoperable in consuming systems.

When considering the implementation of use cases involving allergy/intolerance consumers and their suppliers **SHALL** perform an appropriate clinical safety assessment and obtain the necessary clinical safety approvals for the processing performed by their system.

Please read [the following guidance](http://gpconnect.netlify.com/accessrecord_structured_development_allergies_guidance.html#allergyintolerance-interoperability-and-clinical-safety) for further information.

## PractitionerRole

There is an issue with the PractitionerRole resource in the base FHIR specification. It occurs in GP Connect when a Practitioner has more than one PractitionerRole associated with them and both are returned in the same bundle. 

An example of where this happens would be if a list of Medications contained 2 Medications that were prescribed by the same Practitioner,

1. Medication 1, prescribed by Practitioner at Practice A
2. Medication 2, prescribed by Practitioner at Out of Hours service B

2 PractitionerRole resources would be created that both relate to the same Practitioner. However, as the MedicationRequest resource only references the Practitioner and not PractitionerRole it will be impossible to ascertain which PractitionerRole relates to which medication.

As a workaround for this issue in GP Connect when providing responses to queries systems **MUST** only supply 1 PractitionerRole per Practitioner. If more than 1 should exist then the system **MUST NOT** supply any.

## Consultation Retrieval ##

Depending on the provider system not every item in a patient's clinical record will be recorded as part of a consultation. Therefore a consumer system making Consultation oriented queries only must not expect to obtain all items in the patient record.
