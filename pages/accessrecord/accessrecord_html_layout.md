---
title: Layout guide
keywords: 'getcarerecord, development, html, rendering'
sidebar: accessrecord_sidebar
permalink: accessrecord_development_html_layout_guide.html
summary: >-
  Overview of the common HTML view layout guidance in relation to the Access Record capability
tags:
  - development
  - getcarerecord
---

## Purpose ##

This document is intended for use by software developers, both provider supplier and consumer supplier, looking to build a conformant GP Connect HTML care record viewer application.

## Section layout ##

There are two styles of HTML view: pages where multiple tables are provided in the same HTML view page and those where a single table is returned. Sections with multiple tables are subdivided into *subsections*.

### HTML views with a single table ###
HTML views with a single table and hence a single section are:  

**Encounters**, **Clinical Items**, **Administrative Items**, **Observations**, **Referrals**, **Immunisations**.

These views **MUST** have the following structure:

- Section title
- GP transfer banner
- Content banner (*if applicable*)
- Date banner (*if applicable: section date range applied*)
- Exclusion banner (*if applicable: to indicate excluded items*)
- Table

### HTML views with multiple tables ###
HTML views with multiple tables and hence multiple subsections are:
 
**Summary**, **Problems and issues**, **Allergies and adverse reactions**, and **Medications**.

These views **MUST** have the following structure:

- Section title
- GP transfer banner
- Content banner (*if applicable*)
- Subsection (*repeated for each subsection*)
	- Subsection title (*for example, Current Medications*)
	- Subsection content banner (*if applicable*)
	- Date banner (*if applicable: subsection date range applied*)
	- Exclusion banner (*if applicable, to indicate excluded items*)
	- Table

{% include custominfocallout.html content="**Note:** This layout does not fully apply to the Summary HTML view. Subsection content banner messages **MUST** be included only when associated with table content visible in the Summary view. See [Summary HTML view](accessrecord_view_summary.html)." type="info" %}

### Single table example ###

```html
<div>
  <h1>Encounters</h1>
	
  <div class="gptransfer-banner">
    <p><!-- GP transfer banner --></p>
  </div>
	
  <div class="content-banner">
    <p><!-- Content banner --></p>
  </div>
  
  <div class="date-banner">
    <p><!-- Date banner --></p>
  </div>
  
  <div class="exclusion-banner">
    <p><!-- Exclusion banner --></p>
  </div>
  
  <table id="enc-tab">
    <!-- table data -->
  </table>
</div>
```

### Multiple table example ###

```html
<div>
  <h1>Problems and Issues</h1>
   
  <div class="gptransfer-banner">
    <p><!-- GP transfer banner --></p>
  </div>
	
  <div class="content-banner">
    <p><!-- Content banner --></p>
  </div>

  <div>
    <h2>Active Problems and Issues</h2>
	
	<div class="content-banner">
	  <p><!-- Content banner --></p>
	</div>
    
	<div class="date-banner">
	  <p><!-- Date banner --></p>
	</div>
    
	<div class="exclusion-banner">
	  <p><!-- Exclusion banner --></p>
	</div>
    
	<table id="prb-tab-act">
	  <!-- table data -->
	</table>
  </div>
  
  <div>
    <h2>Major Inactive Problems and Issues</h2>

	<div class="content-banner">
	  <p><!-- Content banner --></p>
	</div>
    
	<div class="date-banner">
	  <p><!-- Date banner --></p>
	</div>
    
	<div class="exclusion-banner">
	  <p><!-- Exclusion banner --></p>
	</div>
    
	<table id="prb-tab-majinact">
	  <!-- table data -->
	</table>
  </div>
	
  <div>
    <h2>Other Inactive Problems and Issues</h2>

	<div class="content-banner">
	  <p><!-- Content banner --></p>
	</div>
    
	<div class="date-banner">
	  <p><!-- Date banner --></p>
	</div>
    
	<div class="exclusion-banner">
	  <p><!-- Exclusion banner --></p>
	</div>
    
	<table id="prb-tab-othinact">
	  <!-- table data -->
	</table>
  </div>
</div>
```

## Section and subsection title ##

The section title **MUST** be inside a `<h1>` tags and subsection title **MUST** be inside a `<h2>` tags.

The section and subsection titles are defined in the individual HTML view pages.

## Banners ##

The provider **MUST** return banner messages as described in this section. The consumer system **MUST** present the banner messages as returned by the provider system.

### GP transfer banner ###

In the scenario where the patient's GP record is not 'fully integrated' into the 'new' GP, following a GP transfer, then only data entered to the new GP's record **MUST** be provided. A warning message stating that the record is either not available (no data entered to the new GP record), or incomplete due to the transfer, **MUST** be provided and displayed. The message **MUST** include the date that the data has been excluded from. Set dd-Mmm-yyyy to the date the patient registered at their new GP practice.

```html
<div class="gptransfer-banner">
	<p>Patient record transfer from previous GP practice not yet complete; information recorded before dd-Mmm-yyyy may be missing</p>
</div>
```

### Content banners ###

The content banner **MUST** be used by the provider to detail any specific business rules applied to the section content which is not standard across providers, or any non-compliance with the specification due to constraints of their GP system. 

#### Section content banner ####

Any content description for a section **MUST** be applicable to the whole section (apply to all subsections) and **MUST NOT** be replicated in the subsection content banner.

#### Subsection content banner ####

Any content descriptions for a subsection **MUST** be applicable to that subsection only. Where the content description applies to more than one subsection (but not all), it **MUST** be repeated in the applicable subsections. A subsection content description **MUST NOT** be replicated as section content.


