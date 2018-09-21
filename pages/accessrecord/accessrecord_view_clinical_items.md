---
title: Clinical items
keywords: getcarerecord, view, section, clinical items
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_clinical_items.html
summary: "Clinical items HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| CLI | Clinical Items | Yes | Yes | Yes | Yes |


## Clinical narrative ##

Items of information relating to the care, health or wellbeing of the patient. Examples of this type of information are: childhood and travel vaccinations, screening information and past medical history. It does not include administrative items such as invitations for health-related information.


## Purpose ##

The purpose of supplying clinical items within GP Connect is to allow a clinician to view a history of items relating to the health and wellbeing of a patient.

The list of clinical items is based on a consumer-supplied date range and is ordered by date descending (for example, most recent date/time first).

## Sections and subsections ##

There is a single main section for clinical items with no subsections.

## Section title ##

The section title **MUST** be "Clinical Items".

## Date filter ##

A date filter is applicable for the Clinical Items section.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.

## Table columns ##

Providers must return all the columns as described in the table below, sorted by `Date` descending:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date`  <i class="fa fa-sort-desc" aria-hidden="true"> | The date of entry of the clinical item | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry`| A short human readable title for the clinical item | `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the clinical item | `free-text` |

## Section business rules ##

The following business rules are applicable:

| Supplier | Business Rules |
|----------|----------------|
| EMIS | Includes coded clinical items relating to a patients care e.g. procedures, test results, conditions |
| TPP | Message to include indication of inclusion of practice-specific codes |
| Vision | Message to include meaningful interpretation of Read Chapter 1 with Chapters A - Z |
| Microtest | Message to include meaningful interpretation of items excluding Read Code Chapter 2 and Codes starting 9 and 0 |

## HTML view ##

{% include accessrecord/clinical.html %}


## Example view ##

<p data-height="400" data-theme-id="light" data-slug-hash="ooQORw" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Clinical Items" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/ooQORw/">clinical items</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/ooQORw) for an example of using AngularJS to generate table content." %}
