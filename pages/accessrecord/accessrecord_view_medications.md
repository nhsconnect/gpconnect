---
title: Medications
keywords: getcarerecord, view, section, medications
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_medications.html
summary: "Medications HTML view"
---
{% include customcallout.html content="**Warning:** The content of the Medications view is currently under review following initial First of Type feedback, and will be uplifted in a future version of the specification." type="danger" %}

<a href="#" class="back-to-top">Back to Top</a>

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| MED | Medications | Yes | Yes | Yes | Yes |


## Clinical narrative ##

A drug or other form of medicine that is used to treat or prevent disease. 

## Purpose ##

The purpose of this section is to provide a chronological history of medication prescribing as recorded.

## Sections and subsections ##

Contains one main section, and three subsections:

 - [Current Medication Issues](accessrecord_view_medications.html#current-medication-issues)
 - [Current Repeat Medications](accessrecord_view_medications.html#current-repeat-medications)
 - [Past Medications](accessrecord_view_medications.html#past-medications)
 
### Section content banner ###

Provider message(s) describing at a summary level how this section has been populated. Provider content messages can be found [here](accessrecord_provider_variance.html#medications).




## Current medication issues ##

### Clinical narrative ###

A list of drugs or other forms of medicines that are currently being used to treat or prevent disease for the patient.

### Purpose ###

The purpose of this subsection is to provide a view of medications that the patient is currently taking which informs the clinical decision-making process.

{% include customcallout.html content="**Warning:** The current medications list will only contain those items prescribed by the patient's current GP organization. Hence, if the patient has been issued prescriptions elsewhere or has recently moved GP practice then this list may not be complete. " type="danger" %} 

### Date filter ###

A default or consumer provided date range **MUST NOT** be applied by the provider for this section. The current issue of repeat or acute medication will be returned.

### Subsection content banner ###

There are no content banner messages for this subsection.

### Table construction requirements ###

Providers **MUST** adhere to the table construction requirements listed below:

- table header **MUST** be "Current Medication Issues"
- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

### Table columns ###

Providers **MUST** return all the columns as described in the table below, ordered by `Start Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date`  <i class="fa fa-sort-desc" aria-hidden="true">  | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp;| Descriptive name of medication item (including dosage) | `free-text` |
| <center>3</center> | `Type` | Type of medication issued (values `Repeat` or `Acute`) | `free-text` |
| <center>4</center> | `Scheduled End` | Scheduled end date of medication issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Days Duration` | Duration of medication issued | `integer` |
| <center>6</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | `free-text` |




## Current repeat medications##

### Clinical narrative ###

A list of repeat drugs or other forms of medicines that are currently being used to treat or prevent disease for the patient. This may also include PRN occasional use medication - for example, EpiPen, antihistamines, monitoring and continence products.

### Purpose ###

The purpose of this subsection is to provide a view of repeat medications that the patient is currently prescribed, which informs the clinical decision-making process.

### Date filter ###

A default or consumer provided date range **MUST NOT** be applied by the provider for this section. All current repeat medication (templates/courses) will be returned.

### Subsection content banner ###

Provider messages describing at a summary level how they have populated this subsection can be found [here](accessrecord_provider_variance.html#current-repeat-medications-subsection).

### Table construction requirements ###

Providers **MUST** adhere to the table construction requirements listed below:

- table header **MUST** be "Current Repeat Medications"
- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

### Table columns ###

Providers **MUST** return all the columns as described in the table below, ordered by `Last Issued` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Last Issued`  <i class="fa fa-sort-desc" aria-hidden="true">  |  Date of medication item last issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp; | Descriptive name of medication item (including dosage) | `free-text` |
| <center>3</center> | `Start Date` | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>4</center> | `Review Date` | Review date of medication issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Number Issued` | Number of times medication item issued | `integer` |
| <center>6</center> | `Max Issues` | Maximum number of issues allowed for medication item | `integer` |
| <center>7</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | `free-text` |





## Past medications ##

### Clinical narrative ###

A history view of drugs or other forms of medicines that have been used to treat or prevent disease for the patient.

### Purpose ###

The purpose of this subsection is to provide a historical view of repeat medications that the patient has been recorded to have been prescribed or taken. This informs the clinical decision-making process.
 
Where the medication was Cancelled (Acute) or Discontinued (Repeat), this *SHOULD* be included in the Details column as Cancelled followed by Date of Cancellation or Discontinued, followed by Date when discontinued.

### Date filter ###

A date filter is applicable for the Past Medications subsection (details of the banner message returned can be found [here](accessrecord_provider_variance.html#date-banner-message)):

- All relevant records **MUST** be returned according to the consumer-supplied date range
- If a date is not supplied all records **MUST** be returned

### Subsection content banner ###

There are no content banner messages for this subsection.

### Table construction requirements ###

Providers **MUST** adhere to the table construction requirements listed below:

- table header **MUST** be "Past Medications"
- table columns **MUST** be ordered left-to-right (1..N)
- table content **MUST NOT** be truncated

### Table columns ###

Providers **MUST** return all the columns as described in the table below, ordered by `Start Date` descending:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp;|
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date`   <i class="fa fa-sort-desc" aria-hidden="true"> | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp;| Descriptive name of medication item (inculding dosage) | `free-text` |
| <center>3</center> | `Type` | Type of medication issued (values `Repeat` or `Acute`) | `free-text` |
| <center>4</center> | `Last Issued` |  Date of medication item last issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Review Date` | Review date of medication issued | `dd-Mmm-yyyy` |
| <center>6</center> | `Number Issued` | Number of times medication item issued | `integer` |
| <center>7</center> | `Max Issues` | Maximum number of issues allowed for medication item | `integer` |
| <center>8</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  | `free-text` |


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/medications.html %}
