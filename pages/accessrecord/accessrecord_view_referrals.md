---
title: Referrals
keywords: getcarerecord, view, section, referrals
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_referrals.html
summary: "Referrals HTML View."
---

## Referrals ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| REF | Referrals | Yes | Yes | Yes | Yes |

### Purpose ###

A list of all referrals related to a patient ordered by date descending (i.e. most recent date/time first).

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant records SHALL be returned with-in Consumer supplied date range.

### Table Construction ###

- Table header SHALL be "Referrals".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Date
	- the date of referral.
2. From 
3. To
4. Priority
5. Details
	- longer human readable free-text details for the medication item.

### HTML View ###

The following content highlights the expected HTML tags and format providers SHALL use when generating the HTML content:

{% raw %}
```html
<div>
	<h2>Referrals</h2>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>From</th>
				<th>To</th>
				<th>Priority</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr> <!-- The <tr>...</tr> element will repeat for each referral -->
				<td>{{Referral Date}}</td>
				<td>{{Referral From}}</td>
				<td>{{Referral To}}</td>
				<td>{{Referral Priority}}</td>
				<td>{{Referral Details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
