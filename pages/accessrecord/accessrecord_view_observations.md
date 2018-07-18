---
title: Observations
keywords: getcarerecord, view, section, observations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_observations.html
summary: "Observations HTML View."
---

## Observations ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| OBS | Observations | Yes | Yes | Yes | Yes |

### Clinical Narrative ###

A clinical observation is a repeatable data element recorded by health professionals in the course of assessment or care of their patients or clients. Examples include, blood pressure measurement, weight, height or temperature.

### Purpose ###

The purpose of this section is to enable the clinician to view and compare chronologically data recorded in structured form pertaining to a patient’s physical condition.

### Sections and Subsections ###

There is only a single main section for Observations with no subsections.

### Date Filter ###

A date filter is applicable for the Observations section.

### Section Banner Content ###

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
										<li>Contains observations with numeric and other measurement ranges.</li>
									</ul>
								<p><b>Only displayed if a date filter is applied:</b></p>
									<ul>
										<li>For the selected date range DD-MMM-YYYY to DD-MMM-YYYY subject to patient preferences and/or RCGP exclusions.</li>
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
								<p><b>Only displayed if a date filter is not applied:</b></p>
									<ul>
										<li>All relevant items subject to patient preferences and/or RCGP exclusions.</li>
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
										<li>Contains Observations with numeric and other measurement ranges.</li>
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


### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Observations".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (i.e. most recent date/time first).


### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` | The date of the observation | `dd-Mmm-yyyy` |
| <center>2</center> | `Entry` | A short human readable free-text title for the observation | `free-text` |
| <center>3</center> | `Value` | Value and range (where available) of the observation | `free-text` |
| <center>4</center> | `Details` | Longer human readable details for the observation | `free-text` |


{% include custominfocallout.html content="**Important:** In recent workshops the GP Principal suppliers have indicated this section will contain all clinical items that represent measurement data (i.e. blood pressure, temperature, heart rate etc.)." type="warning" %}
	
	
### HTML View ###

{% raw %}
```html
<div ng-controller="ctrl">
	<h3>Active Problems and Issues</h3>
	<table class="table">
		<thead>
			<tr>
				<th class="col-sm-2">Date</th>
				<th class="col-sm-2">Entry</th>
				<th class="col-sm-2">Value</th>
				<th class="col-sm-2">Details</th>
			</tr>
		</thead>
			<tr ng-repeat="x in records" class="table">
				<td class="col-sm-2">{{x.date}}</td>
				<td class="col-sm-2">{{x.entry}}</td>
				<td class="col-sm-2">{{x.value}}</td>
				<td class="col-sm-2">{{x.details}}</td>
			</tr>
	</table>
</div>
```
{% endraw %}

{% include custominfocallout.html content="**Important:** AngularJS tags (e.g ng-repeat) are present merely to indicate to a developer the structure of the table content. Presence of these tags are not intended to imply use of any specific technology." type="warning" %}

## Example View ##

<p data-height="425" data-theme-id="light" data-slug-hash="aENJMQ" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Observations" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/aENJMQ/">Observations</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/aENJMQ) for example of using AngularJS to generate table content" %}