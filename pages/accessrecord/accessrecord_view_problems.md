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
|Microtest|  Significance represents Priority of High, Medium, Low <br> (maps to Major, Routine and Minor respectively) |


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

The following content highlights the expected HTML tags and format providers SHALL use when generating the HTML content:

{% raw %}
```html
<div>
	<h2>Active Problems and Issues</h2>
	<table>
		<thead>
			<tr>
				<th>Start Date</th>
				<th>Entry</th>
				<th>Significance</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr> <!-- The <tr>...</tr> element will repeat for each problem or issue -->
				<td>{{Problem Start Date}}</td>
				<td>{{Problem Entry}}</td>
				<td>{{Problem Significance}}</td>
				<td>{{Problem Details}}</td>
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

<br/>

Provider systems not supporting Inactive Problems (e.g. INPS) SHALL display a message in the Section Banner to indicate:

- Inactive Problems are not supported as in the [HTML Implementation Guide - Not Supported](https://nhsconnect.github.io/gpconnect/accessrecord_development_html_implementation_guide.html#not-supported
) section.
- That any Problems and Issues recorded for the Patient are included in the Active Problems and Issues section.

Provider systems that do support Inactive Problems, but when no records exist for the requested Patient SHALL display the standard [HTML Implementation Guide - Supported But Hasn't Been Recorded](https://nhsconnect.github.io/gpconnect/accessrecord_development_html_implementation_guide.html#supported-but-hasnt-been-recorded) message.

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

The following content highlights the expected HTML tags and format providers SHALL use when generating the HTML content:

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
			<tr> <!-- The <tr>...</tr> element will repeat for each problem or issue -->
				<td>{{Problem Start Date}}</td>
				<td>{{Problem End Date}}</td>
				<td>{{Problem Entry}}</td>
				<td>{{Problem Significance}}</td>
				<td>{{Problem Details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
