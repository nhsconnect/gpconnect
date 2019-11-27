---
title: Problem guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_problems_guidance.html
summary: "Guidance for populating and consuming the ProblemHeader resource"
---

## What is a problem? ##
'Problem' is a concept supported by all the GP clinical systems that allows a clinician to identify/highlight specific clinical items in the medical record to describe the status of the patient's health.

Any clinical item can be identified as a problem, though the method of doing this varies between GP clinical systems.

Examples of possible problems:
*	Anxiety with depression		
*	Swollen legs		
*	Hypertension		
*	Blood pressure recorded by patient at home 		
*	Atrial fibrillation		
*	Knee pain		
*	Upper respiratory tract infection		
*	Lives alone		

As well as highlighting an item, the problem record also links that item to all the other information in the patient record that describes what has happened in regard to that item.

For example, the problems record highlights that the patient has hypertension. It also shows how the hypertension was identified, what discussions have taken place with the patient about their hypertension and what treatments and medication the patient is on to help manage their hypertension.

To support this, problems are linked to:

* every consultation where the problem has been discussed or information about the problem has been recorded
* every clinical item in the patient record that a clinician has identified as relevant to the problem (for example, test results, medication)
* every other problem in the patient record that a clinician has identified as relevant to the problem

## Problem relationships
Problem records are linked to consultations, clinical items and other problems. Different provider systems manage links to problems in different ways. To reduce the impact of this to consumers, the provider system will transform their problem linkages into a common model for export.

Each problem record is linked to:
*	all consultations where the problem was discussed or information about the problem was recorded
    *	consultations that are directly linked to the problem in the provider system; and
    *	consultations that created/updated a clinical item that has been linked to the problem
*	all clinical items in the patient record that the recording clinician identified as giving further information about the problem
    *	clinical items that are directly linked to the problem in the provider system; and
    *	clinical items that are within a consultation topic that is linked to the problem
*	other problems that the recording clinician identified as giving further information about the problem
    *	problems that are directly linked to the problem in the provider system

<a href="images/access_structured/Problem_Relationships.png"><img src="images/access_structured/Problem_Relationships.png" alt="Problem Relationships" style="max-width:100%;max-height:100%;"></a>

## Clinical item references

When a clinical item is linked to the problem, a reference to its FHIR&reg; resource is held in either extension[actualProblem] or extension[relatedClinicalContent].

When linking to the clinical item that is held in a single FHIR resource the reference will be to that resource. When linking to the clinical item that is held across multiple resources (for example, Medication and Medical Device) the reference must be to the FHIR resource specified below.
* for a Medication or Medical Device prescription plan - reference the `MedicationRequest` (intent = plan) profile
* for a Medication or Medical Device prescription issue - reference the `MedicationRequest` (intent = order) profile
* for an Allergy – reference the `Allergy` profile
* for an Immunisation – reference the `Immunization` profile
* for Uncategorised Data – reference the `Observation` – Uncategorised profile
* for a Referral - reference the `ReferralRequest` profile
* for a Document - reference the `DocumentReference` profile
* for an Investigation - reference the `DiagnosticReport` profile
* for a Diary Entry - reference the `ProcedureRequest` profile

## Problems linking to problems

It is possible within GP clinical systems to link problems together. This is done by a clinician when they consider the problems to have a clinical impact or give context to each other.

The methods and terminology used to link problems varies a great deal between clinical systems and are not compatible with each other. For example, in one GP clinical system grouping two problems merges them into a single problem while in another it keeps them as two separate problems that are linked together.

To resolve this, GP Connect will only show the logical linkage between problems (whether the linked problem is a parent, child or sibling) without reflecting the terminology of the provider system.

## Problems linking to unsupported clinical items

Depending on the GP Connect version supported by the provider system, it can be possible for the problem to link to a clinical item that the provider system is not yet able to export with GP Connect. For example, if the problem contains a link to a referral record but the provider system does not yet support exporting referrals.

Where a provider system is not able to export a linked clinical item, it will create a reference entry with the:

* `Condition.extension[relatedClinicalContent.valueReference.reference.Display` set to “[Clinical area] items are not supported by the provider system.”

   Where [Clinical area] identifies the type of the clinical item that is not supported.

The example below shows references to two items, one for an observation and another for referrals that aren’t supported by the provider system:
```json

"extension": [
   {
     "url": "http://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-CareConnect-RelatedClinicalContent-1",
     "valueReference": {
       "reference": "Observation/6734572634"
     }
   },
   {
     "url": "http://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-CareConnect-RelatedClinicalContent-1",
     "valueReference": {
       "display": "Referral items are not supported by the provider system"
     }
   }
]
```


## Problems containing confidential items

Where a Problem is marked as confidential it will (as per the structured requirements on confidentially) not be included in returned data and the Confidential Items warning message will be included in the `List` containing the query response.

Where a Problem is not marked as confidential but includes items that are marked as confidential or are considered sensitive, the following information is returned:
* the Problem will be included in the response as normal
* the confidential item(s) will NOT be included in the response
* there will be NO reference to the confidential item(s) in the `ProblemHeader (Condition)` profile
* the Confidential Items warning message will be included in the `List` containing the query response

In effect, there will be a warning message that items were excluded from the response due to confidentiality but there will be no indication from which Problems(s) they were removed.

## Using the `List` resource for problem queries

The results of a query for problem details **MUST** return a `List` containing references to all `ProblemHeader (Condition)` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason` with the value `noContent`.
