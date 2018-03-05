---
title: Medication_Introduction
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication_introduction.html
summary: "Introduction to populating and reading the Medication resource"
---

## Introduction ##

## The ordering process in GP systems for medications and medical devices 
The medication  or medical device ordering process in GP systems can be considered to be a 2 stage process.
1. The authorisation - this is where the medication or medical device is initially added on to the GP systems. It represents a 'plan' that the GP intends to authorise a medication for the patient.
2. The issue - this is the point the plan is turned into and actual 'order' or prescription. At this point the prescription will either be printed and signed or the order will be passed on to the Electronic Prescription service to send to the patients nominated pharmacy.

There are a number of clinical reasons why the process is split up in this way. Below are some examples of scenarios when it advantageous to have the separate parts,
* Repeat medication added from a discharge summary ready for patient to request 
* Add BP drug ready for follow-up nurse clinic to issue
* Issue rescue steroid/antibiotic pack and add repeats for flares 
* Flu vaccinations

There are 3 different business processes for issuing a medication to a patient that are well established in general practice and are driven by factors such as how often a patient will require the medication, helping practices to create efficient processes for prescribing and applying the appropriate controls to drugs where appropriate. The 3 processes are,
 1. Acute Prescribing
 2. Repeat Prescribing
 3. Repeat Dispensing
 
### Acute prescriptions ###
An acute prescription is when a medication or medical device is a one off prescription. It is usually a course of medication that is issued to treat a specific complaint. 
If the patient needs further medication they would need to see their doctor again in order for them to assess their condition and decide if another prescription is appropriate.

### Repeat prescriptions ###
A repeat prescription enables a patient to be issued a number of prescriptions without it being necessary to see their doctor after each individual prescription. The number of prescriptions is usual determined by the doctor when they make the initial order, however it is also possible to set a review date for a medication or medical device that is prescribed in a regular manner instead of limiting the number of issues. Typically the duration that repeat prescriptions cover is 6 or 12 months although they are flexible and can be written for any period. 
Although the patient does not have to see their doctor in order to authorise each issue of the medication they will need to have the prescription authorised by another clinician in the practice. 

### Repeat dispensing ###
When a medication or medical device is repeat dispensed the patient will be able to pick up the item from the pharmacy without the need for each prescription to be issued by the GP practice.
Apart from the practice not needing to issue each prescription repeat dispensing works in a similar manner to repeat prescriptions where the doctor is able to determine the number of issues or the time period before needing to visit the doctor again for the prescription to be re-authorised.


## Medication prescibed elsewhere ##
In GP systems in addition to ordering medications and issuing them to a patient it is also possible for clinicians to record medication that was not issued by their GP practice. This may happen if a patient has been in hospital and informs a clinician that they were prescribed a medication or allocated a medical device during that episode of care. All GP systems allow for data to be entered to record details of medications that they are informed about but do not issue within the medication section in the system.
The main use is to record a medication or medical device being managed by another organisation, the requirement to enable interaction checking and decision support to interact with these items.

## FHIR medication profiles 
FHIR has a number of resources that are available to represent different concepts related to medications. These resources that are intended to cover the full medication lifecycle.
* Medication - contains details of the actual medication or medical device
* Medication Request - is designed to cope with planning, proposing or ordering medications
* Medication Dispense - is to represent exactly what medication was dispensed. I n some cases this can differ slightly from what was ordered/prescribed.
* Medication Administration - is to be used to describe when the medication is administered, how it was given and by whom.
* Medication Statement - This is to make a statement about the medication a person has taken and can be 'basedOn' a record of an historic prescription that would be represented using one or more MedicationRequest resources.  
In GP Connect we are interested in the medication data that is captured in GP clinical systems. This data is about the practices record of medication the patient has taken and whether that has been prescribed by a clinician at that practice. Therefore in order be able to represent the information that is available in the GP systems we are interested in 3 of the above FHIR profiles Medication, Medication Request and Medication Statement. In later sections these will all be detailed at a data item level.

## Using the FHIR profiles to represent the ordering process
The majority of the information in GP systems that GP Connect needs to represent is in the forms described above. That is either an order/prescription that has been actioned by a clinician at the practice or a medication or medical device that the practice has been informed that a patient has been prescribed. To represent this using FHIR GP suppliers must create  or a Medication Statement about each medication or medical device record that is contained on the GP system. Each Medication Statement will reflect an item that was ordered using one of the 3 business processes previously described or a medication or medical device that was prescribed or allocated elsewhere but has been recorded by a clinician at the practice. 
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

Both repeat prescriptions and repeat prescribing are represented in a similar manner to the acute prescriptions. The difference is that there is now a one to many relationship where there can be one Medication Request with intent='Plan' and it can relate to many Medication Requests that have intent='order'. In this relationship for every time a repeat has been issued it will be represented by a separate Medication Request with intent='order'.
For repeat dispensed medication some of the resources relating to individual issues may be post dated if the effective period of the medication or medical device has not elapsed. However for all MedicationRequest resources with intent='order' the authoredOn date should be the same as the related MedicationRequest with intent='plan'.

### Unissued medications and medication prescribed elsewhere ###
Unissued prescription and dispensing UML diagram:

{: .center-image }
![Unissued medications and medications prescribed elsewhere diagram](images/access_structured/Unissued medications and medications prescribed elsewhere.png)

Unissued medications and medications that have been prescribed elsewhere that have been added to the system by a clinician at the practice will be represented by a Medication Statement and a Medication Request where intent='plan' but with no further resources.

### Using the list resource for medication queries
The results of a query for medication details must return a list containing references to all MedicationStaement resources that are returned. The list should be populated in line with the guidance on list resources. If the list is empty then an empty list must be returned with an emptyReason of noContent.

