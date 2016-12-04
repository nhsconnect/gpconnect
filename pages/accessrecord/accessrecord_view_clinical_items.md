---
title: Clinical Items
keywords: getcarerecord, view, section, clinical items
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_clinical_items.html
summary: "Clinical Items HTML View."
---

## Clinical Items ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| CLI | Clinical Items | Yes | Yes | Yes | Yes |

### Purpose ###

A list of clinical items related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned with-in Consumer supplied date range.

###Clinical Items Section Banner Content Message###

Providers to provide message describing at a summary level how they have populated this section, including reference to items identified as Diagnoses, Procedures, Symptoms
 
 
 | Provider | Message |
 | -------- | ------- |
 | EMIS |    |
 | TPP |  Message to indicate inclusion of Practice-specific codes |
 | INPS| Message to include Read Chapter 1 with Chapters A - Z |
 |Microtest| Message to include Items excluding Read Code Chapter 2 and Codes starting 9 and 0 |



### Table Construction ###

- Table header SHALL be "Clinical Items".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by start date descending (i.e. most recent date/time first).

### Table Columns ###

1. Date
	- the date of entry of the clinical item.
2. Entry
	- a short human readable free-text title for the clinical item.
3. Details
	- longer human readable free-text details for the clinical item.

### HTML View ###

{% raw %}
```html
<div>
	<h2>Clinical Items</h2>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>Entry</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items">
				<td>{{item.date}}</td>
				<td>{{item.entry}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
