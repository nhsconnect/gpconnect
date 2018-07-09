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


### Clinical Narrative ###

Items of information relating to the care, health or wellbeing of the patient. Examples of this type of information are: childhood and travel vaccinations, screening information and past medical history. It does not include administrative items such as invitations for health-related information.


### Purpose ###

The purpose of supplying Clinical Items within GP Connect is to allow a clinician to view a history of items relating to the health and wellbeing of a patient.

The list of clinical items is based on a consumer supplied date range and is ordered by date descending (i.e. most recent date/time first).


### Sections and Subsections ###

There is only a single main section for Clinical Items with no subsections.


### Date Filter ###

A date filter is applicable for the Clinical Items section.


### Section Banner Content Message ###

Providers message describing at a summary level how they have populated this section:

<div class="panel panel-default">
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> EMIS banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
		<p><b>Always displays this text:</b></p>
			<ul>
				<li>Contains coded clinical items relating to a patients care e.g. procedures, test results, conditions.</li>
			</ul>
		<p><b>Only displayed if a date filter is applied:</b></p>
			<ul>
				<li>For the selected date range DD-MMM-YYYY to DD-MMM-YYYY subject to patient preferences and/or RCGP exclusions.</li>
			</ul>
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> TPP banner content (click here to expand/collapse)</p>
  </div>
  <div class="panel-body">
		<p><b>If data is hidden due to sharing preferences (only shows if data is contained within current date range):</b></p>
			<ul>
				<li>Some patient data is hidden by sharing rules. The data in this section may be incomplete.</li>
			</ul>
		<p><b>Displayed dependent on date range:</b></p>
			<ul>
				<li>Data for the period DD-MMM-YYYY to DD-MMM-YYYY.</li>
				<li>All Data Items from DD-MMM-YYYY.</li>
				<li>All Data Items until DD-MMM-YYYY.</li>
				<li>All relevant items.</li>
			</ul>
		<p><b>If GP2GP in progress:</b></p>
			<ul>
				<li>Record is in transit and may be incomplete.</li>
			</ul> 
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> INPS banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
    	<p><b>Always displays this text:</b></p>
			<ul>
				<li>All relevant items subject to patient preferences and/or RCGP exclusions.</li>
				<li>Contains clinical items including, but not limited to, Procedures, Diagnoses, Symptoms, Conditions; may include items included in other sections such as Linked Problems.</li>
			</ul>
		<p><b>Only displayed if a date filter is applied:</b></p>
			<ul>
				<li>For the period DD-MMM-YYYY to DD-MMM-YYYY.</li>
			</ul>
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> MicroTest banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
    	<p><b>Always displays this text:</b></p>
			<ul>
				<li>Contains clinical items including, but not limited to, Procedures, Diagnoses, Symptoms, Conditions; may include items included in other sections such as Linked Problems.</li>
			</ul>
		<p><b>Only displayed if a date filter is not applied:</b></p>
			<ul>
				<li>All relevant items.</li>
			</ul>	
		<p><b>Only displayed if a date filter is applied:</b></p>
			<ul>
				<li>For the period DD-MMM-YYYY to DD-MMM-YYYY.</li>
			</ul>
  </div>
</div>


### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Clinical Items".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (i.e. most recent date/time first).


### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` | The date of entry of the clinical item | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry`| A short human readable title for the clinical item | `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the clinical item | `free-text` |


### Section Business Rules ###

| Supplier | Business Rules |
|----------|----------------|
| EMIS | N/A |
| TPP | Message to include indication of inclusion of Practice-specific codes |
| INPS | Message to include meaningful interpretation of Read Chapter 1 with Chapters A - Z |
| MicroTest | Message to include meaningful interpretation of items excluding Read Code Chapter 2 and Codes starting 9 and 0 |


### HTML View ###

{% raw %}
```html
<div ng-app="ngRepeat" ng-controller="repeatController">
	<h2>Clinical Items</h2>
	<table class="table">
		<thead>
			<tr>
				<th class="col-sm-2">Date</th>
				<th class="col-sm-2">Entry</th>
				<th class="col-sm-2">Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items" class="table">
				<td>{{item.date}}</td>
				<td>{{item.entry}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}

{% include important.html content="AngularJS tags (e.g ng-repeat) are present merely to indicate to a developer the structure of the table content. Presence of these tags are not intended to imply use of any specific technology." %} 

## Example View ##

<p data-height="265" data-theme-id="light" data-slug-hash="ooQORw" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Clinical Items" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/ooQORw/">Clinical Items</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/ooQORw) for example of using AngularJS to generate table content" %}
