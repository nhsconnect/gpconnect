---
title: Clinical items
keywords: getcarerecord, view, section, clinical items
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_clinical_items.html
summary: "Clinical Items HTML view"
---

<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| CLI | Clinical Items | Yes | Yes | Yes | Yes |


## Clinical narrative ##

Items of information relating to the care, health or wellbeing of the patient. Examples of this type of information are: childhood and travel vaccinations, screening information and past medical history. It does not include administrative items such as invitations for health-related information.

## Purpose ##

The purpose of supplying clinical items within GP Connect is to allow a clinician to view a history of items relating to the health and wellbeing of a patient.

## Sections and subsections ##

There is a single main section for clinical items with no subsections.

### Date filter ###

A date filter is applicable for the Clinical items section. Provider messages for a date filter can be found [here](accessrecord_provider_variance.html#date-banner-message).

### Section content banner ###

Provider message(s) describing at a summary level how this section has been populated. Provider content messages can be found [here](accessrecord_provider_variance.html#clinical-items).

### Table construction requirements ###

Providers **MUST** adhere to the table construction requirements listed below:

- table header **MUST** be "Clinical Items"
- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

### Table columns ###

Providers **MUST** return all the columns as described in the table below, ordered by `Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` <i class="fa fa-sort-desc" aria-hidden="true">| The date of entry of the clinical item | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry`| A short human readable title for the clinical item | `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the clinical item | `free-text` |


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/clinical.html %}


