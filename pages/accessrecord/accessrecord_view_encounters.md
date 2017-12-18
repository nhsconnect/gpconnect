---
title: Encounters
keywords: getcarerecord, view, section, encounters
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_encounters.html
summary: "Encounters HTML View."
---

## Encounters ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ENC | Encounters | Yes | Yes | Yes | Yes |

### Purpose ###

A list of encounters related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned with-in Consumer supplied date range.

### Table Construction ###

- Table header SHALL be "Encounters".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Date
	- the date of the encounter.
2. Title<sup>1</sup>
	- a short human readable free-text title for the encounter.
3. Details
	- longer human readable free-text details for the encounter.

<sup>1</sup> To be composed of a subset of the `Practitioner` and `Organization` details linked to the encounter (i.e. *Miss Tanya Turnpike (Practice Nurse) - Dr Johnson and Partners (J12345)*)

### HTML View ###

The following content highlights the expected HTML tags and format providers SHALL use when generating the HTML content:

{% raw %}
```html
<div>
	<h2>Encounters</h2>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>Title</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr> <!-- The <tr>...</tr> element will repeat for each encounter -->
				<td>{{Encounter Date}}</td>
				<td>{{Encounter Title}}</td>
				<td>{{Encounter Details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}

{% include codepen.html slug-hash="rrNKWb" %}

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/rrNKWb) for example of using AngularJS to generate table content" %}