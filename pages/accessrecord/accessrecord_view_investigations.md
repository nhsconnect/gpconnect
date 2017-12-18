---
title: Investigations
keywords: getcarerecord, view, section, investigations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_investigations.html
summary: "Investigations HTML View."
---

## Investigations ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| INV | Investigations | Yes<sup>1</sup> | No | No | No |

<sup>1</sup> The Investigations section can currently only be provided by a single GP principal system supplier (i.e. TPP).

{% include todo.html content="The Investigations section to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Purpose ###

A list of all investigations related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned with-in Consumer supplied date range.

### Table Construction ###

- Table header SHALL be "Investigations".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Date
	- the date of the investigation.
2. Title
	- a short human readable free-text title for the investigation.
3. Details
	- longer human readable free-text details for the investigation.

### HTML View ###

The following content highlights the expected HTML tags and format providers SHALL use when generating the HTML content:

{% raw %}
```html
<div>
	<h2>Investigations</h2>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>Title</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr> <!-- The <tr>...</tr> element will repeat for each investigation -->
				<td>{{Investigation Date}}</td>
				<td>{{Investigation Title}}</td>
				<td>{{Investigation Details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
