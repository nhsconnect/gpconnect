---
title: Encounters
keywords: getcarerecord, view, section, encounters
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_encounters.html
summary: "Encounters HTML view"
---

## Encounters ##

| Section Code | Section Name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| ENC | Encounters | Yes | Yes | Yes | Yes |


### Clinical narrative ###

An encounter is an interaction between a patient and a health care professional (HCP) that is recorded on the patient record. This can include:

- Planned encounters - such as pre-arranged Appointments with a GP
- Unplanned encounters - such as at an out of hours clinic and those unrecorded through appointment module(s)
- Direct encounters - such as a face-to-face session with a GP
- Indirect encounters - such as a GP reviewing and updating a patient record on receipt of some test results


### Purpose ###

The purpose of supplying encounters within GP Connect is to allow a clinician to view a history of a patient’s interactions with a clinician or an HCP.

The list of encounters is based on a consumer-supplied date range and is ordered by date descending (that is, most recent date/time first).

Data will include the date, the practitioner (and role) and organisation (and code), then a block of free text which will include any free text narrative recorded during the consultation and some basic details of related activities will also be shown (for example - meds prescribed, procedures performed, diagnosis recorded, examinations, history recorded, care plans created, allergies or sensitivities recorded).


### Sections and subsections ###

There is a single main section for encounters with no subsections.


### Date filter ###

A date filter is applicable for the encounters section.


### Section content banner ###

Provider's message describing at a summary level how they have populated this section.

<div class="panel-group" id="accordion">
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseOne">EMIS banner content (click here to expand/collapse) </a>
						</div>
                        <div id="collapseOne" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>Always displays this text:</b></p>
									<ul>
										<li>Contains information recorded during consultations with the patient.</li>
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
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseThree">Vision banner content (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseThree" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>Always displays this text:</b></p>
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
										<li>Contains Appointment information and any related information recorded during the consultation; related items may also occur in other sections.</li>
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

- Table header **SHALL** be "Encounters".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (that is, most recent date/time first).


### Table columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details |
| ----- | ---- | ----------- | ------------- |
| <center>1</center> | `Date` | The date of the encounter | `dd-Mmm-yyyy` |
| <center>2</center> | `Title`| A short human readable title for the encounter, to be composed of a subset of the `Practitioner` and `Organization` details linked to the encounter| `free-text` |
| <center>3</center> | `Details` | Longer human readable details for the encounter | `free-text` |


### HTML view ###

{% raw %}
```html
<div ng-controller="ctrl">
	<h2>Encounters</h2>
	<table class="table">
		<thead>
			<tr>
				<th class="col-sm-2">Date</th>
				<th class="col-sm-2">Title</th>
				<th class="col-sm-2">Details</th>
			</tr>
		</thead>
			<tr ng-repeat="x in records"  class="angular-with-newlines">
				<td class="col-sm-2">{{x.date}}</td>
				<td class="col-sm-2">{{x.title}}</td>
				<td class="col-sm-2">{{x.details}}</td>
			</tr>
	</table>
</div>
```
{% endraw %}

{% include custominfocallout.html content="**Important:** AngularJS tags (for example, ng-repeat) are present merely to indicate to a developer the structure of the table content. Presence of these tags are not intended to imply use of any specific technology." type="warning" %}

## Example view ##

<p data-height="930" data-theme-id="light" data-slug-hash="JMdYpm" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Encounters" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/JMdYpm/">Encounters</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/JMdYpm) for an example of using AngularJS to generate table content" %}
