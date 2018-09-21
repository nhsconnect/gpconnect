---
title: Encounters
keywords: getcarerecord, view, section, encounters
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_encounters.html
summary: "Encounters HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ENC | Encounters | Yes | Yes | Yes | Yes |


## Clinical narrative ##

An encounter is an interaction between a patient and a health care professional (HCP) that is recorded on the patient record. This can include:

- Planned encounters - such as pre-arranged appointments with a GP
- Unplanned encounters - such as at an out of hours clinic and those unrecorded through appointment module(s)
- Direct encounters - such as a face-to-face session with a GP
- Indirect encounters - such as a GP reviewing and updating a patient record on receipt of some test results


## Purpose ##

The purpose of supplying encounters within GP Connect is to allow a clinician to view a history of a patient’s interactions with a clinician or an HCP.

The list of encounters is based on a consumer-supplied date range and is ordered by date descending (that is, most recent date/time first).

Data will include the date, the practitioner (and role) and organisation (and code), then a block of free text which will include any free text narrative recorded during the consultation and some basic details of related activities will also be shown (for example, medications prescribed, procedures performed, diagnosis recorded, examinations, history recorded, care plans created, allergies or sensitivities recorded).

## Sections and subsections ##

There is a single main section for encounters with no subsections.

## Section title ##

The section title **MUST** be "Encounters".

## Date filter ##

A date filter is applicable for the encounters section.

## Section content banner ##

Provider message describing at a summary level how they have populated this section.

## Table columns ##

Providers must return all the columns as described in the table below, sorted by `Date` descending:

| Order | Name | Description | Value Details |
| ----- | ---- | ----------- | ------------- |
| <center>1</center> | `Date`  <i class="fa fa-sort-desc" aria-hidden="true">| The date of the encounter | `dd-Mmm-yyyy` |
| <center>2</center> | `Title`| A short human-readable title for the encounter, to be composed of a subset of the `Practitioner` and `Organization` details linked to the encounter| `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the encounter | `free-text` |

## HTML view ##

{% include accessrecord/encounters.html %}

## Example view ##

<p data-height="930" data-theme-id="light" data-slug-hash="JMdYpm" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Encounters" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/JMdYpm/">Encounters</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/JMdYpm) for an example of using AngularJS to generate table content." %}
