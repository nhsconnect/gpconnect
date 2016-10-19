---
title: Allergies
keywords: getcarerecord, view, section, allergies
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_allergies.html
summary: "Allergies HTML View."
---

## Allergies and Sensitivities ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ALL | Allergies and Sensitivities | Yes | Yes | Yes<sup>1</sup> | Yes |

<sup>1</sup> INPS have indicated they don't record end dates for allergies & sensitivities. Hence, no History view is possible.

Contains two sections:

 - [Current Allergies and Sensitivities](accessrecord_view_allergies.html#current-allergies-and-sensitivities)
 - [Historical Allergies and Sensitivities](accessrecord_view_allergies.html#historical-allergies-and-sensitivities)

## Current Allergies and Sensitivities ##

### Purpose ###

A list of current allergies and sensitivities related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned (i.e. no time limit/filtering is to be applied).

### Table Construction ###

- Table header SHALL be "Current Allergies and Sensitivities".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by start date descending (i.e. most recent date/time first).

### Table Columns ###

1. Start Date
	- the start date of the allergy or sensitivity.
2. Details
	- longer human readable free-text details for the allergy or sensitivity.

### HTML View ###

{% raw %}
```html
<div>
	<h2>Current Allergies and Sensitivities</h2>
	<table>
		<thead>
			<tr>
				<th>Start Date</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items">
				<td>{{item.start}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}

## Historical Allergies and Sensitivities ##

### Purpose ###

A list of historical allergies and sensitivities related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned (i.e. no time limit/filtering is to be applied).

### Table Construction ###

- Table header SHALL be "Historical Allergies and Sensitivities".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by start date descending (i.e. most recent date/time first).

### Table Columns ###

1. Start Date
	- the start date of the allergy or sensitivity.
2. End Date
	- the end date of the allergy or sensitivity. 
3. Details
	- longer human readable free-text details for the allergy or sensitivity.

### HTML View ###

{% raw %}
```html
<div>
	<h2>Historical Allergies and Sensitivities</h2>
	<table>
		<thead>
			<tr>
				<th>Start Date</th>
				<th>End Date</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items">
				<td>{{item.start}}</td>
				<td>{{item.end}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
