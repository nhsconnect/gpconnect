---
title: Medication
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication_introduction.html
summary: "Guidance for populating and reading the Medication resource"
---

## Introduction ##

## The medication ordering process ##
The medication ordering process in GP systems can be considered to be a 2 stage process.
1. The authorisation - this is where the medication is initially added on to the GP systems. It provides a 'plan' that the GP intends to give a medication to the patient.
2. The issue - this is the point the plan is turned into and actual 'order' or prescription. At this point the prescription will either be printed and signed or the order will be passed on to the Electronic Prescription service to send to the patients nominated pharmacy.

There are a number of clinical reasons why the process is split up in this way. Below are some examples of scenarios when it advantagous to have the separarte parts,
* Repeat medication added from a discharge summary ready for patient to request 
* Add BP drug ready for follow-up nurse clinic to issue
* Issue rescue steroid/antibiotic pack and add repeats for flares 
* Flu vaccinations

There are 3 different business processes for issuing a medication to a patient that are well established in general practice and are driven by factors such as how often a patient will require the medication, helping practices to create effiecent processes for prescribing and applying the appropriate controls to drugs where appropriate. The 3 processes are,
 1. Acute Prescribing
 2. Repeat Prescribing
 3. Repeat Dispensing
 
### Acute prescriptions ###
An acute prescription is when a medication is a one off prescription. It is usually a course of medication that is issued to treat a specific complaint. 
If the patient needs further medication they would need to see their doctor again in order for them to assess their condition and decide if another prescription is appropriate.

### Repeat prescriptions ###
A repeat prescription enables a patient to be issued a number of prescriptions without it being necessary to see their doctor after each individual prescription. The number of prescriptions is usual determined by the doctor when they make the initial order, however it is also possible to set a review date for a medication that is prescribed in a regular manner instead of limiting the number of issues. Typically the durations that repeat prescriptions cover is 6 or 12 months although they are flexible and can be written for any period. 
Although the patient does not have to see their doctor in order to authorise each issue of the medication they will need to have the prescription authorised by someone else in the practice. 

### Repeat dispensing ###
When a medication is repeat dispensed the patient will be able to pick up their medication from the pharmacy without the need for each prescription to be issued by the GP practice.
Apart from the practice not needing to issue each prescription repeat dispensing works in a similar manner to repeat prescriptions where the doctor is able to determine the number of issues or the time period before needing to visit the doctor again for the prescription to be re-authorised.

## Medication prescibed elsewhere ##
In GP systems in addition to ordering medications and issuing them to a patient it is also possible for clinicians s to record medication that was not issued by their GP practice. This may happen if a patient has been in hospital and informs a clinician that they were prescribed a medication during that episode of care. All GP systems allow for data to be entered to record details of medications that they are informed about but do not issue within the medication section in the system.

