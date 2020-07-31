---
title: Known issues
keywords: structured, design, known issues, bugs
tags: [structured,design]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_known_issues.html
summary: "Known issues related to the Access Record Structured capability pack"
---

## Allergy interoperability and clinical safety ##

Allergies are currently recorded using multiple schemes across general practice systems and, therefore, may not be understood or fully interoperable in consuming systems.

When considering the implementation of use cases involving allergy/intolerance, consumers and their suppliers **SHALL** perform an appropriate clinical safety assessment and obtain the necessary clinical safety approvals for the processing performed by their system.

Please read [the following guidance](http://gpconnect.netlify.com/accessrecord_structured_development_allergies_guidance.html#allergyintolerance-interoperability-and-clinical-safety) for further information.

## PractitionerRole

There is an issue with the PractitionerRole resource in the base FHIR&reg; specification. It occurs in GP Connect when a practitioner has more than one PractitionerRole associated with them and both are returned in the same bundle.

An example of where this happens would be if a list of medications contained two medications that were prescribed by the same practitioner:

1. Medication 1, prescribed by Practitioner at Practice A
2. Medication 2, prescribed by Practitioner at Out of Hours service B

Two PractitionerRole resources would be created that both relate to the same practitioner. However, as the MedicationRequest resource only references the practitioner and not PractitionerRole it will be impossible to ascertain which PractitionerRole relates to which medication.

This issue may occur for any profile where there is a reference to Practitioner rather than PractitionerRole

As a workaround for this issue, in GP Connect when providing responses to queries systems **MUST** only supply 1 PractitionerRole per practitioner. If more than one should exist then the system **MUST NOT** supply any.

## Consultation retrieval ##

Depending on the provider system not every item in a patient's clinical record will be recorded as part of a consultation. Therefore, a consumer system making consultation-oriented queries only must not expect to obtain all items in the patient record.

## Data quality ##

The purpose of GP Connect is to make the data recorded in the patient's GP practice record available throughput the NHS to support the direct care of the patient. If there are any gaps, mistakes or other quality issues with the data in the GP practice record, these issues will show up in the data supplied by GP Connect. The quality of data will depend on the work done by local GP practices and will vary a great deal across the estate.

Further work to improve the quality of data recorded in the GP practice is outside the scope of GP Connect.

## Blood pressure
Guidance on how to populate [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1) with blood pressure information needs to go through the curation process

## CodeableConcept guidance
The CodeableConcept guidance document needs to go through curation

## Immunisations
The CareConnect immunisation profile is currently subject to curation regarding potential changes to the way in which it defines immunisation events where the vaccine is not given.
This specification will needed to be updated in due course with any changes resulting from that curation process.
