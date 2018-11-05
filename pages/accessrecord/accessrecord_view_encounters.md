---
title: Encounters
keywords: getcarerecord, view, section, encounters
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_encounters.html
summary: "Encounters HTML view"
---


| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ENC | Encounters | Yes | Yes | Yes | Yes |


## Clinical narrative ##

An encounter is an interaction between a patient and a health care professional (HCP) that is recorded on the patient record. This can include:

- Planned encounters - such as pre-arranged Appointments with a GP
- Unplanned encounters - such as at an out of hours clinic and those unrecorded through appointment module(s)
- Direct encounters - such as a face-to-face session with a GP
- Indirect encounters - such as a GP reviewing and updating a patient record on receipt of some test results


## Purpose ##

The purpose of supplying encounters within GP Connect is to allow a clinician to view a history of a patient’s interactions with a clinician or an HCP.

## Sections and subsections ##

There is a single main section for encounters with no subsections.


### Date filter ###

A date filter is applicable for the encounters section. Provider messages for a date filter can be found [here](accessrecord_provider_variance.html#date-banner-message).


### Section content banner ###

Provider messages describing at a summary level how they have populated this section can be found [here](accessrecord_provider_variance.html#encounters).


### Table construction requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **MUST** be "Encounters".
- Table columns **MUST** be ordered left-to-right (1..N).
- Table content **MUST NOT** be truncated.



### Table columns ###

Providers must return all the columns as described in the table below, ordered by `Date` descending:

| Order | Name | Description | Value Details |
| ----- | ---- | ----------- | ------------- |
| <center>1</center> | `Date` <i class="fa fa-sort-desc" aria-hidden="true">| The date of the encounter | `dd-Mmm-yyyy` |
| <center>2</center> | `Title`| A short human readable title for the encounter, to be composed of a subset of the `Practitioner` and `Organization` details linked to the encounter| `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the encounter | `free-text` |


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/encounters.html %}

