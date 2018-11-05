---
title: Observations
keywords: getcarerecord, view, section, observations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_observations.html
summary: "Observations HTML view"
---

<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| OBS | Observations | Yes | Yes | Yes | Yes |

## Clinical narrative ##

A clinical observation is a repeatable data element recorded by health professionals in the course of assessment or care of their patients or clients. Examples include, blood pressure measurement, weight, height or temperature.

## Purpose ##

The purpose of this section is to enable the clinician to view and compare chronologically data recorded in structured form pertaining to a patient’s physical condition.

## Sections and subsections ##

There is only a single main section for Observations with no subsections.

### Date filter ###

A date filter is applicable for the Observations section. Provider messages for a date filter can be found [here](accessrecord_provider_variance.html#date-banner-message).

### Section content banner ###

Provider messages describing at a summary level how they have populated this section can be found [here](accessrecord_provider_variance.html#observations).


### Table construction requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **MUST** be "Observations".
- Table columns **MUST** be ordered left-to-right (1..N).
- Table content **MUST NOT** be truncated.


### Table columns ###

Providers must return all the columns as described in the table below, ordered by `Date` descending:


| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ----- | ---- | ----------- | -------------------------------- |
| <center>1</center> | `Date`  <i class="fa fa-sort-desc" aria-hidden="true"> | The date of the observation | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry`   | A short human readable free-text title for the observation | `free-text` |
| <center>3</center> | `Value`   | Value and range (where available) of the observation | `free-text` |
| <center>4</center> | `Details` | Longer human readable details for the observation. Number formatting must follow the guidelines published on page 5 of the [CUI Medication Line](http://webarchive.nationalarchives.gov.uk/20160921162642/http://systems.digital.nhs.uk/data/cui/uig/medlineqig.pdf) document.  | `free-text` |



{% include custominfocallout.html content="**Important:** GP Principal suppliers have indicated this section will contain all clinical items that represent measurement data (i.e. blood pressure, temperature, heart rate etc.)." type="warning" %}
	
	
## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/observations.html %}

