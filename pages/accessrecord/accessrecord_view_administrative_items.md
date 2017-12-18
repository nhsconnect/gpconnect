---
title: Administrative Items
keywords: getcarerecord, view, section, administrative items
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_administrative_items.html
summary: "Administrative Items HTML View."
---

## Administrative Items ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ADM | Administrative Items | Yes | No<sup>1</sup> | Yes | Yes |

<sup>1</sup> EMIS have indicated they can't support extracting administrative items for Stage 1 of the Maturity Model.

### Purpose ###

A list of all coded administrative items related to a patient ordered by date descending (i.e. most recent date/time first).

{% include tip.html content="This may contain information about letters/mail merging, appointment DNAs, consent recording and other administrative terms recorded by the GP." %}

### Structured Data ###

{% include todo.html content="Structured data mappings to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Date Horizon ###

All relevant<sup>^</sup> records SHALL be returned with-in Consumer supplied date range.

<sup>^</sup> For GP Connect FoT relevant records are all coded items held in the GP CIS system under the READ code hierarchy for administrative content.


### Section Banner Content Message ###

Providers message describing at a summary level how they have populated this section, to include the following:

| Provider | Message |
| ------------ | ------------ |-
| EMIS|  |
| TPP|   |
| INPS|  |
|Microtest| Chapter Heading - Read 2 to distinguish the administrative codes (those starting '9' (Administration) and '0' (Occupation)   |


### Table Construction ###

- Table header SHALL be "Administrative Items".
- Table columns SHALL be ordered left-to-right (1..N).
- Table content SHALL NOT be truncated.
- Table rows SHALL be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

1. Date
	- the date of administrative item.
2. Entry<sup>1</sup>
	- a short free-text human readable description of the administrative item. 
3. Details<sup>1</sup>
	- a longer free-text human readable description of the administrative item.  

<sup>1</sup> Codes such as READ or SNOMED SHALL not be included.

### HTML View ###

The following content highlights the expected HTML tags and format providers SHALL use when generating the HTML content:

{% raw %}
```html
<div>
	<h2>Administrative Items</h2>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>Entry</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr> <!-- The <tr>...</tr> element will repeat for each administrative item -->
				<td>{{Administrative Item Date}}</td>
				<td>{{Administrative Item Entry}}</td>
				<td>{{Administrative Item Details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}
