---
title: Medication guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication_guidance.html
summary: "Guidance on the representation of medication in GP Connect"
---

## Ordering process in GP systems for medications and medical devices 
The medication or medical device ordering process in GP systems can be considered to be a 2-stage process.
1. The authorisation - this is where the medication or medical device is initially added on to the GP systems. It represents a 'plan' that the GP intends to authorise a medication for the patient.
2. The issue - this is the point the plan is turned into an actual 'order' or prescription. At this point the prescription will either be printed and signed, or the order will be passed on to the Electronic Prescription Service to send to the patient’s nominated pharmacy.

There are several clinical reasons why the process is split up in this way. Below are some examples of scenarios when it advantageous to have the separate parts:

* repeat medication added from a discharge summary ready for patient to request 
* add blood pressure (BP) drug ready for follow-up nurse clinic to issue
* issue rescue steroid/antibiotic pack and add repeats for flares 
* flu vaccinations

There are 3 different business processes for issuing a medication to a patient that are well established in general practice and are driven by factors such as how often a patient will require the medication, helping practices to create efficient processes for prescribing and applying the appropriate controls to drugs where appropriate. The 3 processes are:

 1. Acute prescribing
 2. Repeat prescribing
 3. Repeat dispensing
 
### Acute prescriptions
An acute prescription is when a medication or medical device is a one-off prescription. It is usually a course of medication that is issued to treat a specific complaint. 
If the patient needs further medication they would need to see their doctor again for them to assess their condition and decide if another prescription is appropriate.

### Repeat prescriptions
A repeat prescription enables a patient to be issued more than one prescription without it being necessary to see their doctor after each individual prescription. The number of prescriptions is usually determined by the doctor when they make the initial order. However, it is also possible to set a review date for a medication or medical device that is prescribed in a regular manner instead of limiting the number of issues. Typically, the duration that repeat prescriptions cover is 6 or 12 months although they are flexible and can be written for any period. 
Although the patient does not have to see their doctor to authorise each issue of the medication, they will need to have the prescription authorised by another clinician in the practice. 

### Repeat dispensing
When a medication or medical device is repeat-dispensed the patient will be able to pick up the item from the pharmacy without the need for each prescription to be issued by the GP practice.
Apart from the practice not needing to issue each prescription, repeat-dispensing works in a similar manner to repeat prescriptions where the doctor is able to determine the number of issues or the time period before needing to visit the doctor again for the prescription to be re-authorised.


## Medication prescribed elsewhere
In GP systems, in addition to ordering medications and issuing them to a patient, it is also possible for clinicians to record medication that was not issued by their GP practice. This may happen if a patient has been in hospital and informs a clinician that they were prescribed a medication or allocated a medical device during that episode of care. All GP systems allow for data to be entered to record details of medications that they are informed about, but do not issue within the medication section in the system.
The main uses are to record a medication or medical device being managed by another organisation, the requirement to enable interaction checking and decision support to interact with these items.

## FHIR medication resources
FHIR has a collection of resources that are available to represent different concepts related to medications. These resources are intended to cover the full medication lifecycle:
* [`Medication`](accessrecord_structured_development_medication.html) - contains details of the actual medication or medical device
* [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) - is designed to cope with planning, proposing or ordering medications
* `MedicationDispense` - is to represent exactly what medication was dispensed. In some cases, this can differ slightly from what was ordered/prescribed.
* `MedicationAdministration` - is to be used to describe when the medication is administered, how it was given and by whom.
* [`MedicationStatement`](accessrecord_structured_development_medicationstatement.html) - this is to make a statement about the medication a person has taken and can be 'basedOn' a record of an historic prescription that would be represented using one or more MedicationRequest resources.  

In GP Connect, we are interested in the medication data that is captured in GP clinical systems. This data is about the practice’s record of medication the patient has taken and whether that has been prescribed by a clinician at that practice. 

Therefore, in order be able to represent the information that is available in the GP systems we are interested in 3 of the above FHIR profiles: 

- `Medication`
- `MedicationRequest`
- and `MedicationStatement`

`MedicationDispense` and `MedicationAdministration` are not used in this capability.

In later sections these are detailed at a data item level.

## Using the FHIR profiles to represent the ordering process

Most of the information in GP systems that GP Connect needs to represent is in the forms described above. That is, either an order/prescription that has been actioned by a clinician at the practice or a medication or medical device that the practice has been informed that a patient has been prescribed. 

To represent this using FHIR, GP suppliers **MUST** create a `MedicationStatement` about each medication or medical device record that is contained on the GP system. Each `MedicationStatement` will reflect an item that was ordered using one of the 3 business processes previously described or a medication or medical device that was prescribed or allocated elsewhere but has been recorded by a clinician at the practice. 

Where a medication statement represents an order, it will be based on a one or more `MedicationRequest` resources that reflect the ordering/prescribing of that medication or medical device by the practice. 

The GP Connect profile of the `MedicationRequest` will be used to represent the 2 stages of the ordering process:

1. **The authorisation** - in conjunction with `MedicationStatement`, a `MedicationRequest` with an intent of `plan` represents an authorisation for acute, repeat, repeat dispensed medication.

2. **The issue** - each time the medication is issued then it **SHOULD** be represented using a `MedicationRequest` with the intent element set to `order`. There will be one `order` for acutes but may be many for repeats.

