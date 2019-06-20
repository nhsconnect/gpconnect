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

## What is Uncategorised Data ##
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

* Uncategorised data is any item of data in the patient record that does not fit into one of the existing or planned clinical areas defined by GP Connect

## Qualifiers ##

In GP systems, structured records can have additional coded or structured attributes that refine or expand the meaning of the coded element of the record. These additional attributes are commonly known as qualifiers. Structured records may have one or more qualifiers. The qualifiers are used refine the meaning of the coded element of the record. 

Each provider system supports a different set of qualifiers. However, there are three key qualifiers that are common across all provider systems:

* Laterality -	For example: A patient record may have a fracture of the left femur
* Severity -	For example: A patient record may have a severe asthmatic attack
* Episodicity - 	For example: This is the patients first episode of an asthmatic attack

### Common Qualifiers ###

Where the uncategorised data contains any of the three common qualifiers they will (along with the clinical code they are qualifying) be exported in a SNOMED CT expression written using ‘SNOMED CT Compositional Grammar’.


There are a number of ways of forms of expression in SNOMED CT. The simplest of these is the close-to-user (or "stated") view of an expression. This contains references to the concept together with refinements as selected by the user or as encoded by a clinical application to represent the semantics of a single clinical statement (i.e. a discrete clinical record entry). The requirements identified to support the representation of the sanctioned qualifiers used in GP systems.


The expressivity of the expressions required to represent qualifiers specified for this version of GPConnect only require a subset of the SNOMED Compositional grammar.

For example, “Fracture of left tibia” can be represented as:

* 31978002|fracture of tibia|: 272741003 |laterality| = 7771000 |left|

The terms can be omitted to shorten the expression:

* 31978002: 272741003=7771000

The expression may rendered to text:

* fracture of tibia: laterality = left


It should be noted that it is only valid to lateralise SNOMED CT concepts that are defined with a site attribute that is that is lateralisable. The lateralisable sites are defined in the refest 723264001 | Lateralizable body structure reference set (foundation metadata concept) | . It may not be possible at this stage for GP systems to compute whether the concept being qualified is defined with a lateralisable site. At this stage if data is captured with a clinical input of laterality that this should be populated in the FHIR resource.

### Other Qualifiers ###

Where the uncategorised data contains any qualifiers that are not common, they will be exported as text.

### Output ###

* The clinical code and Common Qualifiers will be exported as a single SNOMED CT expression without terms in:
  * observation.code.coding.expression.code
* The original terms text of the Clinical Code and Common Qualifiers will be exported as a single piece of human readable text in:
  * observation.code.coding.expression.text
* The original term text of the Clinical Code and all qualifiers (including common) will be exported as a single piece of human readable text in:
  * Observation.code.text


