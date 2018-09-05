---
title: HTML Layout Guide
keywords: 'getcarerecord, development, html, rendering'
sidebar: accessrecord_sidebar
permalink: accessrecord_development_html_layout_guide.html
summary: >-
  Overview of the common HTML view layout guidance in relation to the Access
  Record capability.
tags:
  - development
  - getcarerecord
---

## HTML layout guide ##

### Purpose ###

This document is intended for use by software developers looking to build a conformant GP Connect HTML care record viewer application.

## Section layout ##

There are two styles of HTML View: pages where multiple tables are provided in the same HTML View page and those where a single table is returned.  Sections with multiple tables are subdivided into *Sub-sections*.

### HTML views with a single table ###
HTML Views with a single table and hence a single Section are:  

**Encounters**, **Clinical Items**, **Administrative Items**, **Observations**, **Referrals**, **Immunisations**.

These Views **SHALL** have the following structure:

- Section title
- GP transfer banner
- Content banner (*if applicable*)
- Date banner (*if applicable: section date range applied*)
- Exclusion banner (*if applicable: to indicate excluded items*)
- Table

### HTML views with multiple tables ###
HTML Views with multiple tables and hence multiple Sections are:
 
**Problems**, **Allergies**, **Medications**.

These Views **SHALL** have the following structure:

- Section title
- GP transfer banner
- Content banner (*if applicable*)
- Subsection (*repeated for each subsection*)
	- Subsection title (*e.g. Current Medications*)
	- Subsection content banner (*if applicable*)
	- Date banner (*if applicable: section date range applied*)
	- Exclusion banner (*if applicable, to indicate excluded items*)
	- Table

{% include custominfocallout.html content="**Note:** This layout does not apply to the Summary HTML View.  See [Summary HTML View](accessrecord_view_summary.html)" type="info" %}

#### Single table example ####

```html
<div>
  <h1>Encounters</h1>
  
  <div>
    <p><!-- Content Banner --></p>
  </div>
  
  <div>
    <p><!-- Date Banner --></p>
  </div>
  
  <div>
    <p><!-- Exclusion Banner --></p>
  </div>
  
  <table>
    <!-- table data -->
  </table>
</div>
```

#### Multiple table example ####

```html
<div>
  <h1>Problems and Issues</h1>
  
  <div>
    <p><!-- Content Banner --></p>
  </div>

  <div>
    <h2>Active Problems and Issues</h2>
    
	<div>
	  <p><!-- Date Banner --></p>
	</div>
    
	<div>
	  <p><!-- Exclusion Banner --></p>
	</div>
    
	<table>
	  <!-- table data -->
	</table>
  </div>
  
  <div>
    <h2>Inactive Problems and Issues</h2>
    
	<div>
	  <p><!-- Date Banner --></p>
	</div>
    
	<div>
	  <p><!-- Exclusion Banner --></p>
	</div>
    
	<table>
	  <!-- table data -->
	</table>
  </div>
</div>
```

## Section and subsection title ##

The section title **SHALL** be inside a `<h1>` tags and sub-section title SHALL be inside a `<h2>` tags.

The section and subsection titles are defined in the individual html view pages.

## GP transfer banner ##

In the scenario where the patient's GP record is not 'fully integrated' into the 'new' GP, following a GP transfer, then only data entered to the new GP's record **SHALL** be provided. A warning message stating that the record is either not available (no data entered to the new GP record), or incomplete due to the transfer, **SHALL** be provided and displayed.

```html
<div>
	<p>GP transfer underway – record may be incomplete</p>
</div>
```

## Content banners ##

The content banner **SHALL** be used by the provider to detail any specific business rules applied to the section content which is not standard across providers, or any non-compliance with the specification due to constraints of their GP system. 

### Section content banner ###

Any content description for a section **MUST** be applicable to the whole section (apply to all subsections) and **MUST NOT** be replicated in the subsection content banner.

### Subsection content banner ###

Any exclusion descriptions for a subsection **MUST** be applicable to that subsection only. Where the exclusion description applies to more than one subsection (but not all), it **MUST** be repeated in the applicable subsections. A subsection exclusion description **MUST NOT** be replicated as section content.


## Date banner ##

The Provider **SHALL** supply all matching dates/times, e.g. the period 2011-05-23 to 2011-05-27 includes all items with times from the start of the 23rd May through to the end of the 27th of May.

If no end date is supplied, the Provider **SHALL** supply all data from start date onwards (including future where applicable).

If no start date is supplied, the Provider **SHALL** supply all data until the end date.

### Applied date ranges ###

Consumer Systems **SHALL** display the date range applied to a section's data, as supplied by the Provider where applicable, beneath the Section Header.

```html
<div>
	<p>For the period 'dd-mmm-yyyy' to 'dd-mmm-yyyy'</p>
</div>
```

If no Consumer End date: 

```html
<div>
	<p>All Data Items from [Start Date]</p>
</div>
``` 

If no Consumer Start date:

```html
<div>
	<p>All Data Items until [End Date]</p> 
</div>
``` 

### Default date ranges ###

Where the Consumer System has not supplied a date-range, then where applicable and while the default is for ALL items to be provided, the following message **SHALL** be supplied by the Provider and displayed by the Consumer System beneath the Section Header.

```html
<div>
	<p>All relevant items</p>
</div>
``` 

### Per section default time frames ###

Section Default Time Frames **SHALL** be configurable, by the Provider, to be easily amendable if required in response to FoT feedback 

{% include custominfocallout.html content="**Information:** Section default time frames to be reviewed following FoT feedback." type="warning" %}

| Section Code   | Time Frame | FHIR Resource(s) |
|----------------|------------|------------------|
| ADM  | All |- |                
| ALL  | All Relevant | AllergyIntolerance<sup>1</sup> |
| CLI  | All | Condition, Procedure |
| ENC  | All | Encounter |
| IMM  | All Relevant | Immunization<sup>1</sup> |
| MED  | All Relevant | Medication, MedicationOrder, MedicationDispense, MedicationAdministration |
| OBS  | All Relevant | Observation |
| PRB  | All Relevant | Problem|
| REF  | All Relevant | Referral |
| SUM  | - | Summary<sup>2</sup> |

<sup>1</sup> An explicit time frame is not allowed to be specified as the system **SHALL** return 'All Relevant' resources.<br>
<sup>2</sup> An explicit time frame is not allowed as these are set piece views, the system **SHALL** return 'All Relevant' resources.

Provider systems **SHALL** return a HTTP *Bad Request* `400` error response if a date range is specified for a section that does not support filtering by a consumer supplied date range.

## Section exclusion banner ##

Exclusions may be applied to the section / subsections in various circumstances. Where any exclusions have been applied a message banner **SHALL** be included. As shown in the layout, the exclusion banner will only be included against the specific table where exclusions have been applied, therefore it will only be at section level where it is a single table section.

The following message **SHALL** be supplied by the Provider if any items were excluded for these reasons.


```html
<div>
	<p>Items excluded due to confidentiality, patient preferences and/or RCGP sensitive dataset exclusions</p>
</div>
```

## Section content message ##

Following the Section Header & Date Range Applied, Consumer Systems **SHALL** display the Provider-returned message describing the contents of the section and indicating where contents may vary - e.g. where Historical Allergies are included in the Current Allergies sub-section, or where a particular column is not provided




