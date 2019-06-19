---
title: Observation - uncategorised data
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_uncategorisedData_guidance.html
summary: "Guidance for populating and consuming the uncategorised data from GP systems using GP Connect"
---

## What is Categorised Data ##
When a clinician / user of a GP Clinical System records clinical data they may, as part of entering the information, identify what type of information they are recording.

For example, where the clinician uses a GP systems allergy function to record a patient’s allergy information it is explicitly identified in the system as an allergy.

The volume of this categorisation varies between provider systems. For the majority of provider systems, the following types of information are explicitly categorised when they are recorded.
* Allergy
* Appointment
* Consultation
* Demographics
* Diary Entry
* Document
* Flag / Alert
* Immunisation
* Medication and Medical Device
* Problem
* Referral
* Test Request
* Test Result

## What is Categorised Data ##
There is data that a clinician / user will enter without identifying what type of information they are recorded. This information is usually entered as either free text or a combination of clinical code(s), values, qualifiers and text.

For example:
* The clinician records the patient’s resting pulse by recording the resting pulse clinical code followed by a value of the patient’s pulse.
* The clinician records that a patient has a sore throat by recording the sore throat clinical code
* The patient records that a patient reports being irritable with their family as a piece of free text

For the majority of provider systems, the following types of information are not explicitly categorised when they are recorded.
* Condition
* Family History
* Observation
* Procedure

Consideration was given to attempting to categorise data using the recorded clinical codes. It was decided not to progress this based on a clinical review of its risks and benefits.

## Uncategorised Data Definition ## 
Different provider systems have different levels of classification. This could result in one system seeing data as uncategorised while another can assign it a category. To different intepretations, GP Connect defined uncategorised data as:

* Any item of data in the patient record that does not fit into one of the clinical areas defined by GP Connect

