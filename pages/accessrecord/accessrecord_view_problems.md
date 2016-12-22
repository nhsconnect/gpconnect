---
title: Problems and Issues
keywords: getcarerecord, view, section, problems
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_problems.html
summary: "Problems HTML View."
---

## Problems and Issues ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| PRB | Problems and Issues | Yes | Yes | Yes | Yes |

Contains two sections:

 - [Active Problems and Issues](accessrecord_view_problems.html#active-problems-and-issues)
 - [Inactive Problems and Issues](accessrecord_view_problems.html#inactive-problems-and-issues)


### Section Banner Content Message ###

Providers message describing at a summary level how they have populated this section, to include the following:

| Provider | Message |
| ------------ | ------------ |-
| EMIS|  |
| TPP| Section includes Summary Items  |
| INPS| All problems included in Active Section |
|Microtest|  Significance represents Priority of High, Medium, Low  |


## Active Problems and Issues ##

### Purpose ###

A list of active problems and issues related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned (i.e. no time limit/filtering is to be applied).

### Table Construction ###

- Table header SHALL be "Active Problems and Issues".
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
	<h2>Active Problems and Issues</h2>
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

## Inactive Problems and Issues ##

### Purpose ###

A list of inactive (i.e. end dated) problems and issues related to a patient ordered by date descending (i.e. most recent end? date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned with-in Consumer supplied date range.

### Table Construction ###

- Table header SHALL be "Inactive Problems and Issues".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by start date descending (i.e. most recent date/time first).

If the Provider system does not support Inactive Problems (INPS), then display a message in the Section Banner to indicate 

1. as in the HTML Implementation Guide page
https://nhsconnect.github.io/gpconnect/accessrecord_development_html_implementation_guide.html#not-supported

2. that any Problems and Issues recorded for the Patient are included in the Active Problems and Issues section

If the Provider system supports Inactive Problems, but no records exist for the Patient requested, then provide the standard message as specified in the HTML Implementation Guide

https://nhsconnect.github.io/gpconnect/accessrecord_development_html_implementation_guide.html#supported-but-hasnt-been-recorded

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
	<h2>Inactive Problems and Issues</h2>
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
