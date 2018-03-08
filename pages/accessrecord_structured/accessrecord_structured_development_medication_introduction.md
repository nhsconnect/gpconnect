---
title: Introduction
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication_introduction.html
summary: "Introduction to populating and reading FHIR&reg; medication resources"
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
* Medication - contains details of the actual medication or medical device
* MedicationRequest - is designed to cope with planning, proposing or ordering medications
* MedicationDispense - is to represent exactly what medication was dispensed. In some cases, this can differ slightly from what was ordered/prescribed.
* MedicationAdministration - is to be used to describe when the medication is administered, how it was given and by whom.
* MedicationStatement - this is to make a statement about the medication a person has taken and can be 'basedOn' a record of an historic prescription that would be represented using one or more MedicationRequest resources.  
In GP Connect, we are interested in the medication data that is captured in GP clinical systems. This data is about the practice’s record of medication the patient has taken and whether that has been prescribed by a clinician at that practice. Therefore, in order be able to represent the information that is available in the GP systems we are interested in 3 of the above FHIR profiles: Medication, MedicationRequest and MedicationStatement. In later sections these will all be detailed at a data item level.

## Using the FHIR profiles to represent the ordering process
Most of the information in GP systems that GP Connect needs to represent is in the forms described above. That is, either an order/prescription that has been actioned by a clinician at the practice or a medication or medical device that the practice has been informed that a patient has been prescribed. To represent this using FHIR, GP suppliers MUST create a medication statement about each medication or medical device record that is contained on the GP system. Each medication statement will reflect an item that was ordered using one of the 3 business processes previously described or a medication or medical device that was prescribed or allocated elsewhere but has been recorded by a clinician at the practice. 
Where a medication statement represents an order, it will be 'basedOn' a medication request or medication requests that reflect the ordering/prescribing of that medication or medical device by the practice. 
The GP Connect profile of the FHIR medication request will be used to represent the 2 stages of the ordering process:
1. The authorisation - in conjunction with MedicationStatement, a medication request with an intent of 'plan' represents an authorisation for acute, repeat, repeat dispensed medication.
2. The issue - each time the medication is issued then it **SHOULD** be represented using a MedicationRequest with the intent element set to 'order'. There will be one 'order' for acutes but may be many for repeats.

### Acute medication representation
Acute UML diagram:

{: .center-image }
![Acute medications diagram](images/access_structured/Acute medication representation.png)

An acute medication will be represented by a medication statement that is based on a medication request with the intent of 'plan' that has a single medication request with the intent of 'order' associated to it. The order will be 'basedOn' the plan using that element to reference the medication request with intent set to 'plan'. This is illustrated in the diagram above.

### Repeat prescription and repeat dispensing
Repeat prescription and dispensing UML diagram:

{: .center-image }
![Repeat prescription and repeat dispensing diagram](images/access_structured/Repeat prescription and repeat dispensing.png)

Both repeat prescriptions and repeat prescribing are represented in a similar manner to the acute prescriptions. The difference is that there is now a one-to-many relationship where there can be one medication request with intent='Plan' and it can relate to many medication requests that have intent='order'. In this relationship, every time a repeat has been issued it will be represented by a separate medication request with intent='order'.
For repeat dispensed medication, some of the resources relating to individual issues may be post-dated if the effective period of the medication or medical device has not elapsed. However, for all MedicationRequest resources with intent='order' the authoredOn date **SHOULD** be the same as the related medication request with intent='plan'.

### Unissued medications and medication prescribed elsewhere
Unissued prescription and dispensing UML diagram:

{: .center-image }
![Unissued medications and medications prescribed elsewhere diagram](images/access_structured/Unissued medications and medications prescribed elsewhere.png)

Unissued medications and medications that have been prescribed elsewhere that have been added to the system by a clinician at the practice will be represented by a medication statement and a medication request where intent='plan' but with no further resources.

### Using the list resource for medication queries
The results of a query for medication details MUST return a list containing references to all MedicationStatement resources that are returned. The list **SHOULD** be populated in line with the guidance on list resources. If the list is empty, then an empty list MUST be returned with an emptyReason with the value noContent.
