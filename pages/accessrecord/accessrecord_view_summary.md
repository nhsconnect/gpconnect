---
title: Summary
keywords: getcarerecord, view, section, summary
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_summary.html
summary: "Summary HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |
| SUM | Summary | Yes | Yes | Yes | Yes |


## Clinical narrative ##

Clinicians work in busy and time-pressured environments. They need access to high-quality, relevant and wherever possible consistent information to support safe, effective and efficient assessment of their patients.

Timely sharing of clinical information is key to the delivery and improvement of safe and effective clinical care.

## Purpose ##

The purpose of this section is to provide a summarised view of the pertinent clinical information regarding a patient within a single screen. This allows a clinician to efficiently peruse key information from the patient’s clinical record and supports clinical decision making.

## Sections ##

There is only a single main section for the summary section with 5 subsections:

 - [Last 3 Encounters](accessrecord_view_summary.html#last-3-encounters)
 - [Active Problems and Issues](accessrecord_view_summary.html#active-problems-and-issues)
 - [Current Allergies and Adverse Reactions](accessrecord_view_summary.html#current-allergies-and-adverse-reactions)
 - [Recent Acute Medication](accessrecord_view_summary.html#current-medication-issues)
 - [Current Repeat Medications](accessrecord_view_summary.html#current-repeat-medications)

 
## Date filter ##

Date filters are not supported for this section. All relevant records shall be returned.

## Section banner content ##

Provider's message describing at a summary level how they have populated this section.

## Sections detail ##

### Last 3 Encounters ###

This section is an exact replica of the Encounters section with a filter applied to show the three most recent encounters. Further details about this section can be found there including any date range filtering and business rules.

{% include callout.html content="Please see HTML guidance in the [Encounters](accessrecord_view_encounters.html) section. " type="primary" %} 

{% include custominfocallout.html content="**Important:** the section title for Encounters on the Summary view should explicitly state 'Last 3 encounters'.  The columns and content should be as per the HTML guidance for encounters with the exception of only 3 rows in the table." type="warning" %}

### Active Problems and Issues ###

This section is an exact replica of the Active Problems and Issues subsection, which is the first subsection within the Problems and issues section. Further details about this subsection can be found there, including any date range filtering and business rules.

{% include callout.html content="Please see HTML guidance in the [Active problems and issues](accessrecord_view_problems.html#active-problems-and-issues) section." type="primary" %} 

### Current Allergies and Adverse Reactions ###

This section is an exact replica of the Current Allergies and Adverse Reactions subsection, which is the first subsection within the Allergies and adverse reactions section. Further details about this subsection can be found there, including any business rules.

{% include callout.html content="Please see HTML guidance in the [Current allergies and adverse reactions](accessrecord_view_allergies.html#current-allergies-and-adverse-reactions) section." type="primary" %} 

### Recent Acute Medication ###

This section is an exact replica of the Recent Acute Medication issues subsection, which is the first subsection within the Medications section. Further details about this subsection can be found there, including any business rules.

{% include callout.html content="Please see HTML guidance in the [Recent acute medication](accessrecord_view_medications.html#recent-acute-medication) section." type="primary" %} 

### Current Repeat Medication ###

This section is an exact replica of the Current Repeat Medication subsection, which is the second subsection within the Medications section. Further details about this subsection can be found there, including any business rules.

{% include callout.html content="Please see HTML guidance in the [Current repeat medication](accessrecord_view_medications.html#current-repeat-medication) section." type="primary" %} 
