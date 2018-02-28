---
title: Medication
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication_guidance.html
summary: "Guidance for populating and reading the Medication resource"
---

## FHIR medication profiles ##
FHIR has a number of resources that are available to represent different concepts related to medications. These resources that are intended to cover the full medication lifecycle.
* Medication - contains details the actual medicication or medical device
* Medication Request - is designed to cope with planning, proposing or ordering medications
* Medication Dispence - is to represent exactly what medication was dispensed. I n some cases this can differ slightly from what was ordered/prescribed.
* Medication Administration - is to be used to describe when the medication is administered, how it was given and by whom.
* Medication Statement - This is to make a statement about the medication a person has taken and can be 'based on' a record of  
In GP Connect we are only interested in the medication data that is captured in GP clinical systems. This data is about the practices record of medication the patient has taken and whether that has been prescribed by a clinician at that practice. Therefore in order be able to represent the information that is available in the GP systems we are interested in 3 of the above FHIR profiles Medication, Medication Request and Medication Statement. In later sections these will all be detailed at a data item level.

## Using the FHIR profiles to represent the ordering process
The majority of the information in GP systems that GP Connect needs to represent is in the forms described above. That is either an order/prescription that has been actioned by a clinician at the practice or a medication that the practice has been informed that a patient has taken. To represent this using FHIR GP suppliers must create a Medication Statement about each medication record that is contained on the GP system. Each Medication Statement will reflect an item that was ordered using one of the 3 business processes previously described or a medication that was prescribed elsewhere but has been recorded by a clinician at the practice. 
Where a Medication Statement represents an order it will be 'basedOn' a Medication Request or a number of Medication Requests that reflect the ordering/prescribing of that medication or medical device by the practice. 
The GP Connect profile of the FHIR medication request will be used to represent the 2 stages of the ordering process, 
1. The authorisation - in conjunction with MedicationStattement, a MedicationRequest with an intent of 'plan' represents an authorisation for acute, repeat, repeat dispensed medication
2. The issue - each time the medication is issued then a medication request with the intent element set to 'plan'. There will be one 'order' for acutes but may be many for repeats.

### Acute medication representation ###
Acute UML diagram:

{: .center-image }
![Acute medications diagram](images/access_structured/Acute medication representation.png)

An acute medication will be represented by a medication statement that is based on a medication request with the intent of 'plan' that has a single medication request with the intent of 'order' associated to it. The order will be 'basedOn' the plan using that element to reference the Medication request with intent set to 'plan'. This is illustrated in the diagram above.

### Repeat prescription and repeat dispensing ###
Repeat prescription and dispensing UML diagram:

{: .center-image }
![Repeat prescription and repeat dispensing diagram](images/access_structured/Repeat prescription and repeat dispensing.png)

Both repeat prescriptions and repeat prescribing are represented in a similar manner to the acute medications. The difference is that there is now a one to many relationship where there can be one Medication Request with intent='Plan' and it can relate to many Medication Requests that have intent='order'. In this relationship for every time a repeat has been issued it will be represented by a sparate Medication Request with intent='order'.
All medication request resources that are related to a record of a repeat dispense
For repeat dispensed medication some of the resources relating to individual issues may be post dated if the effective period of the medication has not elapsed.

### Unissued medications and medication prescribed elsewhere ###
Unissued prescription and dispensing UML diagram:

{: .center-image }
![Unissued medications and medications prescribed elsewhere diagram](images/access_structured/Unissued medications and medications prescribed elsewhere.png)

Unissued medications and medications that have been prescribed elsewhere that have been added to the system by a clinician at the practice will be represented by a Medication Statement and a Medication Request where intent='plan' but with no further resources.

### Degraded medications ###
Where degraded medication records arising from GP2GP record transfer are present in the patient record then these should be coded using the appropriate degrade code (196421000000109, Transfer-degraded medication entry) with the original medication name conveyed by CodeableConcept/text.

### Medication interoperability ###
Consumers of medication resources generated by other systems should consider the clinical safety issues arising from processing medication information recorded in different care settings and contexts and seek clinical safety guidance where appropriate. 

Key concerns are the understandibility of received medication information and appropriate actions to degrade and identify medication concepts which are not understood by the receiving system. Appropriate clinical workflows may also be required at the receiver e.g. deactivation of revceived medications such that they must be explicitly re-authoraised to make them issueable.

Currently dosage and quantity information are expressed in unstructured/textual form. A system intending to consume dosage and quantity information needs to be capable of handling unstructured quantities and dosages.

### Mixtures ###
On some systems it is possible to prescribe custom formulations compounded from a number of other medications (extemporaneous preparations). Mixtures should be expressed using the degrade code (196421000000109, Transfer-degraded medication entry) with the consituents of the mixture expressed via CodeableConcept/text.

### Non dm+d medications ###
In some cases drugs may be recorded as freetext or may be present in the original systems drug dictionary but not in DM+D. Where no DM+D code is available to describe the medication then the medication code should be expressed using the degrade (196421000000109, Transfer-degraded medication entry) with the original drug name present in CodeableConcept/text. 

### dm+d name versus displayed name ###
It is possible for historic/legacy medications to be displayed with a name corresponding to the name in the original systems drug dictionary rather than the DM+D name. This name should be preserved via CodeableConcept/text when representing the medication via resources. CodeableConcept/text is rendundant when the displayed medication name on the original system and the DM+D name are identical and in these cases CodeableConcept/text should be omitted.

### Medication reviews ###
The resources required to describe diarised review activities and reminders for medication reviews are out of scope for this guidance. 

### Future dated prescriptions ###
Medication issues may be future dated e.g. repeat dispensed medications.

### Amendments ###
Where an authorisation is amended e.g. Proprietary/Generic switch, altered dates, change of quantities etc ... then the existing authorisation should be stopped/discontinued and and appropriate reason supplied via detectedIssue. A new authorisation should be created to hold the amended details and subsequent issues of the medication should reference the amended authorisation rather than the previous version.

### Medication discontinuation/stopping ###
Where a medication is stopped/discomtinued then the status of the authorisation should be changed to 'stopped' and a textual stop reason provided via detectedIssue/detail.

A detectedIssue should not be generated when an authorisation has simply expired (exceeded review date or number of issues)


### Re-authorisation ###
Where a medication is re-authorised a new authorisation should be generated and subsequent issues of the medication should reference the new authorisation.

### Exceeding issues ###
*** TO DO Web ability to go beyond number of issues or dates without re-authorisation

### Medication list query ###
Out of scope for this document
* Full Medication List including all issues
* Current Medication List - active repeats and medication issued in last month
* How much can be done via generic FHIR query,_filter
* Empty list behaviour

