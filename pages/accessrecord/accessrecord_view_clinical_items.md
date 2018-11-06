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

Provider messages describing at a summary level how they have populated this section can be found [here](accessrecord_provider_variance.html#clinical-items).


### Table construction requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **MUST** be "Clinical Items".
- Table columns **MUST** be ordered left-to-right (1..N).
- Table content **MUST NOT** be truncated.



### Table columns ###

Providers must return all the columns as described in the table below, ordered by `Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` <i class="fa fa-sort-desc" aria-hidden="true">| The date of entry of the clinical item | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry`| A short human readable title for the clinical item | `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the clinical item | `free-text` |


### Section business rules ###

The following business rules are applicable:

| Supplier | Business Rules |
|----------|----------------|
| EMIS | N/A |
| TPP | Message to include indication of inclusion of practice-specific codes |
| Vision | Message to include meaningful interpretation of Read Chapter 1 with Chapters A - Z |
| Microtest | Message to include meaningful interpretation of items excluding Read Code Chapter 2 and Codes starting 9 and 0 |


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/clinical.html %}


