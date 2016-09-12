---
title: Immunisations
keywords: getcarerecord, view, section, immunisations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_immunisations.html
summary: "Immunisations HTML View."
---

## Immunisations ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| IMM | Immunisations | Yes | Yes | Yes | Yes |

### Purpose ###

A list of all immunisations related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned (i.e. no time limit/filtering is to be applied).

### Table Construction ###

- Table header SHALL be "Immunisations".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Date
	- the date of immunisation.
2. Vaccination 
3. Part
4. Contents
5. Details
	- longer human readable free-text details for the immunisation.

### HTML View ###

{% raw %}
```html
<div>
	<h2>Immunisations</h2>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>Vaccination</th>
				<th>Part</th>
				<th>Contents</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items">
				<td>{{item.date}}</td>
				<td>{{item.vaccination}}</td>
				<td>{{item.part}}</td>
				<td>{{item.contents}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
