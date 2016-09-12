---
title: Problems
keywords: getcarerecord, view, section, problems
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_problems.html
summary: "Problems HTML View."
---

## Problems ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| PRB | Problems | Yes | Yes | Yes | Yes |

Contains two sections:

 - [Active Problems and Summary Items](accessrecord_view_problems.html#active-problems-and-summary-items)
 - [Inactive Problems and Summary Items](accessrecord_view_problems.html#inactive-problems-and-summary-items)

## Active Problems and Summary Items ##

### Purpose ###

A list of active problems and summary items related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned (i.e. no time limit/filtering is to be applied).

### Table Construction ###

- Table header SHALL be "Active Problems and Summary Items".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by start date descending (i.e. most recent date/time first).

### Table Columns ###

1. Start Date
	- the start date of the problem.
2. Entry
	- a short human readable free-text title for the problem.
3. Significance
	- the significance of the problem (i.e. Major or Minor).
4. Details

### HTML View ###

{% raw %}
```html
<div>
	<h2>Active Problems and Summary Items</h2>
	<table>
		<tbody>
			<tr>
				<th>Start Date</th>
				<th>Entry</th>
				<th>Significance</th>
				<th>Details</th>
			</tr>
			<tr ng-repeat="item in items">
				<td>{{item.start}}</td>
				<td>{{item.entry}}</td>
				<td>{{item.significance}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}

## Inactive Problems and Summary Items ##

### Purpose ###

A list of inactive (i.e. end dated) problems and summary items related to a patient ordered by date descending (i.e. most recent end? date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned with-in Consumer supplied date range.

### Table Construction ###

- Table header SHALL be "Inactive Problems and Summary Items".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by start date descending (i.e. most recent date/time first).

If no end dated records exist then the following 

### Table Columns ###

1. Start Date
	- the start date of the problem.
2. End Date
	- the end date of the problem.
3. Entry
	- a short human readable free-text title for the problem.
4. Significance
	- the significance of the problem (i.e. Major or Minor).
5. Details
	- longer human readable free-text details for the problem.

### HTML View ###

{% raw %}
```html
<div>
	<h2>Inactive Problems and Summary Items</h2>
	<table>
		<thead>
			<tr>
				<th>Start Date</th>
				<th>End Date</th>
				<th>Entry</th>
				<th>Significance</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items">
				<td>{{item.start}}</td>
				<td>{{item.end}}</td>
				<td>{{item.entry}}</td>
				<td>{{item.significance}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
