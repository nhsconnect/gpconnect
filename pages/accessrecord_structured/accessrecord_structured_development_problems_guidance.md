---
title: Problems guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_problems_guidance.html
summary: "Guidance for populating and consuming the ProblemHeader resource"
---

## What is a Problem ##
Problem is a concept supported by all the GP Clinical Systems that allows a clinician to identify / highlight specific clinical items in the clinical record as of particular important to the care and treatment of the patient. 

Any clinical item can be identified as a problem though the method of doing this can vary greatly between GP clinical systems.

Examples of possible problems:
*	Anxiety with Depression		
*	Swollen legs		
*	Hypertension		
*	Blood pressure recorded by patient at home 		
*	Atrial fibrillation		
*	Knee pain		
*	Upper respiratory tract infection		
*	Lives alone		

As well as highlighting an item of particular relevant to the patient’s care, the problem records also links that item to all the other information in the patient record that describes what has happened in regards to that item.


For example, the problems record highlights that the patient has hypertension. It also shows how the hypertension was identified, what discussion have taken place with the patient about their hypertension and what treatments and medication the patient is on the help manage their hypertension.


To support this, problems are linked to:

* every consultation where the problem has been discussed or information about the problem has been recorded. 
* every clinical item in the patient record that a clinician has identified as relevant to the problem (for example test results, medication).
* every other problem in the patient record that a clinician has identified as relevant to the problem.

## Problem relationships
Problem records are linked to consultations, clinical items and other problems. Different provider systems manage links to problems in different ways. To reduce the impact of this to consumers, the provider system will transform their problem linkages into a common model for export.

Each Problem record is linked to:
*	All consultations where the problem was discussed or information about the problem was recorded
    *	Consultations that are directly linked to the problem in the provider system; and
    *	Consultations that created/updated a clinical item that has been linked to the problem 
*	All clinical items in the patient record that give further information about the problem.
    *	Clinical items that are directly linked to the problem in the provider system; and
    *	Clinical items that are within a consultation topic that is linked to the problem
*	Other problems that give further information about the problem
    *	Problems that are directly linked to the problem in the provider system

<img src="images/access_structured/Problem_Linkages.png" alt="Problem Linkages" style="max-width:100%;max-height:100%;">

## Clinical Item References

When a clinical item is linked to the Problem a reference to its FHIR resource is held in either extension[actualProblem] or extension[relatedClinicalContent].


When linking to the clinical item that is held in a single FHIR resource the reference will be to that resource. When linking to the clinical item that is held across multiple resources (for example Medication and Medical Device) the reference must be to the FHIR resource specified below. 
* For a Medication or Medical Device prescription plan - reference the MedicationRequest (intent = plan) resource
* For a Medication or Medical Device prescription issue - reference the MedicationRequest (intent = order) resource
* For an Allergy – reference the Immunization resource 
* For Uncategorised Data – reference the Observation – Uncategorised resource


## Problems linking to unsupported clinical items

Depending on the GP Connect version supported by the provider system it can be possible for the problem to link to a clinical item that the provider system is not yet able to export with GP Connect. For example, if the problem contains a link to a referral record but the provider system does not yet support exporting referrals.


Where a provider system is not able to export a linked clinical item it will create a actualproblem or relatedclinicalcontent entry with the:

* Reference.Identifier set to null; and
* Reference.Display set to “Clinical item not supported by the provider system.”

## Problem Guidance

### Problem structure and relationships in GP systems

### Modelling problems using FHIR resources

### Active and Inactive problems

### Problem severity

### Use of terminology and the actualProblem extension

### Relationships to other problems

### Other related data in the GP record

### Placeholders for uncurated/implemented content/docs

