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

This document is intended for use by software developers looking to build a conformant GP Connect HTML care record viewer application.

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
 
**Problems**, **Allergies**, **Medications**.

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
    <h2>Inactive Problems and Issues</h2>

	<div class="content-banner">
	  <p><!-- Content banner --></p>
	</div>
    
	<div class="date-banner">
	  <p><!-- Date banner --></p>
	</div>
    
	<div class="exclusion-banner">
	  <p><!-- Exclusion banner --></p>
	</div>
    
	<table id="prb-tab-inact">
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

In the scenario where the patient's GP record is not 'fully integrated' into the 'new' GP, following a GP transfer, then only data entered to the new GP's record **MUST** be provided. A warning message stating that the record is either not available (no data entered to the new GP record), or incomplete due to the transfer, **MUST** be provided and displayed. The message **MUST** include the date that the data has been excluded from.

```html
<div class="gptransfer-banner">
	<p>Patient record transfer from previous GP Practice not yet complete; any information recorded before dd-mmm-yyyy has been excluded</p>
</div>
```

### Content banners ###

The content banner **MUST** be used by the provider to detail any specific business rules applied to the section content which is not standard across providers, or any non-compliance with the specification due to constraints of their GP system. 

#### Section content banner ####

Any content description for a section **MUST** be applicable to the whole section (apply to all subsections) and **MUST NOT** be replicated in the subsection content banner.

#### Subsection content banner ####

Any exclusion descriptions for a subsection **MUST** be applicable to that subsection only. Where the exclusion description applies to more than one subsection (but not all), it **MUST** be repeated in the applicable subsections. A subsection exclusion description **MUST NOT** be replicated as section content.


### Date banner ###

The provider **MUST** supply all matching dates/times - for example, the period 2011-05-23 to 2011-05-27 includes all items with times from the start of the 23rd May through to the end of the 27th of May.

If no end date is supplied, the provider **MUST** supply all data from start date onwards (including future where applicable).

If no start date is supplied, the provider **MUST** supply all data until the end date.

#### Applied date ranges ####

Consumer systems **MUST** display the date range applied to a section's data, as supplied by the provider where applicable, beneath the section header.

```html
<div class="date-banner">
	<p>For the period 'dd-mmm-yyyy' to 'dd-mmm-yyyy'</p>
</div>
```

If no consumer end date: 

```html
<div class="date-banner">
	<p>All data items from [Start Date]</p>
</div>
``` 

If no consumer start date:

```html
<div class="date-banner">
	<p>All data items until [End Date]</p> 
</div>
``` 

#### Default date ranges ####

Where the consumer system has not supplied a date range, then where applicable and while the default is for ALL items to be provided, the following message **MUST** be supplied by the provider and displayed by the consumer system beneath the section header.

```html
<div class="date-banner">
	<p>All relevant items</p>
</div>
``` 

#### Per section default time frames ####

Section default time frames **MUST** be configurable, by the provider, to be easily amendable if required in response to First of Type (FoT) feedback.

{% include custominfocallout.html content="**Information:** Section default time frames to be reviewed following FoT feedback." type="warning" %}

|Section                          | Section code   | Time frame   |
|---------------------------------|----------------|--------------|
| Administrative items            | ADM            | Consumer supplied |              
| Allergies and adverse reactions | ALL            | All          |
| Clinical items                  | CLI            | Consumer supplied |
| Encounters                      | ENC            | Consumer supplied |
| Immunisations                   | IMM            | All          |
| Medications                     | MED            | Consumer supplied (for past medications only) |
| Observations                    | OBS            | Consumer supplied |
| Problems and issues             | PRB            | Consumer supplied (for inactive problems and issues only) |
| Referrals                       | REF            | Consumer supplied |
| Summary                         | SUM            | All          |


Provider systems **MUST** return a HTTP *Bad Request* `400` error response if a date range is specified for a section that does not support filtering by a consumer supplied date range.

### Section exclusion banner ###

Exclusions may be applied to the section/subsections in various circumstances. Where any exclusions have been applied a message banner **MUST** be included. As shown in the layout, the exclusion banner will only be included against the specific table where exclusions have been applied. Therefore, it will only be at section level where it is a single table section.

The following message **MUST** be supplied by the provider if any items were excluded for these reasons:


```html
<div class="exclusion-banner">
	<p>Items excluded due to confidentiality and/or patient preferences</p>
</div>
```

## Generic table construction requirements ##

Providers must adhere to the table construction requirements listed below:

- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

{% include custominfocallout.html content="**Information:** All other table requirements can be found on their associated HTML view page." type="info" %}

Consumer systems **MUST** display all content supplied by the provider system.
