---
title: Medications
keywords: getcarerecord, view, section, medications
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_medications.html
summary: "Medications HTML View."
---

## Medications ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| MED | Medications | Yes | Yes | Yes | Yes |

Contains three sections:

 - [Current Medication Issues](accessrecord_view_medications.html#current-medication-issues)
 - [Current Repeat Medications](accessrecord_view_medications.html#current-repeat-medications)
 - [Past Medications](accessrecord_view_medications.html#past-medications)


### Section Banner Content Message ###

Providers message describing at a summary level how they have populated this section, and also the warning message where medications prescribed elsewhere have been excluded:

| Provider | Message |
| ------------ | ------------ |
| EMIS| EMIS message here <br> Medications prescribed elsewhere have been excluded|
| TPP|  TPP message here <br> Medications prescribed elsewhere have been excluded|
| INPS| INPS message here <br> Medications prescribed elsewhere have been excluded|
| Microtest| Microtest message here <br> Medications prescribed elsewhere have been excluded|


## Current Medication Issues ##

### Purpose ###

A list of all current acute and repeat medications issued to a patient ordered by date descending (i.e. most recent date/time first).

{% include warning.html content="The current medications list will only contain those items prescribed by the patient's current GP organization. Hence, if the patient has been issued prescriptions elsewhere or has recently moved GP practice then this list may not be complete." %}

### Date Horizon ###

All relevant records **SHALL** be returned (i.e. no time limit/filtering is to be applied).

### Sub Section Banner Content Message ###

Providers message describing at a summary level how they have populated this section.

| Provider | Message |
| ------------ | ------------ |
| EMIS| message to be added here|
| TPP|  message to be added here|
| INPS| message to be added here|
| Microtest| message to be added here|

### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Current Medication Issues".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date` | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp;| Descriptive name of medication item (inculding dosage) | `free-text` |
| <center>3</center> | `Type` | Type of medication issued | `Repeat` <br> `Acute` |
| <center>4</center> | `Scheduled End` | Scheduled end date of medication issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Days Duration` | Duration of medication issued | `integer` |
| <center>6</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | `free-text` |

Provider systems **SHALL** include all relevant clinical content in the `Details` free-text field. As a minimum the free-text narrative **SHALL** include these items: <br>
- `MedicationOrder.medication.code`
- `MedicationOrder.dosageInstruction.dose[x]`
- `MedicationOrder.dosageInstruction.schedule[x]`
- `MedicationOrder.dosageInstruction.rate`
- `MedicationOrder.dosageInstruction.maxDosePerPeriod`


### HTML View ###

{% raw %}
```html
<div ng-controller="ctrl">
	<h3>Current Medication Issues</h3>
		<table class="table">
			<thead>
				<tr>
					<th class="col-sm-2">Start Date</th>
					<th class="col-sm-2">Medication Item</th>
					<th class="col-sm-2">Type</th>
					<th class="col-sm-2">Scheduled End</th>
					<th class="col-sm-2">Days Duration</th>
					<th class="col-sm-2">Details</th>
				</tr>
			</thead>
				<tr ng-repeat="x in records" class="table">
					<td class="col-sm-2">{{x.date}}</td>
					<td class="col-sm-2">{{x.drug}}</td>
					<td class="col-sm-2">{{x.type}}</td>
					<td class="col-sm-2">{{x.scheduledEnd}}</td>
					<td class="col-sm-2">{{x.daysDuration}}</td>
					<td class="col-sm-2">{{x.details}}</td>
				</tr>
		</table>
</div>
```
{% endraw %}

## Current Repeat Medications##

### Purpose ###

A list of all current repeat medications issued to a patient ordered by date descending (i.e. most recent Last Issued date/time first).

### Date Horizon ###

All relevant records **SHALL** be returned (i.e. no time limit/filtering is to be applied).

### Sub Section Banner Content Message ###

Providers message describing at a summary level how they have populated this section.

| Provider | Message |
| ------------ | ------------ |
| EMIS| message to be added here|
| TPP|  message to be added here|
| INPS| message to be added here|
| Microtest| message to be added here|

### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Current Repeat Medications".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by Last Issued date descending (i.e. most recent date/time first).

### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Last Issued` |  Date of medication item last issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp; | Descriptive name of medication item (inculding dosage) | `free-text` |
| <center>3</center> | `Start Date` | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>4</center> | `Review Date` | Review date of medication issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Number Issued` | Number of times medication item issued | `integer` |
| <center>6</center> | `Max Issues` | Maximum number of issues allowed for medication item | `integer` |
| <center>7</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | `free-text` |

{% include todo.html content="Number Issued, & Max Issues to be reviewed given Provider variances "%}

### HTML View ###

{% raw %}
```html
<div ng-controller="ctrl">
	<h3>Current Repeat Medications</h3>
		<table class="table">
			<thead>
				<tr>
					<th class="col-sm-2">Last Issued</th>
					<th class="col-sm-2">Medication Item</th>
					<th class="col-sm-2">Start Date</th>
					<th class="col-sm-2">Review Date</th>
					<th class="col-sm-2">Number Issued</th>
					<th class="col-sm-2">Max Issues</th>
					<th class="col-sm-2">Details</th>
				</tr>
			</thead>
				<tr ng-repeat="x in records1" class="table">
					<td class="col-sm-2">{{x.lastIssued}}</td>
					<td class="col-sm-2">{{x.drug}}</td>
					<td class="col-sm-2">{{x.start}}</td>
					<td class="col-sm-2">{{x.review}}</td>
					<td class="col-sm-2">{{x.numberIssued}}</td>
					<td class="col-sm-2">{{x.maxIssues}}</td>
					<td class="col-sm-2">{{x.details}}</td>
				</tr>
		</table>
</div>
```
{% endraw %}

## Past Medications ##

### Purpose ###

A list of all past medications, issued to a patient ordered by date descending (i.e. most recent date/time first). The type will include Acute, or Repeat. 

Where the medication was cancelled (Acute) or Discontinued (Repeat), this should be included in the Details column as Cancelled followed by Date of Cancellation or Discontinued, followed by Date when discontinued.

### Date Horizon ###

All relevant records **SHALL** be returned according to consumer-supplied date range.

### Sub Section Banner Content Message ###

Providers message describing at a summary level how they have populated this section.

{% include important.html content="For Providers not able to differentiate between prescriptions ended 'normally', and those discontinued, or cancelled, before the original prescribed end date, this can be mitigated by Banner description:
<br><br>
<b>Past Medications may include prescriptions which have been cancelled or discontinued before the original prescribed end date</b>" %}

| Provider | Message |
| ------------ | ------------ |
| EMIS| message to be added here|
| TPP|  message to be added here|
| INPS| message to be added here|
| Microtest| message to be added here|

### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Past Medications".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp;|
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date` | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp;| Descriptive name of medication item (inculding dosage) | `free-text` |
| <center>3</center> | `Type` | Type of medication issued (values `Repeat` or `Acute`) | `free-text` |
| <center>4</center> | `Last Issued` |  Date of medication item last issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Review Date` | Review date of medication issued | `dd-Mmm-yyyy` |
| <center>6</center> | `Number Issued` | Number of times medication item issued | `integer` |
| <center>7</center> | `Max Issues` | Maximum number of issues allowed for medication item | `integer` |
| <center>8</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  | `free-text` |

{% include todo.html content="Number Issued, & Max Issues to be reviewed given Provider variances "%}

### HTML View ###

{% raw %}
```html
<div ng-controller="ctrl">
	<h3>Past Medications</h3>
		<table class="table">
			<thead>
				<tr>
					<th class="col-sm-2">Start Date</th>
					<th class="col-sm-2">Medication Item</th>
					<th class="col-sm-2">Type</th>
					<th class="col-sm-2">Last Issued</th>
					<th class="col-sm-2">Review Date</th>
					<th class="col-sm-2">Number Issued</th>
					<th class="col-sm-2">Max Issues</th>
					<th class="col-sm-2">Details</th>
				</tr>
			</thead>
				<tr ng-repeat="x in records2" class="table">
					<td class="col-sm-2">{{x.start}}</td>
					<td class="col-sm-2">{{x.drug}}</td>
					<td class="col-sm-2">{{x.type}}</td>
					<td class="col-sm-2">{{x.lastIssued}}</td>
					<td class="col-sm-2">{{x.review}}</td>
					<td class="col-sm-2">{{x.numberIssued}}</td>
					<td class="col-sm-2">{{x.maxIssues}}</td>
					<td class="col-sm-2">{{x.details}}</td>
				</tr>
		</table>
</div>
```
{% endraw %}

{% include important.html content="AngularJS tags (e.g ng-repeat) are present merely to indicate to a developer the structure of the table content. Presence of these tags are not intended to imply use of any specific technology." %}

## Example View ##

<p data-height="1865" data-theme-id="light" data-slug-hash="GyJROK" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Medications" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/GyJROK/">Medications</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/GyJROK) for example of using AngularJS to generate table content" %}
