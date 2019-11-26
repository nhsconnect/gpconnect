---
title: Diary Entry guidance
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_diaryentry_guidance.html
summary: "Guidance for populating and consuming the Diary Entry profile"
---

## What is a Diary Entry?

A diary entry is a proposal for clinical action to be undertaken at an indicative date in the future, which has not been completed or cancelled. 
The diary entry is created unscheduled, that is, it is not an appointment (but may result in an appointment being created) and resources are not directly committed to it. 
The diary entry may be a reminder for a review, a follow up to a consultation / treatment / test, a recall or treatment to be provided according to a schedule.
Diary entries may be known as Recalls within some GP Clinical Systems.

The use of diary entries may vary significantly from one practice to another and may not have any constraint in the scope as to what can be selected as the action associated to the diary entry.
Some examples of actions which may be recorded as diary entries are:

- Antipsychotic injections
- Asthma review
- Cytology Smear
- Depo Provers 
- Diabetes review
- Epilepsy review
- Mental Health review
- NHS Health checks (5years)
- Over 75 Check
- Seasonal influenza vaccination due 
- Repeat Blood tests 

Any future intention for a clinical action recorded as an Appointment or Task is out of scope.

## Medication Reviews

Medication reviews are considered to fall under the definition of a diary entry.
GP clinical systems which have a separate feature for medication reviews **MUST** include the medication reviews.
Medication reviews **MUST** be assigned the SNOMED CT code <code>314529007 | Medication review due (situation) |</code> regardless of the source system coding.
Hereafter, reference to diary entries **MUST** be assumed to include medication reviews.

## Diary Entry Status

The scope of diary entries is limited to incomplete actions only, that is complete or cancelled diary entries **MUST NOT** be included.

GP clinical systems have differing approach to allocating status to incomplete diary entries.
It is unlikely that there is sufficient consistency of use of status, so all incomplete diary entries **MUST** be given a standard status of <code>active</code>.

## Diary Entry code

GP clinical systems **MUST** populate the <code>code</code> with a valid SNOMED CT code wherever practical.

GP clinical systems **MAY** include codes for incomplete diary entries which have a standard interpretation of a completed action (for example, procedure codes).
These **MUST** be interpreted as incomplete by consumer systems.
Consumer systems **MUST** ensure these are presented to system users in such a manner that it is clear and unambiguous that the coded item represents an incomplete planned action regardless of its text description or SNOMED CT meaning.  
The consumer system **MUST** maintain the diary entry's meaning as an incomplete planned action wherever the code element may be accessed or exported, except where the action has been completed within the consumer system.

## Diary Entry planned date

GP clinical systems may hold one or more date entries for the planned date for the diary entry. 
By defintion, diary entries are not planned to occur on a specific date.
Where it is supported by the data capture for a diary entry, a period during which the diary entry should occur is preferred.
The GP clinical system provider is to determine whether its data supports the inclusion of a period for the planned date or can only meaningfully return a single planned date.

## Using the `List` resource for diary entry queries

The results of a query for diary entry details **MUST** return a `List` containing references to all `ProcedureRequest` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason` with the value `no-content-recorded`.
