---
title: Observations
keywords: getcarerecord, view, section, observations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_observations.html
summary: "Observations HTML View."
---

## Observations ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| OBS | Observations | Yes | Yes | Yes | Yes |

### Purpose ###

A list of all observations related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned with-in Consumer supplied date range.

{% include important.html content="In recent workshops the GP Principal suppliers have indicated this section will contain all clinical items that represent measurement data (i.e. blood pressure, temperature, heart rate etc.)." %}

### Table Construction ###

- Table header SHALL be "Observations".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Date
	- the date of observation.
2. Entry
	- a short human readable free-text title for the observation.
3. Value
4. Details
	- longer human readable free-text details for the observation.

### HTML View ###

{% raw %}
```html
<div>
	<h2>Observations</h2>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>Entry</th>
				<th>Value</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items">
				<td>{{item.date}}</td>
				<td>{{item.entry}}</td>
				<td>{{item.value}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
