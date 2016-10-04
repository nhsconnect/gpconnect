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
 - [Current Medication Repeats](accessrecord_view_medications.html#current-medication-repeats)
 - [Past Medications](accessrecord_view_medications.html#past-medications)

## Current Medication Issues ##

### Purpose ###

A list of all current acute and repeat medications issued to a patient ordered by date descending (i.e. most recent date/time first).

{% include warning.html content="The current medications list will only contain those items prescribed by the patient's current GP organization. Hence, if the patient has been issued prescriptions elsewhere or has recently moved GP practice then this list may not be complete." %}

### Structured Data ###

| Logical Item | FHIR Mapping | Narrative Item |
|---------------|------------|----------------|
| Medication Material |	MedicationOrder.medication.code | M |
| Medication Start and End Time	| MedicationOrder.dosageInstruction.schedule[x] | - |
| Medication Dosage units |	MedicationOrder.dosageInstruction.dose[x] | M |
| Medication Schedule(when/how often) | MedicationOrder.dosageInstruction.schedule[x] | M |
| Medication Dosage Rate | MedicationOrder.dosageInstruction.rate | M |
| Max Medication Dosage quantity | MedicationOrder.dosageInstruction.maxDosePerPeriod | M |

### Date Horizon ###

All relevant records SHALL be returned with-in Consumer supplied date range.

### Table Construction ###

- Table header SHALL be "Current Medication Issues".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Start Date
2. Drug
3. Type
 - i.e. Repeat or Acute
4. Scheduled End
5. Days Duration
6. Details<sup>1</sup>
	- longer human readable free-text details for the medication item.

Provider systems SHALL include all relevant clinical content in the `Details` free-text field. As a minimum the free-text narrative SHALL include the items marked as mandatory in `Narrative Item` column of the `Structured Data` table.

### HTML View ###

{% raw %}
```html
<div>
	<h2>Current Medication Issues</h2>
	<table>
		<thead>
			<tr>
				<th>Start Date</th>
				<th>Drug</th>
				<th>Type</th>
				<th>Scheduled End</th>
				<th>Days Duration</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items">
				<td>{{item.start}}</td>
				<td>{{item.drug}}</td>
				<td>{{item.type}}</td>
				<td>{{item.scheduledEnd}}</td>
				<td>{{item.daysDuration}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}

## Current Medication Repeats ##

### Purpose ###

A list of all current repeat medications issued to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned (i.e. no time limit/filtering is to be applied).

### Table Construction ###

- Table header SHALL be "Current Medication Repeats".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Start Date
2. Drug
3. Last Issued
4. Review Date
5. Number Issued
6. Max Issues
7. Details
	- longer human readable free-text details for the medication item.

### HTML View ###

{% raw %}
```html
<div>
	<h2>Current Medication Repeats</h2>
	<table>
		<tbody>
			<tr>
				<th>Start Date</th>
				<th>Drug</th>
				<th>Last Issued</th>
				<th>Review Date</th>
				<th>Number Issued</th>
				<th>Max Issues</th>
				<th>Details</th>
			</tr>
			<tr ng-repeat="item in items">
				<td>{{item.start}}</td>
				<td>{{item.drug}}</td>
				<td>{{item.lastIssued}}</td>
				<td>{{item.review}}</td>
				<td>{{item.numberIssued}}</td>
				<td>{{item.maxIssues}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}

## Past Medications ##

### Purpose ###

A list of all past medications issued to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned (i.e. no time limit/filtering is to be applied).

### Table Construction ###

- Table header SHALL be "Past Medications".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Start Date
2. Drug
3. Type
	- i.e. Repeat or Acute
4. Last Issued
5. Review Date
6. Number Issued
7. Max Issued
8. Details

### HTML View ###

{% raw %}
```html
<div>
	<h2>Past Medications</h2>
	<table>
		<tbody>
			<tr>
				<th>Start Date</th>
				<th>Drug</th>
				<th>Type</th>
				<th>Last Issued</th>
				<th>Review Date</th>
				<th>Number Issued</th>
				<th>Max Issues</th>
				<th>Details</th>
			</tr>
			<tr ng-repeat="item in items">
				<td>{{item.start}}</td>
				<td>{{item.drug}}</td>
				<td>{{item.type}}</td>
				<td>{{item.lastIssued}}</td>
				<td>{{item.review}}</td>
				<td>{{item.numberIssued}}</td>
				<td>{{item.maxIssues}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
