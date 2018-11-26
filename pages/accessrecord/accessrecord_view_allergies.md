---
title: Allergies and adverse reactions
keywords: getcarerecord, view, section, allergies
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_allergies.html
summary: "Allergies HTML view"
---

<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ALL | Allergies and Adverse Reactions| Yes | Yes<sup>1</sup> | Yes<sup>2</sup> | Yes |

<sup>1</sup> EMIS have indicated that they are including all allergies & sensitivities in the 'Current Allergies .....' section.

<sup>2</sup> Vision have indicated they don't record end dates for allergies & sensitivities. Hence, no History view is possible.


## Clinical narrative ##

A reaction to a substance not intended to occur. Allergies are caused by hypersensitivity of the immune system to an external agent

## Purpose ##

The purpose of this section is to provide the clinician with a list of patient allergies to enable safe prescribing and treatment recommendations for a patient.

## Sections and subsections ##

Contains two sections:

 - [Current Allergies and Adverse Reactions](accessrecord_view_allergies.html#current-allergies-and-adverse-reactions)
 - [Historical Allergies and Adverse Reactions](accessrecord_view_allergies.html#historical-allergies-and-adverse-reactions)

### Date filter ###

Date filters are not supported for this section all relevant records shall be returned for the Current and Historic Allergies and Adverse Reactions.
 
 
### Section content banner ###

Provider messages describing at a summary level how they have populated this section can be found [here](accessrecord_provider_variance.html#allergies-and-adverse-reactions).


## Current Allergies and Adverse Reactions ##

### Clinical narrative ###

A reaction to a substance not intended to occur. Allergies are caused by hypersensitivity of the immune system to an external agent

### Purpose ###

The purpose of this section is to provide the clinician with a list of current allergies to enable safe prescribing and treatment recommendations for a patient.

### Subsection content banner ###

Provider messages describing at a summary level how they have populated this subsection can be found [here](accessrecord_provider_variance.html#current-allergies-and-adverse-reactions-subsection):

### Table construction requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **MUST** be "Current Allergies and Adverse Reactions".
- Table columns **MUST** be ordered left-to-right (1..N).
- Table content **MUST NOT** be truncated.



### Table columns ###

Providers must return all the columns as described in the table below, ordered by `Start Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date` <i class="fa fa-sort-desc" aria-hidden="true">| The start date of the allergy or adverse reaction | `dd-Mmm-yyyy` |
| <center>2</center> | `Details` | Longer human readable details for the allergy or adverse reaction | `free-text` |




## Historical Allergies and Adverse Reactions ##

### Clinical narrative ###

A reaction to a substance not intended to occur. Allergies are caused by hypersensitivity of the immune system to an external agent.

### Purpose ###

The purpose of this section is to provide the clinician with a list of historical allergies to enable safe prescribing and treatment recommendations for a patient.


### Subsection content banner ###

Provider messages describing at a summary level how they have populated this subsection can be found [here](accessrecord_provider_variance.html#historical-allergies-and-adverse-reactions-subsection):

### Table construction requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **MUST** be "Historical Allergies and Adverse Reactions".
- Table columns **MUST** be ordered left-to-right (1..N).
- Table content **MUST NOT** be truncated.


### Table columns ###

Providers must return all the columns as described in the table below, ordered by `End Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date` | The start date of the allergy or adverse reaction | `dd-Mmm-yyyy` |
| <center>2</center> | `End Date` <i class="fa fa-sort-desc" aria-hidden="true"> | The end date of the allergy or adverse reaction | `dd-Mmm-yyyy` |
| <center>3</center> | `Details` | Longer human readable details for the allergy or adverse reaction | `free-text` |


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/allergies.html %}

