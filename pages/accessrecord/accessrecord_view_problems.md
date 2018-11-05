---
title: Problems and issues
keywords: getcarerecord, view, section, problems
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_problems.html
summary: "Problems HTML view"
---

<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| PRB | Problems and Issues | Yes | Yes | Yes | Yes |


## Clinical narrative ##

Any issue that is significant to a patient that impacts their health or wellbeing. It includes disease, surgery and social issues such as bereavement or unemployment.

## Purpose ##

The purpose of this section is to provide information about a patient’s significant problems and issues which will inform, or may have previously informed the clinical decision-making process.


## Sections and subsections ##

Contains two sections:

 - [Active Problems and Issues](accessrecord_view_problems.html#active-problems-and-issues)
 - [Inactive Problems and Issues](accessrecord_view_problems.html#inactive-problems-and-issues)

### Date filter ###

A date filter is only applicable for the [Inactive Problems and Issues](accessrecord_view_problems.html#inactive-problems-and-issues) subsection in the Problems and Issues section. Provider messages for a date filter can be found [here](accessrecord_provider_variance.html#date-banner-message).

### Section content banner ###

Provider messages describing at a summary level how they have populated this section can be found [here](accessrecord_provider_variance.html#problems-and-issues).


## Active problems and issues ##

### Clinical narrative ###

Any active issue that is significant to a patient and affects their health or wellbeing. It includes disease, surgery and social issues such as bereavement or unemployment.

### Purpose ###

The purpose of this section is to provide information about a patient’s current and potentially relevant significant problems and issues which will inform the clinical decision-making process.

### Subsection content banner ###

Provider messages describing at a summary level how they have populated this subsection can be found [here](accessrecord_provider_variance.html#active-problems-and-issues-subsection):


### Table construction requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **MUST** be "Active Problems and Issues".
- Table columns **MUST** be ordered left-to-right (1..N).
- Table content **MUST NOT** be truncated.


### Table columns ###

Providers must return all the columns as described in the table below, ordered by `Start Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date`  <i class="fa fa-sort-desc" aria-hidden="true"> | The start date of the problem | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry`| A short human readable title for the problem | `free-text` |
| <center>3</center> | `Significance`| The significance of the problem (i.e. Major or Minor) | `free-text` |
| <center>4</center> | `Details` | Longer human readable details for the problem | `free-text` |





## Inactive problems and issues ##

### Clinical narrative ###

Any inactive issue that was significant to a patient and affected their health or wellbeing. It includes disease, surgery and social issues such as bereavement or unemployment.

### Purpose ###

The purpose of this section is to provide information about a patient’s previous significant problems and issues which may have informed the clinical decision-making process.

### Subsection content banner ###

Provider messages describing at a summary level how they have populated this subsection can be found [here](accessrecord_provider_variance.html#inactive-problems-and-issues-subsection):


### Table construction requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **MUST** be "Inactive Problems and Issues".
- Table columns **MUST** be ordered left-to-right (1..N).
- Table content **MUST NOT** be truncated.


### Table columns ###

Providers must return all the columns as described in the table below, ordered by `End Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date`  | The start date of the problem | `dd-Mmm-yyyy` |
| <center>2</center> | `End Date` <i class="fa fa-sort-desc" aria-hidden="true">  | The end date of the problem | `dd-Mmm-yyyy` |
| <center>3</center> | `Entry`| A short human readable title for the problem | `free-text` |
| <center>4</center> | `Significance`| The significance of the problem (i.e. Major or Minor) | `free-text` |
| <center>5</center> | `Details` | Longer human readable details for the problem | `free-text` |



Provider systems not supporting Inactive Problems (e.g. Vision) **MUST** display a message in the Section Banner to indicate:

- Inactive Problems are not supported as in the [HTML Implementation Guide - Not Supported](accessrecord_development_html_implementation_guide.html#not-supported
) section.
- That any Problems and Issues recorded for the Patient are included in the Active Problems and Issues section.

Provider systems that do support Inactive Problems, but when no records exist for the requested Patient **MUST** display the standard [HTML Implementation Guide - Supported But Hasn't Been Recorded](accessrecord_development_html_implementation_guide.html#supported-but-hasnt-been-recorded) message.



## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/problems.html %}