### Acute medication

An acute medication is represented by a `MedicationStatement`, and two `MedicationRequest` resources - one with an `intent` of `plan` and the second an `intent` of `order`.

{: .center-image }
![Acute medications diagram](images/access_structured/Acute medication representation.png)


### Repeat prescription and repeat dispense

Both repeat prescriptions and repeat dispenses are represented in a similar manner to the acute prescriptions. 

The difference is that there is now a one-to-many relationship where there can be one `MedicationRequest` with an `intent` of `plan` and it can relate to many `MedicationRequest` resources that have an intent of `order`. In this relationship, every time a repeat has been issued it will be represented by a separate `MedicationRequest` with an intent of `order`.

For repeat dispensed medication, some of the resources relating to individual issues may be post-dated if the effective period of the medication or medical device has not elapsed. However, for all `MedicationRequest` resources with an intent of `order` the `authoredOn` date **SHOULD** be the same as the related `MedicationRequest` with `intent` of `plan`.

{: .center-image }
![Repeat prescription and repeat dispensing diagram](images/access_structured/Repeat prescription and repeat dispensing.png)


### Unissued medications and medication prescribed elsewhere

Unissued medications and medications that have been prescribed elsewhere that have been added to the system by a clinician at the practice will be represented by a `MedicationStatement` and a `MedicationRequest` with an `intent` of `plan` but with no further resources.

{: .center-image }
![Unissued medications and medications prescribed elsewhere diagram](images/access_structured/Unissued medications and medications prescribed elsewhere.png)


### Using the `List` resource for medication queries
The results of a query for medication details MUST return a `List` containing references to all `MedicationStatement` resources that are returned. The `List` **SHOULD** be populated in line with the guidance on `List` resources. If the `List` is empty, then an empty `List` MUST be returned with an `emptyReason` with the value `noContent`.

### Degraded medications ###
Where degraded medication records arising from GP2GP record transfer are present in the patient record then these **SHOULD** be coded using the appropriate degrade code (`196421000000109`, Transfer-degraded medication entry) with the original medication name conveyed by `CodeableConcept.text`.

### Medication interoperability ###
Consumers of medication resources generated by other systems **SHOULD** consider the clinical safety issues arising from processing medication information recorded in different care settings and contexts, and seek clinical safety guidance where appropriate. 

Key concerns are the understandability of received medication information and appropriate actions to degrade and identify medication concepts which are not understood by the receiving system. Appropriate clinical workflows may also be required at the receiver - for example, deactivation of received medications such that they MUST be explicitly re-authorised to make them issuable.

Currently dosage and quantity information are expressed in unstructured/textual form. A system intending to consume dosage and quantity information needs to be capable of handling unstructured quantities and dosages.

### Mixtures ###
In some systems it is possible to prescribe custom formulations compounded from other medications (extemporaneous preparations). Mixtures **SHOULD** be expressed using the degrade code (`196421000000109`, Transfer-degraded medication entry) with the constituents of the mixture expressed via `CodeableConcept.text`.

### Non dm+d medications ###
In some cases, drugs may be recorded as free text or may be present in the original system’s drug dictionary, but not in dm+d. Where no dm+d code is available to describe the medication then the medication code **SHOULD** be expressed using the degrade (`196421000000109`, Transfer-degraded medication entry) with the original drug name present in `CodeableConcept.text`. 

### dm+d name versus displayed name ###
It is possible for historic/legacy medications to be displayed with a name corresponding to the name in the original system’s drug dictionary rather than the dm+d name. This name **SHOULD** be preserved via `CodeableConcept.text` when representing the medication via resources. `CodeableConcept.text` is redundant when the displayed medication name on the original system and the dm+d name is identical, and, in these cases, `CodeableConcept.text` **SHOULD** be omitted.

### Medication reviews ###
The resources required to describe diarised review activities and reminders for medication reviews are out of scope for this guidance. 

### Future-dated prescriptions ###
Medication issues may be future-dated – for example, repeat dispensed medications or a deferred acute medication that may not be needed if the condition resolves.

### Amendments ###
Where an authorisation is amended – for example, Proprietary/Generic switch, altered dates, change of quantities and so on, then the existing authorisation/plan **SHOULD** be stopped or discontinued, and an appropriate reason supplied via detectedIssue. A new authorisation **SHOULD** be created, in the form of a `MedicationStatement` and `MedicationRequest` with `intent` of `plan`, to hold the amended details. Subsequent issues of the medication **SHOULD** reference the amended authorisation rather than the previous version.

### Medication discontinuation/stopping ###

Where a medication is stopped or discontinued then the status of the authorisation **SHOULD** be changed to 'stopped' and a textual stop reason provided via `statusReason.reason`.

A `statusReason` **SHOULD NOT** be generated when an authorisation has simply expired (exceeded review date or number of issues).

### Authorisation ###

In conjunction with `MedicationStatement`, a `MedicationRequest` with an `intent` of `plan` represents an authorisation for acute, repeat, repeat dispensed medication.

### Re-authorisation ###

Where a medication is re-authorised a new authorisation **SHOULD** be generated in the form of a `MedicationStatement` and `MedicationRequest` with `intent` of `plan`. Subsequent issues of the medication **SHOULD** reference the new authorisation.

