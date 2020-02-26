---
title: Diary entry guidance
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_diaryentry_guidance.html
summary: "Guidance for populating and consuming the Diary Entry profile"
---

## What is a diary entry?

A diary entry is primarily a proposal for clinical action to be undertaken at an indicative date in the future, which has not been completed or cancelled. 
The diary entry is dated but unscheduled - that is, it is not an appointment (but may result in an appointment being created) and resources are not directly committed to it. 
The diary entry may be a reminder for a review, a follow up to a consultation / treatment / test, a recall or treatment to be provided according to a schedule.
Diary entries may be known as 'recalls' within some GP clinical systems.

The use of diary entries may vary significantly from one practice to another and may not have any constraint in the scope as to what can be selected as the action associated to the diary entry.
Some examples of actions which may be recorded as diary entries are:

- Antipsychotic injections
- Asthma review
- Cytology Smear
- Depo Provera 
- Diabetes review
- Epilepsy review
- Mental Health review
- NHS Health checks (5years)
- Over 75 Check
- Seasonal influenza vaccination due 
- Repeat Blood tests 

Any future intention for a clinical action recorded as an Appointment, Warning / Alert or Task is out of scope.

## Medication reviews

Medication reviews are considered to fall under the definition of a diary entry.
GP clinical systems which have a separate feature for medication reviews **MUST** include the medication reviews.
These medication reviews **MUST** be assigned the SNOMED CT code <code>314529007 | Medication review due (situation) |</code> or one of its child codes as most appropriate.
Hereafter, reference to diary entries **MUST** be assumed to include medication reviews.

Consumers should be aware that medication reviews may occur in additional to the main, planned medication review recorded in the GP clinical system and shared via this resource.

## Diary entry status

The scope of diary entries is limited to incomplete actions only - that is, complete or cancelled diary entries **MUST NOT** be included.

GP clinical systems have differing approach to allocating status to incomplete diary entries.
It is unlikely that there is sufficient consistency of use of status, so all incomplete diary entries **MUST** be given a standard status of <code>active</code>.

## Diary entry code

GP clinical systems **MUST** populate the <code>code</code> with a valid SNOMED CT code wherever practical.

GP clinical systems **MAY** include codes for incomplete diary entries which have a standard interpretation of a completed action (for example, procedure codes).
These **MUST** be interpreted as incomplete by consumer systems.
Consumer systems **MUST** ensure these are presented to system users in such a manner that it is clear and unambiguous that the coded item represents an incomplete planned action regardless of its text description or SNOMED CT meaning.  
The consumer system **MUST** maintain the diary entry's meaning as an incomplete planned action wherever the code element may be accessed or exported.

## Diary entry planned date

The planned date may be a single date or a date range according to the source GP clinical system and local recording practice. 
The GP clinical system provider is to determine whether its data supports the inclusion of a period for the planned date or can only meaningfully return a single planned date.
The planned date may represent an earliest date, latest date, indicative date or a combination but this may vary by record / use and the resource will not provide distinctions in this respect.

## Dairy entry authoredOn

The diary entry <code>authoredOn</code> is the date the diary entry was captured on the GP clinical system.
There may also be a consultation referenced which may have occurred on a different date.
Consumer systems which display an originating date for the diary entry (that is when the need for the action was determined) should give the consultation date primacy.

## Using the `List` resource for diary entry queries

The results of a query for diary entry details **MUST** return a `List` containing references to all `ProcedureRequest` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason` with the value `no-content-recorded`.
