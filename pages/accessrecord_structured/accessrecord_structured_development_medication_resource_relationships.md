---
title: Medication resource relationships
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication_resource_relationships.html
summary: "Representation of medication processes using FHIR&reg profiles in GP Connect"
---
## Ordering process in GP systems for medications and medical devices 

The medication or medical device ordering process in GP systems can be considered to be a two-stage process:

1. **The authorisation** - this is where the medication or medical device is initially added on to the GP systems. It represents a 'plan' that the GP intends to authorise a medication for the patient.

2. **The issue** - this is the point the plan is turned into an actual 'order' or prescription. At this point the prescription will either be printed and signed, or the order will be passed on to the Electronic Prescription Service (EPS) to send to the patient’s nominated pharmacy.

There are several clinical reasons why the process is split up in this way. Below are some examples of scenarios when it advantageous to have the separate parts:

* repeat medication added from a discharge summary ready for patient to request 
* add blood pressure (BP) drug ready for follow-up nurse clinic to issue
* issue rescue steroid/antibiotic pack and add repeats for flares 
* flu vaccinations

There are three different business processes for issuing a medication or medical device to a patient that are well established in general practice and are driven by factors such as how often a patient will require the medication/medical device, helping practices to create efficient processes for prescribing and applying the appropriate controls to drugs where appropriate. The three processes are:

 1. Acute prescribing
 2. Repeat prescribing
 3. Repeat dispensing
 
### Acute prescriptions

An acute prescription is when a medication or medical device is a one-off prescription. It is usually a course of medication/ medical device that is issued to treat a specific complaint. 

If the patient needs further medication/medical device they would need to see their doctor again for them to assess their condition and decide if another prescription is appropriate.

It is possible for clinicians where appropriate to postdate acute medications. For instance, in a situation where a patient has flu-like symptoms the clinician may provide a prescription for antibiotics dated a week in the future and advise the patient to use it if symptoms persist. This is also known as delayed prescribing.

### Repeat prescriptions

A repeat prescription enables a patient to be issued more than one prescription without it being necessary to see their doctor after each individual prescription.

The number of prescriptions is usually determined by the doctor when they make the initial order. However, it is also possible to set a review date for a medication or medical device that is prescribed in a regular manner instead of limiting the number of issues.

Typically, the duration that repeat prescriptions cover is 6 or 12 months although they are flexible and can be written for any period. 
Although the patient does not have to see their doctor to authorise each issue of the medication/medical device, they will need to have the prescription authorised by another clinician in the practice. 

### Repeat dispensing

When a medication or medical device is repeat-dispensed the patient will be able to pick up the item from the pharmacy without the need for each prescription to be issued by the GP practice.
Apart from the practice not needing to issue each prescription, repeat-dispensing works in a similar manner to repeat prescriptions where the doctor is able to determine the number of issues or the time period before needing to visit the doctor again for the prescription to be re-authorised.

### Unissued medications

It is possible in GP systems to record an intent to prescribe a medication or medical device but not to actually place an order for the medication/medical device. These will exist in GP systems without a prescription or EPS request ever being issued. 

## Medication prescribed elsewhere

In GP systems, in addition to ordering medications/medical devices and issuing them to a patient, it is also possible for clinicians to record medications/medical devices that were not issued by their GP practice. This may happen if a patient has been in hospital and informs a clinician that they were prescribed a medication or allocated a medical device during that episode of care. 

All GP systems allow for data to be entered to record details of medications/medical devices that they are informed about, but do not issue within the medication/medical device section in the system.

The main uses are to record a medication or medical device being managed by another organisation, the requirement to enable interaction checking and decision support to interact with these items.

## FHIR medication resources

FHIR has a collection of resources that are available to represent different concepts related to medications and medical devices. These resources are intended to cover the full medication lifecycle:

| Resource name       | Description | Used in GP Connect |
|---------------------|-------------------| ----------|
| [`Medication`](accessrecord_structured_development_medication.html) | The actual medication or medical device. | Yes |
| [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html) | Planning, proposing or ordering medications or medical devices. | Yes |
| [`MedicationStatement`](accessrecord_structured_development_medicationstatement.html) | Used to make a statement about the medication or medical device a person has taken and can be 'basedOn' a record of an historic prescription that would be represented using one or more MedicationRequest resources. | Yes |
| `MedicationDispense` | Represent exactly what medication/medical device was dispensed. In some cases, this can differ slightly from what was ordered/prescribed. | No |
| `MedicationAdministration` | Describe when the medication/medical device is administered, how it was given and by whom. | No |

