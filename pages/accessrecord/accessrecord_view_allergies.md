---
title: Allergies and adverse reactions
keywords: getcarerecord, view, section, allergies
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_allergies.html
summary: "Allergies HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ALL | Allergies and Adverse Reactions| Yes | Yes<sup>1</sup> | Yes<sup>2</sup> | Yes |

<sup>1</sup> EMIS have indicated that they are including all allergies & sensitivities in the 'Current Allergies …..' section

<sup>2</sup> Vision have indicated they don't record end dates for allergies & sensitivities. Hence, no History view is possible

## Clinical narrative ##

A reaction to a substance not intended to occur. Allergies are caused by hypersensitivity of the immune system to an external agent.

## Purpose ##

The purpose of this section is to provide the clinician with a list of patient allergies to enable safe prescribing and treatment recommendations for a patient.

## Sections and subsections ##

Contains two subsections:

 - [Current Allergies and Adverse Reactions](accessrecord_view_allergies.html#current-allergies-and-adverse-reactions)
 - [Historical Allergies and Adverse Reactions](accessrecord_view_allergies.html#historical-allergies-and-adverse-reactions)

## Section title ##

The section title **MUST** be 'Allergies and Adverse Reactions'.
 
## Date filter ##

Date filters are not supported for this section all relevant records shall be returned for the current and historic allergies and adverse reactions.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.



## Current allergies and adverse reactions ##

### Clinical narrative ###

A reaction to a substance not intended to occur. Allergies are caused by hypersensitivity of the immune system to an external agent.

### Purpose ###

The purpose of this section is to provide the clinician with a list of current allergies to enable safe prescribing and treatment recommendations for a patient.

### Subsection title ###

The subsection title **MUST** be 'Current Allergies and Adverse Reactions'.

### Subsection content banner ###

Provider message describing at a summary level how they have populated this subsection.

### Table columns ###

Providers must return all the columns as described in the table below, sorted by `Start Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| 1 | `Start Date`  <em class="fa fa-sort-desc" aria-hidden="true">| The start date of the allergy or adverse reaction | `dd-Mmm-yyyy` |
| 2 | `Details` | Longer human-readable details for the allergy or adverse reaction | `free-text` |


## Historical allergies and adverse reactions ##

### Clinical narrative ###

A reaction to a substance not intended to occur. Allergies are caused by hypersensitivity of the immune system to an external agent.

### Purpose ###

The purpose of this section is to provide the clinician with a list of historical allergies to enable safe prescribing and treatment recommendations for a patient.

### Subsection title ###

The subsection title **MUST** be 'Historical Allergies and Adverse Reactions'.

### Subsection content banner ###

Provider message describing at a summary level how they have populated this subsection.

### Table columns ###

Providers must return all the columns as described in the table below, sorted by `End Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| 1 | `Start Date` | The start date of the allergy or adverse reaction | `dd-Mmm-yyyy` |
| 2 | `End Date`  <em class="fa fa-sort-desc" aria-hidden="true"> | The end date of the allergy or adverse reaction | `dd-Mmm-yyyy` |
| 3 | `Details` | Longer human readable details for the allergy or adverse reaction | `free-text` |


## HTML view ##

{% include accessrecord/allergies.html %}

## Example view ##

<p data-height="530" data-theme-id="light" data-slug-hash="NXqqZW" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Allergies" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/NXqqZW/">Allergies</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/NXqqZW) for example of using AngularJS to generate table content." %}
