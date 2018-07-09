---
title: Medications
keywords: getcarerecord, view, section, medications
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_medications.html
summary: "Medications HTML View."
---

## Medications ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| MED | Medications | Yes | Yes | Yes | Yes |


### Clinical Narrative ###

A drug or other form of medicine that is used to treat or prevent disease. 

### Purpose ###

The purpose of this section is to provide a chronological history of medication prescribing as recorded.

### Sections and Subsections ###

Contains one main section, and three subsections:

 - [Current Medication Issues](accessrecord_view_medications.html#current-medication-issues)
 - [Current Repeat Medications](accessrecord_view_medications.html#current-repeat-medications)
 - [Past Medications](accessrecord_view_medications.html#past-medications)
 
### Section Banner Content ###

Providers message describing at a summary level how they have populated this section, and also the warning message where medications prescribed elsewhere have been excluded:

<div class="panel panel-default">
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> EMIS banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
		<p><b>Always displays this text:</b></p>
			<ul>
				<li>Non - BNF designated items e.g. local mixtures, have been excluded.</li>
				<li>May also contain immunisations issued as medications.</li>
				<li>Can also contain details on problems linked to medications if available.</li>
				<li>Past medications may include prescriptions which have been cancelled or discontinued before the original prescribed end date.</li>
				<li>Medication Max Issues are not shared currently.</li>
  
			</ul>
		<p><b>Only displayed if a record is in transit:</b></p>
			<ul>
				<li>Data may be incomplete due to a pending GP transfer.</li>
			</ul>
		<p><b>Only if line item(s) have been excluded:</b></p>
			<ul>
			  <li>Data items removed due to patient preference, confidentiality and / or RCGP exclusions.</li>
			</ul>
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> TPP banner content (click here to expand/collapse)</p>
  </div>
  <div class="panel-body">
    No setion banner content text displayed.
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> INPS banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
    No setion banner content text displayed.
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> MicroTest banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
    No setion banner content text displayed.
  </div>
</div>

### Subsection Business Rules ###

| Supplier | Business Rules |
|----------|----------------|
| EMIS | Medication item appears in this section if it has been 28 days or less for from the last issued date (applies to acute and repeat medications). |
| TPP | TBC |
| INPS | Medication item appears in this section if it has been 12 months or less for from the last issued date (applies to acute and repeat medications). |
| MicroTest | Microtest use two ‘lists’ to present the patient drugs to the user who can then toggle between the two as they choose. The lists are headed ‘current’ and ‘removed’ and aim to break a potentially long list of drugs into two more relevant groups. <br><br> This categorisation is a flag on the database maintained either manually by the doctor or, more likely, automatically by the system (if a drug hasn’t been issued for more than a configurable period, typically 6 months, then a drug will be automatically moved from the ‘current’ list to the ‘removed’ list). <br><br> Whichever list a drug is in has no bearing on what other data is held on the system about the patient’s history with the drug. No data is lost when moving a drug from one list to the other. |

### Discontinued/Cancelled/Naturally ended Medications ###

{% include note.html content="It is not currently possible for all GP system suppliers to distinguish between “Discontinued”, “Cancelled” & “Naturally Ended” medications." %} 

The definitions for each of these are supplied below:

- Naturally Ended: Medication naturally came to an end, i.e. no manual intervention via the user (auto system transition)
- Cancelled: Actively stopped acute medication by user
- Discontinued: Actively stopped repeat medication by user

Not all suppliers can supply the details (date and reason) for the ending of a medication (either through discontinuation or cancellation).

It is extremely important for the details regarding the ending of a medication to be available to a clinician, as this will highlight any clinical issues (e.g. stopping a medication due to an allergy etc.) and allow the clinician to make an efficient and informed clinical decision.

Refer to decision log item (HDL-212) which contains significant detail around this issue.

The current behaviour of the suppliers is as follows:

<div class="panel panel-default">
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> EMIS behaviour (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
		<p>EMIS cannot distinguish between cancelled, discontinued or ended (always identified as expired for naturally ended), although they do hold a date and free text reason within their system.</p>
		<p>To reduce the clinical risk the following recommendations have been made:</p>	
			<ul>
				<li>The mitigating banner EMIS have implemented is used for pilots only.</li>
				<li>The mitigating banner is complemented by providing pilot users with additional guidance on the behaviour of past medications as part of a wider guidance document (again, pilots only).</li>
				<li>The cancellation/end reason field is included as part of future HTML view specification release, which providers must support as soon as possible (after initial pilots once further pilot feedback has been received). It should be noted the a strategic programme decision has been made to confine the next version of HTML View Access Record to only include resolutions for clinical issues.</li>
  			</ul>
		<p>NOTE: EMIS cannot meet the original requirement of displaying discontinued date for discontinued and cancelled medications due to the way data is stored within EMIS Web. In light of this, the end date and reason suggested as a long term solution would also include the end date and reason for naturally ended medications.</p>
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> TPP behaviour (click here to expand/collapse)</p>
  </div>
  <div class="panel-body">
	Behaviour to be confirmed.
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> INPS behaviour (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
	INPS does not have a concept of cancelled. For discontinued medications they hold a date and reason within their system and this should be included in the details column. Note: INPS use the term de-activated in Vision as opposed to discontinued.
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> MicroTest behaviour (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
    MicroTest only show that the medication has been actively stopped by a user. They do not hold the date or reason for the ending of a medication (these are not viewable in their GP system).
  </div>
</div>



## Current Medication Issues ##

### Clinical Narrative ###

A list of drugs or other forms of medicines that are currently being used to treat or prevent disease for the patient.

### Purpose ###

The purpose of this section is to provide a view of medications that the patient is currently taking which informs the clinical decision-making process.

A list of all current acute and repeat medications issued to a patient ordered by date descending (i.e. most recent date/time first).

{% include warning.html content="The current medications list will only contain those items prescribed by the patient's current GP organization. Hence, if the patient has been issued prescriptions elsewhere or has recently moved GP practice then this list may not be complete." %}

### Date Filter ###

All relevant records **SHALL** be returned (i.e. no time limit/filtering is to be applied).

### Subsection Banner Content Message ###

Providers message describing at a summary level how they have populated this section.

<div class="panel panel-default">
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> EMIS banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
		<p><b>Always displays this text:</b></p>
			<ul>
				<li>All relevant items subject to patient preferences and / or RCGP exclusions.</li>
			</ul>
		<p><b>Only displayed if a record is in transit:</b></p>
			<ul>
				<li>Data may be incomplete due to a pending GP transfer.</li>
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
			</ul>
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> MicroTest banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
    No setion banner content text displayed.
  </div>
</div>




### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Current Medication Issues".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date` | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp;| Descriptive name of medication item (inculding dosage) | `free-text` |
| <center>3</center> | `Type` | Type of medication issued (values `Repeat` or `Acute`) | `free-text` |
| <center>4</center> | `Scheduled End` | Scheduled end date of medication issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Days Duration` | Duration of medication issued | `integer` |
| <center>6</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | `free-text` |

Provider systems **SHALL** include all relevant clinical content in the `Details` free-text field. As a minimum the free-text narrative **SHALL** include these items: <br>
- `MedicationOrder.medication.code`
- `MedicationOrder.dosageInstruction.dose[x]`
- `MedicationOrder.dosageInstruction.schedule[x]`
- `MedicationOrder.dosageInstruction.rate`
- `MedicationOrder.dosageInstruction.maxDosePerPeriod`


### HTML View ###

{% raw %}
```html
<div ng-controller="ctrl">
	<h3>Current Medication Issues</h3>
		<table class="table">
			<thead>
				<tr>
					<th>Start Date</th>
					<th>Medication Item</th>
					<th>Type</th>
					<th>Scheduled End</th>
					<th>Days Duration</th>
					<th>Details</th>
				</tr>
			</thead>
				<tr ng-repeat="x in records" class="table">
					<td>{{x.date}}</td>
					<td>{{x.drug}}</td>
					<td>{{x.type}}</td>
					<td>{{x.scheduledEnd}}</td>
					<td>{{x.daysDuration}}</td>
					<td>{{x.details}}</td>
				</tr>
		</table>
</div>
```
{% endraw %}





## Current Repeat Medications##

### Clinical Narrative ###

A list of repeat drugs or other forms of medicines that are currently being used to treat or prevent disease for the patient. This may also include PRN occasional use medication e.g. EpiPen, antihistamines, monitoring or continence products etc.

### Purpose ###

The purpose of this section is to provide a view of repeat medications that the patient is currently taking which informs the clinical decision-making process.

### Date Filter ###

All relevant records **SHALL** be returned (i.e. no time limit/filtering is to be applied).

### Subsection Banner Content Message ###

Providers message describing at a summary level how they have populated this section.

<div class="panel panel-default">
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> EMIS banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
		<p><b>Always displays this text:</b></p>
			<ul>
				<li>All relevant items subject to patient preferences and / or RCGP exclusions.</li>
			</ul>
		<p><b>Only displayed if a record is in transit:</b></p>
			<ul>
				<li>Data may be incomplete due to a pending GP transfer.</li>
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
    No setion banner content text displayed.
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> MicroTest banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
    No setion banner content text displayed.
  </div>
</div>


### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Current Repeat Medications".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by Last Issued date descending (i.e. most recent date/time first).

### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Last Issued` |  Date of medication item last issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp; | Descriptive name of medication item (inculding dosage) | `free-text` |
| <center>3</center> | `Start Date` | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>4</center> | `Review Date` | Review date of medication issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Number Issued` | Number of times medication item issued | `integer` |
| <center>6</center> | `Max Issues` | Maximum number of issues allowed for medication item | `integer` |
| <center>7</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | `free-text` |



### HTML View ###

{% raw %}
```html
<div ng-controller="ctrl">
	<h3>Current Repeat Medications</h3>
		<table class="table">
			<thead>
				<tr>
					<th>Last Issued</th>
					<th>Medication Item</th>
					<th>Start Date</th>
					<th>Review Date</th>
					<th>Number Issued</th>
					<th>Max Issues</th>
					<th>Details</th>
				</tr>
			</thead>
				<tr ng-repeat="x in records1" class="table">
					<td>{{x.lastIssued}}</td>
					<td>{{x.drug}}</td>
					<td>{{x.start}}</td>
					<td>{{x.review}}</td>
					<td>{{x.numberIssued}}</td>
					<td>{{x.maxIssues}}</td>
					<td>{{x.details}}</td>
				</tr>
		</table>
</div>
```
{% endraw %}




## Past Medications ##

### Clinical Narrative ###

A history view of drugs or other forms of medicines that have been used to treat or prevent disease for the patient.

### Purpose ###

The purpose of this section is to provide a historical view of repeat medications that the patient has been recorded to have been prescribed or taken. This informs the clinical decision-making process.

A list of all past medications, issued to a patient ordered by date descending (i.e. most recent date/time first). The type will include Acute, or Repeat. 

Where the medication was cancelled (Acute) or Discontinued (Repeat), this should be included in the Details column as Cancelled followed by Date of Cancellation or Discontinued, followed by Date when discontinued.

### Date Filter ###

A date filter is applicable for the Past Medications subsection:

- All relevant records **SHALL** be returned according to the consumer-supplied date range
- If a date is not supplied all records **SHALL** be returned


### Subsection Banner Content Message ###

Providers message describing at a summary level how they have populated this section.

<div class="panel panel-default">
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> EMIS banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
		<p><b>Always displays this text when date filtered:</b></p>
			<ul>
				<li>For the period 'dd-Mmm-yyyy' to 'dd-Mmm-yyyy' subject to patient preferences and/or RCGP exclusions.</li>
			</ul>
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> TPP banner content (click here to expand/collapse) </p>
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
		<p><b>Always displays this text when date filtered:</b></p>
			<ul>
				<li>For the period 'dd-Mmm-yyyy' to 'dd-Mmm-yyyy'.</li>
			</ul>
  </div>
  <div class="panel-heading">
    <p class="panel-title"><span class="icon">+</span> MicroTest banner content (click here to expand/collapse) </p>
  </div>
  <div class="panel-body">
		<p><b>Always displays this text when date filtered:</b></p>
			<ul>
				<li>For the period 'dd-Mmm-yyyy' to 'dd-Mmm-yyyy'.</li>
			</ul>
  </div>
</div>


### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Past Medications".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (i.e. most recent date/time first).

### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp;|
| ------------ | ------------ | ------------ |
| <center>1</center> | `Start Date` | Start date of medication item issued | `dd-Mmm-yyyy` |
| <center>2</center> | `Medication Item` &nbsp;&nbsp;&nbsp;| Descriptive name of medication item (inculding dosage) | `free-text` |
| <center>3</center> | `Type` | Type of medication issued (values `Repeat` or `Acute`) | `free-text` |
| <center>4</center> | `Last Issued` |  Date of medication item last issued | `dd-Mmm-yyyy` |
| <center>5</center> | `Review Date` | Review date of medication issued | `dd-Mmm-yyyy` |
| <center>6</center> | `Number Issued` | Number of times medication item issued | `integer` |
| <center>7</center> | `Max Issues` | Maximum number of issues allowed for medication item | `integer` |
| <center>8</center> | `Details` | Longer human readable free-text details for the medication item &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  | `free-text` |


### HTML View ###

{% raw %}
```html
<div ng-controller="ctrl">
	<h3>Past Medications</h3>
		<table class="table">
			<thead>
				<tr>
					<th>Start Date</th>
					<th>Medication Item</th>
					<th>Type</th>
					<th>Last Issued</th>
					<th>Review Date</th>
					<th>Number Issued</th>
					<th>Max Issues</th>
					<th>Details</th>
				</tr>
			</thead>
				<tr ng-repeat="x in records2" class="table">
					<td>{{x.start}}</td>
					<td>{{x.drug}}</td>
					<td>{{x.type}}</td>
					<td>{{x.lastIssued}}</td>
					<td>{{x.review}}</td>
					<td>{{x.numberIssued}}</td>
					<td>{{x.maxIssues}}</td>
					<td>{{x.details}}</td>
				</tr>
		</table>
</div>
```
{% endraw %}

{% include important.html content="AngularJS tags (e.g ng-repeat) are present merely to indicate to a developer the structure of the table content. Presence of these tags are not intended to imply use of any specific technology." %}

## Example View ##

<p data-height="1865" data-theme-id="light" data-slug-hash="GyJROK" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Medications" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/GyJROK/">Medications</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/GyJROK) for example of using AngularJS to generate table content" %}
