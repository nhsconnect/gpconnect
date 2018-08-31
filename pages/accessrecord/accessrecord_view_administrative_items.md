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

<sup>1</sup> EMIS have indicated they can't support extracting administrative items.

### Clinical narrative ###

These include tasks such as scheduling and administering clinical care encounters, Clinical communication with other care organisations, administering and monitoring of critical safety processes such as repeat medication administration and call/recall for care.

### Purpose ###

The purpose of this section is to provide information for the health care teams on the recorded management and administrative processes and activity to support safe and effective care.

### Sections and subsections ###

There is only a single main section for Administrative Items with no subsections.

### Date filter ###

A date filter is applicable for the Administrative Items section.

### Section content banner ###

Providers message describing at a summary level how they have populated this section:

<div class="panel-group" id="accordion">
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseOne">EMIS banner content (click here to expand/collapse) </a>
						</div>
                        <div id="collapseOne" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>Always displays this text:</b></p>
									<ul>
										<li>This system does not support retrieval of Administrative Items data.</li>
										<li>This data may still exist in the source system.</li>
									</ul>
                            </div>
                        </div>
                    </div>
                    <!-- /.panel -->
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseTwo">TPP banner content (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseTwo" class="panel-collapse collapse noCrossRef">
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
                        </div>
                    </div>
                    <!-- /.panel -->
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseThree">INPS banner content (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseThree" class="panel-collapse collapse noCrossRef">
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
                    </div>
                    <!-- /.panel -->
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseFour">MicroTest banner content (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseFour" class="panel-collapse collapse">
                            <div class="panel-body">
								<p><b>Always displays this text:</b></p>
									<ul>
										<li>Contains non-clinical items - including, but not limited to, administrative, occupational, social context, carer information, communications preferences, legal information, learning disability, advance decisions etc.</li>
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
                    </div>
</div>


### Table construction requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Administrative Items".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (i.e. most recent date/time first).


### Table columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` | The date of the administrative item | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry` | A short human readable free-text title for the administrative item | `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the administrative item, codes such as READ or SNOMED **SHALL NOT** be included. | `free-text` |



### HTML view ###

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
			<tr ng-repeat="item in items">
				<td>{{item.date}}</td>
				<td>{{item.entry}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}

{% include custominfocallout.html content="**Important:** AngularJS tags (e.g ng-repeat) are present merely to indicate to a developer the structure of the table content. Presence of these tags are not intended to imply use of any specific technology." type="warning" %}

## Example view ##

<p data-height="400" data-theme-id="light" data-slug-hash="QBoqNR" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Administrative Items" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/QBoqNR/">Allergies</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/QBoqNR) for example of using AngularJS to generate table content" %}
