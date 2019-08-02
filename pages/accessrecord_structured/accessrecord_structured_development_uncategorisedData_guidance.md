---
title: Uncategorised data guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_uncategorisedData_guidance.html
summary: "Guidance for populating and consuming the uncategorised data from GP systems using GP Connect"
---

## What is categorised data? ##
When a clinician/user of a GP clinical system records clinical data they may, as part of entering the information, identify what type of information they are recording.

For example, where the clinician uses a GP system's allergy function to record a patient’s allergy information it is explicitly identified in the system as an allergy.

The volume of this categorisation varies between provider systems. For the majority of provider systems, the following types of information are explicitly categorised when they are recorded.
* Allergy
* Appointment
* Consultation
* Demographics
* Diary Entry
* Document
* Flag/Alert
* Immunisation
* Medication and Medical Device
* Problem
* Referral
* Test Request
* Investigation

## What is uncategorised data? ##
There is data that a clinician/user will enter without identifying what type of information they are recorded. This information is usually entered as either free text or a combination of clinical code(s), values, qualifiers and text.

For example:
* the clinician records the patient’s resting pulse by recording the resting pulse clinical code followed by a value of the patient’s pulse.
* the clinician records that a patient has a sore throat by recording the sore throat clinical code
* the clinician records that a patient reports being irritable with their family as a piece of free text

Consideration was given to attempting to categorise data using the recorded clinical codes. It was decided not to progress this based on a clinical review of its risks and benefits.

## Uncategorised data definition ## 

* Uncategorised data is any item of data in the patient record that does not fit into one of the existing or planned clinical areas defined by GP Connect.

## Qualifiers ##

In GP systems, uncateogirsed data may have additional coded or structured attributes that refine or expand the meaning of the coded element of the record. These additional attributes are commonly known as qualifiers.

Each provider system supports a different set of qualifiers. However, there are three key qualifiers that are common across all provider systems:

* Laterality - for example, a patient record may have a fracture of the left femur.
* Severity - for example, a patient record may have a severe asthmatic attack.
* Episodicity - for example, this is the patient's first episode of an asthmatic attack.

The provider system will translate all of the qualifiers included with the clinical code into human-readable text and concatenate them with the text entered by the recorder (placing the qualifiers first) and placing in observation.comment.

## Values ##

Values are any reading or result that is recorded with the uncategorised data. For example, the uncategorised data 50373000 (Body Height) may have a value of 156cm.

### Single values ###
The majority of uncategorised data that contains values will only have a single value. In these cases, the value will be exported in observation.value.

### Multiple Values ###
There are some cases where an item of uncategorised data may contain multiple values. This happens when:
* there is a single clinical code that describes the uncategorised data as a whole
and
* each recorded value in the uncategorised data is described by its own clinical code

In these cases, each value will be exported in an instance of observation.component.

## Blood pressure ##
Where the clinician/user has explicitly chosen the clinical codes to record a blood pressure reading in the provider system, the provider system **MUST** export the blood pressure reading as uncategorised data using the clinical codes (or SNOMED CT translations) chosen by the clinician/user.

Where the clinician/user has NOT explicitly selected the clinical codes to record a blood pressure reading in the provider system, the provider system **MUST** export the blood pressure using the CareConnect Blood Pressure observation:

    https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-BloodPressure-Observation-1


## Using the `List` resource for uncategorised data queries

The results of a query for uncategorised data **MUST** return a `List` containing references to all `Observation` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason` with the value `noContent`.


