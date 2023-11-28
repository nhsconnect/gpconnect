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

* Anxiety with depression
* Swollen legs
* Hypertension
* Blood pressure recorded by patient at home
* Atrial fibrillation
* Knee pain
* Upper respiratory tract infection
* Lives alone

As well as highlighting an item, the problem record also links that item to all the other information in the patient record that describes what has happened in regard to that item.
For example, the problems record highlights that the patient has hypertension.
It also shows how the hypertension was identified, what discussions have taken place with the patient about their hypertension and what treatments and medication the patient is on to help manage their hypertension.

To support this, problems are linked to:

* every consultation where the problem has been discussed or information about the problem has been recorded
* every clinical item in the patient record that a clinician has identified as relevant to the problem (for example, test results, medication)
* every other problem in the patient record that a clinician has identified as relevant to the problem

## Problem relationships

Problem records are linked to consultations, clinical items and other problems. Different provider systems manage links to problems in different ways. To reduce the impact of this to consumers, the provider system will transform their problem linkages into a common model for export.

{% include note.html content="The diagrams are illustrative to support the specification text. There may be some simplifications or omissions, for instance not all possible linkages to the resources for investigations are shown." %}

Each problem record is linked to:

* all consultations where the problem was discussed or information about the problem was recorded
  * consultations that are directly linked to the problem in the provider system; and
  * consultations that created/updated a clinical item that has been linked to the problem
* all clinical items in the patient record that the recording clinician identified as giving further information about the problem
  * clinical items that are directly linked to the problem in the provider system; and
  * clinical items that are within a consultation topic that is linked to the problem
* other problems that the recording clinician identified as giving further information about the problem
  * problems that are directly linked to the problem in the provider system

<a href="images/access_structured/Problem_Relationships_1_5_v5.png"><img src="images/access_structured/Problem_Relationships_1_5_v5.png" alt="Problem Relationships" style="max-width:100%;max-height:100%;"></a>

## Clinical item references

When a clinical item is linked to the problem, a reference to its FHIR&reg; resource is held in either extension[actualProblem] or extension[relatedClinicalContent].

When linking to the clinical item that is held in a single FHIR resource the reference will be to that resource. When linking to the clinical item that is held across multiple resources (for example, Medication and Medical Device) the reference must be to the FHIR resource specified below.

* for a Medication or Medical Device prescription plan - reference the `MedicationRequest` (intent = plan) profile
* for a Medication or Medical Device prescription issue - reference the `MedicationRequest` (intent = order) profile
* for an Allergy – reference the `Allergy` profile
* for a Consultation - reference the `Encounters` profile
* for an Immunisation – reference the `Immunization` profile
* for Uncategorised Data – reference the `Observation` – Uncategorised profile
* for a Referral - reference the `ReferralRequest` profile
* for a Document - reference the `DocumentReference` profile
* for an Investigation - reference the `DiagnosticReport` profile - if any item related to a diagnostic report is flagged as a problem the diagnosticReport **MUST** be linked to the problem as a related clinical item.
* for a Diary Entry - reference the `ProcedureRequest` profile

## Problems linking to problems

It is possible within GP clinical systems to link problems together. This is done by a clinician when they consider the problems to have a clinical impact or give context to each other.

The methods and terminology used to link problems varies a great deal between clinical systems and are not compatible with each other. For example, in one GP clinical system grouping two problems merges them into a single problem while in another it keeps them as two separate problems that are linked together.

To resolve this, GP Connect will only show the logical linkage between problems (whether the linked problem is a parent, child or sibling) without reflecting the terminology of the provider system.

Problem linkages may be impacted by filtering. See the guidance in the [retrieve a patients structured record page.](accessrecord_structured_development_retrieve_patient_record.html)

## Problems linking to out of scope clinical items

The following items may be recorded in defined clinical areas which are supported by the provider but the clinical items are out of scope in this version of the specification

* Complete diary entries
* Test requests not part of investigation reports

If these clinical items are linked to a problem, they will not be referenced in the provider response.
An encounter reference **MUST** be included as a reference from the problem where applicable, as defined above, regardless of the absence of a reference to the clinical item.

## Problems linking to unsupported clinical items

Depending on the GP Connect version supported by the provider system, it can be possible for the problem to link to a clinical item that the provider system is not yet able to export with GP Connect. For example, if the problem contains a link to a referral record but the provider system does not yet support exporting referrals.

Where a provider system is not able to export a linked clinical item, it will create a reference entry with the:

* `Condition.extension[relatedClinicalContent].valueReference.Display` set to “[Clinical area] items are not supported by the provider system.”

   Where [Clinical area] identifies the type of the clinical item that is not supported.

The example below shows references to two items, one for an observation and another for referrals that aren't supported by the provider system:

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

* The Problem will be included in the response as normal
* The confidential item(s) will NOT be included in the response
* There will be NO reference to the confidential item(s) in the `ProblemHeader (Condition)` profile.
* The Confidential Items warning message will be included in the `List` on the relevant type of type data that was omitted. For example if a piece of uncategorised data was excluded as it was confidential then the warning code would be in the list of uncategorised data that was returned as part of the query.

In effect, there will be a warning message that items were excluded from the response due to confidentiality but there will be no indication from which Problems(s) they were removed.

## Using Problem search parameters

The request for problems supports searching via a part parameter for the problem's clinical status.
Guidance is given in other sections of this specification as to how the provider will populate the response with identifying lists and related clinical content.
This section describes consequences of those requirements specific to problems returned.

If the consumer request specifies a part parameter for status, the provider **MUST** return all problems with matching clinical status.

In addition to the matching problems, the provider **MUST** return the resource items referenced by the problem header as the actual problem, related problems or related clinical content as described on the [Linkages](accessrecord_structured_development_linkages) and the [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record) pages.
The provider **MUST** include the related problem header resource regardless of whether the related problem matches the specified status, that is if the part parameter requests only active problems, where an active problem is directly related to an inactive one, then the inactive problem header will be returned.
The provider **MUST** include a reference in the problems secondary list to the related problem header which does not match the specified status as described in [Using lists to return data](accessrecord_structured_development_lists_for_message_structure).
The provider **MUST NOT** include any resources referenced by the problem header resources in the secondary list which do not match the specified status.
The provider **MAY** include problems in the 'problems linked to problems' secondary list which both meet the search criteria and are linked problems.
The provider **MUST NOT** include any problem reference in the primary problem list which are returned only as related problems and do not directly meet the problem search criteria.

A consumer can therefore receive problems which do not meet the specified status, but the consumer can identify such problem header resources as they will be referenced in the 'problems related to problems' list but are not referenced by the primary problem’s list.

## Using the `List` resource for problem queries

The results of a query for problem details **MUST** return a `List` containing references to all `ProblemHeader (Condition)` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason.code` with the value `no-content-recorded`. In this case, `List.note` **MUST** be populated with the text 'Information not available'.
