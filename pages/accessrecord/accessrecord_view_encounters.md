---
title: Encounters
keywords: getcarerecord, view, section, encounters
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_encounters.html
summary: "Encounters HTML view"
---
<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ENC | Encounters | Yes | Yes | Yes | Yes |


## Clinical narrative ##

An encounter is an interaction between a patient and a health care professional (HCP) that is recorded on the patient record. This can include:

- planned encounters - such as pre-arranged Appointments with a GP
- unplanned encounters - such as at an out of hours clinic and those unrecorded through appointment module(s)
- direct encounters - such as a face-to-face session with a GP
- indirect encounters - such as a GP reviewing and updating a patient record on receipt of some test results


## Purpose ##

The purpose of supplying encounters within GP Connect is to allow a clinician to view a history of a patient’s interactions with a clinician or an HCP.

## Sections and subsections ##

There is a single main section for encounters with no subsections.

### Date filter ###

A date filter is applicable for the encounters section. Provider messages for a date filter can be found [here](accessrecord_provider_variance.html#date-banner-message).

### Section content banner ###

Provider message(s) describing at a summary level how this section has been populated. Provider content messages can be found [here](accessrecord_provider_variance.html#encounters).

### Table construction requirements ###

Providers **MUST** adhere to the table construction requirements listed below:

- table header **MUST** be "Encounters"
- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

### Table columns ###

Providers **MUST** return all the columns as described in the table below, ordered by `Date` descending:

| Order | Name | Description | Value Details |
| ----- | ---- | ----------- | ------------- |
| <center>1</center> | `Date` <i class="fa fa-sort-desc" aria-hidden="true">| The date of the encounter | `dd-Mmm-yyyy` |
| <center>2</center> | `Title`| A short human readable title for the encounter, to be composed of a subset of the `Practitioner` and `Organization` details linked to the encounter| `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the encounter | `free-text` |


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/encounters.html %}