### Date banner ###

A date banner **MUST NOT** be returned for sections which do not support a date filter. See individual HTML views for section date filters supported. For sections which support date filters, the following date banners **MUST** be returned as applicable. 


#### Applied date ranges ####

Provider systems **MUST** return the consumer date range applied to a section's data, where applicable, beneath the section/subsection header.

If consumer start date and end date applied:

```html
<div class="date-banner">
	<p>For the period 'dd-Mmm-yyyy' to 'dd-Mmm-yyyy'</p>
</div>
```

If no consumer end date applied: 

```html
<div class="date-banner">
	<p>Data items from [Start Date]</p>
</div>
``` 

If no consumer start date applied:

```html
<div class="date-banner">
	<p>Data items until [End Date]</p> 
</div>
``` 

#### Not applied date ranges ####

In the event of a consumer date range being applied to a section, subsections not supporting a date filter **MUST** display the following:

```html
<div class="date-banner">
	<p>Date filter not applied</p> 
</div>
``` 

The purpose of this message is to make clear that a consumer specified date filter has not been applied to the subsection(s), which does not support date filters.


#### Default date ranges ####

Where the consumer system has not supplied a date range for a section which supports date filters, and while the default is for ALL items to be provided, the following message **MUST** be supplied by the provider beneath the section/subsection header.

```html
<div class="date-banner">
	<p>All relevant items</p>
</div>
``` 


### Section exclusion banner ###

Exclusions may be applied to the section/subsections in various circumstances. Where any exclusions have been applied a message banner **MUST** be included. As shown in the layout, the exclusion banner will only be included against the specific table where exclusions have been applied. Therefore, it will only be at section level where it is a single table section.

The following message **MUST** be supplied by the provider if any items were excluded for these reasons:


```html
<div class="exclusion-banner">
	<p>Items excluded due to confidentiality and/or patient preferences</p>
</div>
```

## Date filters ##

The provider **MUST** supply all matching dates/times, for example, the period 23-May-2018 to 27-May-2018 includes all items with times from the start of the 23rd May through to the end of the 27th of May.

If no end date is supplied, the provider **MUST** supply all data from start date onwards (including future where applicable).

If no start date is supplied, the provider **MUST** supply all data until the end date.


## Per section default time frames ##

Date filtering is not applicable to all views and for those supporting date filtering it may not be applicable to all subsections.

{% include custominfocallout.html content="**Information:** Section default time frames to be reviewed following FoT feedback. A default time frame is only to be applied upon instruction by NHS Digital." type="warning" %}

|Section                              | Section code     | Subsections                                 | Time frame        |
|-------------------------------------|:----------------:|-------------------------------------------- |-------------------|
| **Administrative items**            | `ADM`            | N/A                                         | Consumer supplied |
| **Allergies and adverse reactions** | `ALL`            | Current allergies and adverse reactions     | N/A               |
|                                     |                  | Historical allergies and adverse reactions  | N/A               |
| **Clinical items**                  | `CLI`            | N/A                                         | Consumer supplied |
| **Encounters**                      | `ENC`            | N/A                                         | Consumer supplied |
| **Immunisations**                   | `IMM`            | N/A                                         | N/A               |
| **Medications**                     | `MED`            | Acute Medication (Last 12 Months)           | All               |
|                                     |                  | Current Repeat Medication                   | All               |
|                                     |                  | Discontinued Repeat Medication              | All               |
|                                     |                  | All Medication                              | Consumer supplied |
|                                     |                  | All Medication Issues                       | Consumer supplied |
| **Observations**                    | `OBS`            | N/A                                         | Consumer supplied |
| **Problems and issues**             | `PRB`            | Active problems and issues                  | All               |
|                                     |                  | Major inactive problems and issues          | Consumer supplied |
|                                     |                  | Other inactive problems and issues          | Consumer supplied |
| **Referrals**                       | `REF`            | N/A                                         | Consumer supplied |
| **Summary**                         | `SUM`            | N/A                                         | N/A               |
| **Emergency Codes**                 |  N/A             | N/A                                         | N/A               |


The default time frame **MUST** be configurable in unit of month(s). It **MUST** be configurable by section (meaning, different sections can be configured with different defaults).

When a default time frame is applied at section level the following requirements **MUST** be adhered to:

- any section/subsection listed in the table above with a time frame of 'All' **MUST** return all data regardless of the default time frame applied
- any section/subsection listed with 'Consumer supplied' **MUST** only apply the default time frame when the consumer does not provide any date filter values
  - a default date filter **MUST NOT** override a consumer supplied date filter value, meaning, the provider **MUST** return the full period as selected by the user
- any section listed with a mix of 'All' and 'Consumer supplied' **MUST** apply the above requirements at the relevant subsection levels

When applying a default time frame the following messages **MUST** be supplied by the provider:

Subsection's time frame 'Consumer supplied'

```html
<div class="date-banner">
    <p> All data items from [SysDate – DefaultDatePeriod]</p>
</div>
```

Subsection's time frame 'All'

```html
<div class="date-banner">
	<p>Date filter not applied</p>
</div>
``` 


Provider systems **MUST** return a HTTP *Bad Request* `400` error response if a date range is specified for a section that does not support filtering by a consumer supplied date range.

## Generic table construction requirements ##

Providers must adhere to the table construction requirements listed below:

- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

{% include custominfocallout.html content="**Information:** All other table requirements can be found on their associated HTML view page." type="info" %}

Consumer systems **MUST** display all content supplied by the provider system.
