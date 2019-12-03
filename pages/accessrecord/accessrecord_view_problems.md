---
title: Problems and issues
keywords: getcarerecord, view, section, problems
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_problems.html
summary: "Problems and issues HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| PRB | Problems and Issues | Yes | Yes | Yes | Yes |


## Clinical narrative ##

Any issue that is significant to a patient that impacts their health or wellbeing. It includes disease, surgery and social issues such as bereavement or unemployment.

## Purpose ##

The purpose of this section is to provide information about a patient's significant problems and issues which will inform or may have previously informed the clinical decision-making process.


## Sections and subsections ##

Contains three sections:

 - [Active Problems and Issues](accessrecord_view_problems.html#active-problems-and-issues)
 - [Major Inactive Problems and Issues](accessrecord_view_problems.html#major-inactive-problems-and-issues)
 - [Other Inactive Problems and Issues](accessrecord_view_problems.html#other-inactive-problems-and-issues)

## Section title ##

The section title **MUST** be 'Problems and Issues'.
'
## Date filter ##

A date filter is applicable for the 'Problems and Issues' section.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.



## Active problems and issues ##

### Clinical narrative ###

Any active issue that is significant to a patient and affects their health or wellbeing. It includes disease, surgery and social issues such as bereavement or unemployment.

### Purpose ###

The purpose of this section is to provide information about a patient's current and potentially relevant significant problems and issues which will inform the clinical decision-making process.

### Subsection title ###

The subsection title **MUST** be 'Active Problems and Issues'.

### Date filter ###

All relevant records **MUST** be returned.

### Subsection content banner ###

Provider message describing at a summary level how they have populated this subsection.

### Table columns ###

Providers must return all the columns as described in the table below, sorted by `Start Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| 1 | `Start Date`  <em class="fa fa-sort-desc" aria-hidden="true">| The start date of the problem | `dd-Mmm-yyyy` |
| 2 | `Entry`| A short human readable title for the problem | `free-text` |
| 3 | `Significance`| The significance of the problem (meaning, Major or Minor) | `free-text` |
| 4 | `Details` | Longer human readable details for the problem | `free-text` |




## Major inactive problems and issues ##

### Clinical narrative ###

Any major inactive issue that was significant to a patient and affected their health or wellbeing. It includes disease, surgery and social issues such as bereavement or unemployment.

### Purpose ###

The purpose of this section is to provide information about a patient's previous significant problems and issues which may have informed the clinical decision-making process.

### Subsection title ###

The subsection title **MUST** be 'Major Inactive Problems and Issues'.

### Date filter ###

A date filter is applicable for the 'Major Inactive Problems and Issues' subsection.

### Subsection content banner ###

Provider message describing at a summary level how they have populated this subsection.

### Table columns ###

Providers must return all the columns as described in the table below, sorted by `End Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| 1 | `Start Date` | The start date of the problem | `dd-Mmm-yyyy` |
| 2 | `End Date`  <em class="fa fa-sort-desc" aria-hidden="true"> | The end date of the problem | `dd-Mmm-yyyy` |
| 3 | `Entry`| A short human-readable title for the problem | `free-text` |
| 4 | `Significance`| The significance of the problem (meaning, Major or Minor) | `free-text` |
| 5 | `Details` | Longer human readable details for the problem | `free-text` |

Provider systems having 3 levels of significance **MUST** include inactive problems with the highest and mid-level significance in this subsection. If more than 3 levels of significance, then those equal to or greater than the mid-level significance **MUST** be included in this subsection. Provider systems **MUST NOT** include problems without a significance level in this subsection (for example, if significance is not mandatory and has not be recorded).

Provider systems supporting inactive problems but not supporting clearly defined significance levels **MUST** return all inactive problems in the 'Other Problems and Issues' subsection, and **MUST**:

 - return a subsection content banner to indicate that any inactive problems are included in the 'Other Problems and Issues' subsection
 - return an error message in place of the subsection table as detailed in the [HTML Implementation Guide - Not Supported](accessrecord_development_html_implementation_guide.html#not-supported) section 

Systems not supporting inactive problems **MUST**:

 - return an error message in place of the subsection table as detailed in the [HTML Implementation Guide - Not Supported](accessrecord_development_html_implementation_guide.html#not-supported) section
 - display a message in the section banner to indicate that any problems and issues recorded for the patient are included in the 'Active Problems and Issues' section

Provider systems that support major inactive problems, but when no records exist for the requested patient, **MUST** display the standard [HTML implementation guide - supported but hasn't been recorded](accessrecord_development_html_implementation_guide.html#supported-but-hasnt-been-recorded) message.





## Other inactive problems and issues ##

### Clinical narrative ###

Any other inactive issue that was significant to a patient and affected their health or wellbeing. It includes disease, surgery and social issues such as bereavement or unemployment.

### Purpose ###

The purpose of this section is to provide information about a patient's previous non-major problems and issues which may have informed the clinical decision-making process.

### Subsection title ###

The subsection title **MUST** be 'Other Inactive Problems and Issues'.

### Date filter ###

A date filter is applicable for the 'Other Inactive Problems and Issues' subsection.

### Subsection content banner ###

Provider message describing at a summary level how they have populated this subsection.

### Table columns ###

Providers must return all the columns as described in the table below, sorted by `End Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| 1 | `Start Date` | The start date of the problem | `dd-Mmm-yyyy` |
| 2 | `End Date`  <em class="fa fa-sort-desc" aria-hidden="true"> | The end date of the problem | `dd-Mmm-yyyy` |
| 3 | `Entry`| A short human-readable title for the problem | `free-text` |
| 4 | `Significance`| The significance of the problem  | `free-text` |
| 5 | `Details` | Longer human readable details for the problem | `free-text` |


Provider systems having 3 levels of significance **MUST** include inactive problems with the lowest level of significance in this subsection. If more than 3 levels of significance, then those less than the mid-level significance must be included in this subsection. Any inactive problems which do not have a significance level **MUST** be included in this section.

Provider systems not supporting inactive problems **MUST** display a message in the section banner to indicate:

 - inactive problems are not supported as in the [HTML Implementation Guide - Not Supported](accessrecord_development_html_implementation_guide.html#not-supported) section
 - that any problems and issues recorded for the patient are included in the 'Active Problems and Issues' subsection

Provider systems that support inactive problems, but when no records exist for the requested patient, **MUST** display the standard [HTML implementation guide - supported but hasn't been recorded](accessrecord_development_html_implementation_guide.html#supported-but-hasnt-been-recorded) message.


## HTML view ##

{% include accessrecord/problems.html %}

## Example view ##

<p data-height="550" data-theme-id="light" data-slug-hash="gopbVv" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Problems" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/gopbVv/">Problems</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/gopbVv) for example of using AngularJS to generate table content." %}