In GP Connect, we are interested in the medication and medical device data that is captured in GP clinical systems. This data is about the practice’s record of medications/medical devices that the patient has taken and whether they has been prescribed by a clinician at that practice. 

Therefore, as shown in the table above, in order be able to represent the information that is available in the GP systems we are interested in three of the above FHIR profiles: `Medication`, `MedicationRequest` and `MedicationStatement`.

## Using the FHIR profiles to represent the ordering process

Most of the information in GP systems that GP Connect needs to represent is in the forms described above. That is, either an order/prescription that has been actioned by a clinician at the practice or a medication or medical device that the practice has been informed that a patient has been prescribed. 

To represent this using FHIR, GP suppliers **MUST** create a `MedicationStatement` about each medication or medical device record that is contained on the GP system. Each `MedicationStatement` will reflect an item that was ordered using one of the 3 business processes previously described or a medication or medical device that was prescribed or allocated elsewhere but has been recorded by a clinician at the practice. 

Where a medication statement represents an order, it will be based on one or more `MedicationRequest` resources that reflect the ordering/prescribing of that medication or medical device by the practice. 

The GP Connect profile of the `MedicationRequest` will be used to represent the 2 stages of the ordering process:

1. **The authorisation** - in conjunction with `MedicationStatement`, a `MedicationRequest` with an intent of `plan` represents an authorisation for acute, repeat, repeat dispensed medication.

2. **The issue** - each time the medication/medical device is issued then it **SHOULD** be represented using a `MedicationRequest` with the intent element set to `order`. There will be one `order` for acutes but may be many for repeats.

### Acute medication

<center>
<a href="images/access_structured/Acute_Medication.png"><img src="images/access_structured/Acute_Medication.png" alt="Acute Medication Diagram" style="max-width:60%;max-height:60%;"></a>
</center>

<div class="screen-reader-text">
This diagram is explained in the following text:
</div>

An acute medication is represented by a `MedicationStatement` and two `MedicationRequest` resources - one with an `intent` of `plan` and the second an `intent` of `order`.

### Repeat prescription and repeat dispense

<center>
<a href="images/access_structured/Repeat_Medication.png"><img src="images/access_structured/Repeat_Medication.png" alt="Repeat Medication Diagram" style="max-width:60%;max-height:60%;"></a>
</center>

<div class="screen-reader-text">
This diagram is explained in the following text:
</div>

Both repeat prescriptions and repeat dispenses are represented in a similar manner to the acute prescriptions. 

The difference is that there is now a one-to-many relationship where there can be one `MedicationRequest` with an `intent` of `plan` and it can relate to many `MedicationRequest` resources that have an intent of `order`. In this relationship, every time a repeat has been issued it will be represented by a separate `MedicationRequest` with an intent of `order`.

For repeat dispensed medication or medical device, some of the resources relating to individual issues may be post-dated if the effective period of the medication or medical device has not elapsed. However, for all `MedicationRequest` resources with an intent of `order` the `authoredOn` date **SHOULD** be the same as the related `MedicationRequest` with `intent` of `plan`.

### Unissued medications/medical devices and medication/medical devices prescribed elsewhere

<center>
<a href="images/access_structured/Unissused_Medication.png"><img src="images/access_structured/Unissused_Medication.png" alt="Unissued Medication Diagram" style="max-width:60%;max-height:60%;"></a>
</center>

<div class="screen-reader-text">
This diagram is explained in the following text:
</div>

Unissued medications/medical devices and medications/medical devices that have been prescribed elsewhere are different concepts but modelled in a similar manner. They will both have been added to the system by a clinician at the practice and will be represented by a `MedicationStatement` and a `MedicationRequest` with an `intent` of `plan`, but with no further resources. This reflects that no orders have been placed for these medications/medical devices by the GP practice. Medications/medical devices that were prescribed elsewhere will be flagged as such by populating the PrescribingAgency extension in the Medication Statement.

### Using the `List` resource for medication/medical devices queries

<center>
<a href="images/access_structured/Medication_Return.png"><img src="images/access_structured/Medication_Return.png" alt="Unissued Medication Diagram" style="max-width:100%;max-height:100%;"></a>
</center>

<div class="screen-reader-text">
This diagram is explained in the following text:
</div>

The results of a query for medication/medical devices details **MUST** return a `List` containing references to all `MedicationStatement` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason` with the value `noContent`.


