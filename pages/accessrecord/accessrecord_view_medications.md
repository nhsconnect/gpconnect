---
title: Medications
keywords: getcarerecord, view, section, medications
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_medications.html
summary: "Medications HTML view"
---

| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| MED | Medications | Yes | Yes | Yes | Yes |


## Clinical narrative ##

A drug or other form of medicine that is used to treat or prevent disease. 

## Purpose ##

The purpose of this section is to provide a history of medication prescribing as recorded.

## Sections and subsections ##

Contains one main section, and five subsections:

 - [Acute Medication (Last 12 Months)](accessrecord_view_medications.html#acute-medication-last-12-months)
 - [Current Repeat Medication](accessrecord_view_medications.html#current-repeat-medication)
 - [Discontinued Repeat Medication](accessrecord_view_medications.html#discontinued-repeat-medication)
 - [All Medication](accessrecord_view_medications.html#all-medication)
 - [All Medication Issues](accessrecord_view_medications.html#all-medication-issues)

 
## Section title ##

The section title **MUST** be 'Medications'.

## Date filter ##

A date filter is applicable to this section. The date filter **MUST** be applied to the All Medication and All Medication Issues subsections only. All other subsections **MUST** return all records as defined in the subsection descriptions below, subject to exclusions.
 
## Section content banner ##

Provider message describing at a summary level how they have populated this section.




## Acute Medication (Last 12 Months) ##

### Clinical narrative ###

A list of acute medicines that are currently being, or have recently been, used to treat or prevent disease for the patient. The provider **MUST** include all acute medication whose `Start Date` (the date the prescription is expected to start) is greater than the current date minus 365 days.

This is aligned to the Acute Medications section in Summary Care Records (SCR). 

### Purpose ###

The purpose of this section is to provide a view of acute medications that the patient has recently been taking, which informs the clinical decision-making process.

### Subsection title ###

The subsection title **MUST** be 'Acute Medication (Last 12 Months)'.

### Date filter ###

All relevant records **MUST** be returned.

### Subsection content banner ###

Provider message describing at a summary level how they have populated this subsection.

Providers **MUST** return the following message, if applicable:

```html
<div>
	<p>Scheduled End Date is not always captured in the source; where it was not recorded, the displayed date is calculated from start date and days duration</p>
</div>
```

### Table columns ###

Providers **MUST** return all the columns as described in the table below, sorted by `Start Date` descending:

<div>
<table>
<thead>
  <tr class="header">
	<th style="width:5%">Order</th>
	<th style="width:23%">Name</th>
	<th style="width:58%">Description</th>
	<th style="width:14%">Value details</th>
  </tr>
 </thead>
  <tr>
    <td style="text-align:center">1</td>
    <td><code>Type</code></td>
    <td>Type of medication issued (for example, <code>Acute, Acute Post-Dated, Acute - [Prescribing Agency Type]<sup><strong>1</strong></sup></code>).</td>
    <td><code>free-text</code></td>
  </tr> 
  <tr>
    <td style="text-align:center">2</td>
    <td><code>Start Date</code> <em class="fa fa-sort-desc" aria-hidden="true"></em></td>
    <td>The date of issue of the acute medications, except where:
		<ul>
			<li>the medication is post-dated it <strong>MUST</strong> be the post date</li>
			<li>the medication is prescribed elsewhere it <strong>MUST</strong> be the expected start date if known, else the entered date </li>
		</ul>
	</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>
  <tr>
    <td style="text-align:center">3</td>
    <td><code>Medication Item</code></td>
    <td>Descriptive name of medication item (including dosage) (for example, <code>Ibuprofen 400mg tablets</code>).</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">4</td>
    <td><code>Dosage Instruction</code></td>
    <td>Dosage instructions for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Dosage Rate</li>
			<li>Schedule (when / how often)</li>
		</ul>
	<p>for example, <code>two to be taken daily</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">5</td>
    <td><code>Quantity</code></td>
    <td>Quantity details for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Quantity</li>
			<li>Quantity unit</li>
		</ul>
	<p>for example, <code>14 capsule</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">6</td>
    <td><code>Scheduled End Date</code></td>
    <td>The date the prescription is expected to finish.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">7</td>
    <td><code>Days Duration</code></td>
    <td>Duration of medication issued in days.</td>
    <td><code>integer</code></td>
  </tr>
  <tr>
    <td style="text-align:center">8</td>
    <td><code>Additional Information</code></td>
    <td>If the medication record includes the information, the following details <strong>MUST</strong> be included (each item <strong>MUST</strong> be separated with a line break):
		<ul>
			<li><code><strong>CONTROLLED DRUG</strong></code> label in <strong>bold</strong> text </li>
			<li><code>CANCELLED: </code> label with cancellation date and reason</li>
			<li>Reason for the medication</li>
			<li>Linked problems / diagnoses</li>
			<li>Other supporting information</li>
		</ul>
	<p>The provider <strong>MAY</strong> include labels in addition to the ones specified to support additional text (for example, <code>Linked Problem : Ear Infection</code>).</p>
	</td>
    <td><code>free-text</code></td>
  </tr>  
</table>
</div>

<sup><strong>1</strong></sup> Where the medication was Prescribed Elsewhere the prescribing agency (type of organisation responsible for authorising and issuing the medication) **MUST** be included with the Type, for example, 'Acute – Dentist'. If the medication item is identifiable as prescribed elsewhere but the type of organisation who prescribed it is not recorded, then the Type **MUST** be returned as 'Acute – Unknown Prescriber'.



## Current Repeat Medication##

### Clinical narrative ###

A list of repeat drugs or other forms of medicines that are currently being used to treat or prevent disease for the patient. This may also include PRN occasional use medication - for example, EpiPen, antihistamines, monitoring or continence products.

The provider **MUST** include all repeat and repeat dispensed medications (templates/plans/courses **NOT** individual issues) which have not been discontinued or otherwise ended. Repeat medications (including repeat dispense) which have not been discontinued are considered current where the Effective End Date (the date the cycle of prescriptions is expected to end) is either greater than the current date or is null. This **MUST** include those which have been authorised but not yet issued (Last Issued and Number Issued will be null).

### Purpose ###

The purpose of this section is to provide a view of all repeat medications that the patient is currently prescribed, which informs the clinical decision-making process.

This is aligned to the Repeat Medications section in Summary Care Records (SCR).

### Subsection title ###

The subsection title **MUST** be 'Current Repeat Medication'.

### Date filter ###

All relevant records **MUST** be returned (that is, no time limit/filtering is to be applied).

### Subsection content banner ###

Provider message describing at a summary level how they have populated this subsection.

Providers **MUST** return the following message, if applicable:

```html
<div>
	<p>The Review Date is that set for each Repeat Course. Reviews may be conducted according to a diary event which differs from the dates shown</p>
</div>
```

### Table columns ###

Providers **MUST** return all the columns as described in the table below, sorted by `Start Date` descending:

<div>
<table>
<thead>
  <tr class="header">
	<th style="width:5%">Order</th>
	<th style="width:23%">Name</th>
	<th style="width:58%">Description</th>
	<th style="width:14%">Value details</th>
  </tr>
 </thead>
  <tr>
    <td style="text-align:center">1</td>
    <td><code>Type</code></td>
    <td>Type of medication issued (for example, <code>Repeat, Repeat Dispense, Repeat – [Prescribing Agency Type]</code>).</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">2</td>
    <td><code>Start Date</code> <em class="fa fa-sort-desc" aria-hidden="true"></em></td>
    <td>The original date of authorisation of the repeat medication (if a provider system allows re-authorisation of a repeat medication the start date <strong>MUST</strong> be the first authorisation). If this is not known (for example, for prescribed elsewhere) then date of entry of the repeat medication record <strong>MUST</strong> be returned.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>
  <tr>
    <td style="text-align:center">3</td>
    <td><code>Medication Item</code></td>
    <td>Descriptive name of medication item (including dosage) (for example, <code>Ibuprofen 400mg tablets</code>).</td>
    <td><code>free-text</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">4</td>
    <td><code>Dosage Instruction</code></td>
    <td>Dosage instructions for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Dosage Rate</li>
			<li>Schedule (when / how often)</li>
		</ul>
	<p>for example, <code>two to be taken daily</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">5</td>
    <td><code>Quantity</code></td>
    <td>Quantity details for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Quantity</li>
			<li>Quantity unit</li>
		</ul>
	<p>for example, <code>14 capsule</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">6</td>
    <td><code>Last Issued Date</code></td>
    <td>The last issue date. If the medication is repeat dispense or prescribed elsewhere this <strong>MUST</strong> be null.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">7</td>
    <td><code>Number of Prescriptions Issued</code></td>
    <td>This <strong>MUST</strong> be the number issued up to the current date inclusive. For a repeat dispense this will be null. This <strong>MUST</strong> be null where no issues of the repeat have been made at the current date. If the medication is repeat dispensed or prescribed elsewhere this <strong>MUST</strong> be null.</td>
    <td><code>integer</code></td>
  </tr>
  <tr>
    <td style="text-align:center">8</td>
    <td><code>Max Issues</code></td>
    <td>The maximum number of issues the repeat prescription has authorised.</td>
    <td><code>integer</code></td>
  </tr>
  <tr>
    <td style="text-align:center">9</td>
    <td><code>Review Date</code></td>
    <td>The date the repeat medication is due for review.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">10</td>
    <td><code>Additional Information</code></td>
    <td>If the medication record includes the information, the following details <strong>MUST</strong> be included (each item <strong>MUST</strong> be separated with a line break):
		<ul>
			<li><code><strong>CONTROLLED DRUG</strong></code> label in <strong>bold</strong> text </li>
			<li>Reason for the medication</li>
			<li>Linked problems / diagnoses</li>
			<li>For Repeat Dispense, the date of the last authorisation and the number of prescription issues authorised</li>
			<li>Other supporting information</li>
		</ul>
	<p>The provider <strong>MAY</strong> include labels in addition to the ones specified to support additional text (for example, <code>Linked Problem : Heart Failure</code>).</p>
	</td>
    <td><code>free-text</code></td>
  </tr>  
</table>
</div>




<div class="bs-callout bs-callout-info"><em class="fa fa-info-circle"></em> <strong>Note:</strong> If the provider system allows the repeat medication (course/template) details to be amend so it differs from the latest prescription issued, then <ul><li>the latest details for the medication (course/template) <strong>MUST</strong> be returned by the provider</li><li>a subsection banner message <strong>MUST</strong> be added such as: the medication below is taken from a list of Repeat Medication Templates in the patient record which may have been amended since they were last issued. See the All Medication Issues subsection for all repeat prescriptions issued.</li></ul></div>


## Discontinued Repeat Medication##

### Clinical narrative ###

A list of discontinued repeat drugs or other forms of medicines. This may also include PRN occasional use medication - for example, EpiPen, antihistamines, monitoring or continence products.

### Purpose ###

The purpose of this section is to provide a view of all discontinued repeat medications that the patient has been prescribed and the circumstances for discontinuing the medication, which informs the clinical decision-making process.

This **MUST** include repeat medications discontinued by a clinician action.

This **MUST NOT** include repeat medications expired by system processes, for example, automatically expiring a medication which has not been issued for a given period of time.

This is aligned to the Discontinued Repeat Medications section in SCR, but is not limited to six months.


### Subsection title ###

The subsection title **MUST** be 'Discontinued Repeat Medication'.

### Date filter ###

All relevant records **MUST** be returned (that is, no time limit/filtering is to be applied).

### Subsection content banner ###

Provider message describing at a summary level how they have populated this subsection.

Providers **MUST** return the following message:

```html
<div>
	<p>All repeat medication ended by a clinician action</p>
</div>
```

### Table columns ###

Providers **MUST** return all the columns as described in the table below, sorted by `Last Issued Date` descending:

<div>
<table>
<thead>
  <tr class="header">
	<th style="width:5%">Order</th>
	<th style="width:23%">Name</th>
	<th style="width:58%">Description</th>
	<th style="width:14%">Value details</th>
  </tr>
 </thead>
  <tr>
    <td style="text-align:center">1</td>
    <td><code>Type</code></td>
    <td>Type of medication issued (for example, <code>Repeat, Repeat Dispense, Repeat – [Prescribing Agency Type]</code>).</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">2</td>
    <td><code>Last Issued Date</code> <em class="fa fa-sort-desc" aria-hidden="true"></em></td>
    <td>The last issue date. If the medication is repeat dispense or prescribed elsewhere this <strong>MUST</strong> be null.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>
  <tr>
    <td style="text-align:center">3</td>
    <td><code>Medication Item</code></td>
    <td>Descriptive name of medication item (including dosage) (for example, <code>Ibuprofen 400mg tablets</code>).</td>
    <td><code>free-text</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">4</td>
    <td><code>Dosage Instruction</code></td>
    <td>Dosage instructions for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Dosage Rate</li>
			<li>Schedule (when / how often)</li>
		</ul>
	<p>for example, <code>two to be taken daily</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">5</td>
    <td><code>Quantity</code></td>
    <td>Quantity details for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Quantity</li>
			<li>Quantity unit</li>
		</ul>
	<p>for example, <code>14 capsule</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">6</td>
    <td><code>Discontinued Date</code></td>
    <td>The date the medication item was discontinued. This should be the date the clinician has entered as the discontinuation date if available, otherwise the system date of the discontinuation action.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">7</td>
    <td><code>Discontinuation Reason</code></td>
    <td>The coded reason for the ending of the medication returned as its text description and/or free text narrative as available.</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">8</td>
    <td><code>Additional Information</code></td>
    <td>If the medication record includes the information, the following details <strong>MUST</strong> be included (each item <strong>MUST</strong> be separated with a line break):
		<ul>
			<li><code><strong>CONTROLLED DRUG</strong></code> label in <strong>bold</strong> text </li>
			<li>Reason for the medication</li>
			<li>Linked problems / diagnoses</li>
			<li>For Repeat Dispense, the date of the last authorisation and the number of prescription issues authorised</li>
			<li>Other supporting information</li>
		</ul>
	<p>The provider <strong>MAY</strong> include labels in addition to the ones specified to support additional text (for example, <code>Linked Problem : Heart Failure</code>).</p>
	</td>
    <td><code>free-text</code></td>
  </tr>  
</table>
</div>




## All Medication ##

### Clinical narrative ###

A history view of drugs or other forms of medicines that have been used to treat or prevent disease for the patient.

### Purpose ###

The purpose of this subsection is to provide a distinct list of all the medications recorded for the patient and to present the list alphabetically to make it easier to view for specific medication items. The list is also presented alphabetically to enable easier identification of changes to a medication over time, for example, change in dosage.

Items included in the Recent Acute Medication and Current Repeat Medication **MUST** also be included within this subsection, as well as past medications.

### Subsection title ###

The subsection title **MUST** be 'All Medication'.

### Date filter ###

If a consumer submits a date filter for this subsection the dates will be applied as follows (this applies equivalent rules to structured medication date filtering):

 1.	If the medication has an effective period (a start date and a scheduled end date), filter using the effective period: 
	1.	The provider system **MUST** return the medication summary data items for all medications whose effective periods overlap the date range (inclusive) sent by the consuming system.
 2.	If the medication has an effective start date, does not have an effective end date and is repeat (repeat prescribed, repeat dispensed or prescribed elsewhere repeat), treat the effective period as ongoing for the filter: 
	1.	The provider system **MUST** return the medication summary data items for all medications whose effective start date is during or before the date range (inclusive) sent by the consuming system.
	2.	Where the medication is prescribed elsewhere and does not identify itself as acute or repeat then treat it as repeat for the filter to ensure the clinician has higher likelihood of visibility of the item and can decide themselves if it is relevant.
 3.	If the medication has an effective start date, does not have an effective end date and is acute (acute or prescribed elsewhere acute), filter using the effective start date: 
	1.	The provider system **MUST** return the medication summary data items for all medications whose effective start date is during the date range (inclusive) sent by the consuming system.
 4.	If the medication does not have an effective start date (for example, prescribed elsewhere), filter using the date it was recorded on the local system: 
	1.	The provider system **MUST** return the medication summary data items for all medications whose recorded date is during the date range (inclusive) sent by the consuming system.
	2.	Where no effective period is available use the date the item was recorded on the system.



### Subsection content banner ###

Provider message describing at a summary level how they have populated this section.


### Table columns ###

Providers **MUST** return all the columns as described in the table below. 

It **MUST** be grouped by `Medication Item`, with `Medication Item` repeated as a distinct group title, then sorted alphabetically. `Medication Items` listed within a group **MUST** be sorted by `Start Date` descending.

Please see the [HTML view](accessrecord_view_medications.html#html-view) and [Example view](accessrecord_view_medications.html#example-view) for a coded example of displaying this subsection.

<div>
<table>
<thead>
  <tr class="header">
	<th style="width:5%">Order</th>
	<th style="width:23%">Name</th>
	<th style="width:58%">Description</th>
	<th style="width:14%">Value details</th>
  </tr>
 </thead>
  <tr>
    <td style="text-align:center"><em class="fa fa-object-group" aria-hidden="true"></em></td>
    <td><code>Medication Item</code> <em class="fa fa-sort-asc" aria-hidden="true"></em></td>
    <td>Grouped distinct descriptive name of medication item (including dosage) (for example, <code>Ibuprofen 400mg tablets</code>).</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">1</td>
    <td><code>Type</code></td>
    <td>Type of medication issued (for example, <code>Acute, Repeat, Repeat Dispense, Acute - [Prescribing Agency Type], Repeat - [Prescribing Agency Type]</code>).</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">2</td>
    <td><code>Start Date</code> <em class="fa fa-sort-desc" aria-hidden="true"></em></td>
    <td>The date the medication was first prescribed. If this is not known (for example, for prescribed elsewhere) then date of entry <strong>MUST</strong> be used.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>
  <tr>
    <td style="text-align:center">3</td>
    <td><code>Medication Item</code></td>
    <td>Descriptive name of medication item (including dosage) (for example, <code>Ibuprofen 400mg tablets</code>).</td>
    <td><code>free-text</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">4</td>
    <td><code>Dosage Instruction</code></td>
    <td>Dosage instructions for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Dosage Rate</li>
			<li>Schedule (when / how often)</li>
		</ul>
	<p>for example, <code>two to be taken daily</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">5</td>
    <td><code>Quantity</code></td>
    <td>Quantity details for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Quantity</li>
			<li>Quantity unit</li>
		</ul>
	<p>for example, <code>14 capsule</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>   
  <tr>
    <td style="text-align:center">6</td>
    <td><code>Last Issued Date</code></td>
    <td>The last issue of the medication item (acute or repeat). If the medication is repeat dispense or prescribed elsewhere this <strong>MUST</strong> be null.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">7</td>
    <td><code>Number of Prescriptions Issued</code></td>
    <td>The sum of the number of issues of the medication – actual issues not the max issues. If this is not known (for example, for medication prescribed elsewhere or repeat dispense, this <strong>MUST</strong> be null).</td>
    <td><code>integer</code></td>
  </tr>
  <tr>
    <td style="text-align:center">8</td>
    <td><code>Discontinuation Details</code></td>
    <td>
		<p><code>CANCELLED: </code>label with cancellation date and reason (acute) or <code>DISCONTINUED: </code>label with discontinued date and discontinuation reason (repeat)</p>
		<p>Details will be equivalent to the combined discontinued date and discontinuation reason columns in Discontinued Repeat Medication, but will apply to Acute medication (labelled cancelled) as well as repeat.</p>
	</td>
    <td><code>free-text</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">9</td>
    <td><code>Additional Information</code></td>
    <td>If the medication record includes the information, the following details <strong>MUST</strong> be included (each item <strong>MUST</strong> be separated with a line break):
		<ul>
			<li><code><strong>CONTROLLED DRUG</strong></code> label in <strong>bold</strong> text </li>
			<li>For Repeat Dispense, the date of the last authorisation and the number of prescription issues authorised</li>
			<li>Reason for the medication</li>
			<li>Linked problems / diagnoses</li>
			<li>Other supporting information</li>
		</ul>
	<p>The provider <strong>MAY</strong> include labels in addition to the ones specified to support additional text (for example, <code>Linked Problem : Heart Failure</code>).</p>
	</td>
    <td><code>free-text</code></td>
  </tr>  
</table>
</div>






## All Medication Issues ##

### Clinical narrative ###

A history view of drugs or other forms of medicines that have been used to treat or prevent disease for the patient.

### Purpose ###

The purpose of this section is to provide a historical view of all issues (prescribed elsewhere and repeat dispense are not included as their issues are not recorded on the GP system).

This is the only subsection to include the individual issues of a repeat medication.

### Subsection title ###

The subsection title **MUST** be 'All Medication Issues'.

### Date filter ###

If a consumer submits a date filter for this section the dates will be applied as follows:

The provider **MUST** return all medication issues which relate to the medication items returned for the All Medication subsection. This may result in records which have an issue date outside of the consumer date filter range.

### Subsection content banner ###

Providers message describing at a summary level how they have populated this section.

### Table columns ###

Providers **MUST** return all the columns as described in the table below. 

It **MUST** be grouped by `Medication Item`, with `Medication Item` repeated as a distinct group title, then sorted alphabetically. `Medication Items` listed within a group **MUST** be sorted by `Issue Date` descending.

Please see the [HTML view](accessrecord_view_medications.html#html-view) and [Example view](accessrecord_view_medications.html#example-view) for a coded example of displaying this subsection.

<div>
<table>
<thead>
  <tr class="header">
	<th style="width:5%">Order</th>
	<th style="width:23%">Name</th>
	<th style="width:58%">Description</th>
	<th style="width:14%">Value details</th>
  </tr>
 </thead>
  <tr>
    <td style="text-align:center"><em class="fa fa-object-group" aria-hidden="true"></em></td>
    <td><code>Medication Item</code> <em class="fa fa-sort-asc" aria-hidden="true"></em></td>
    <td>Grouped distinct descriptive name of medication item (including dosage) (for example, <code>Ibuprofen 400mg tablets</code>).</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">1</td>
    <td><code>Type</code></td>
    <td>Type of medication issued (for example, <code>Acute, Repeat</code>).</td>
    <td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">2</td>
    <td><code>Issue Date</code> <em class="fa fa-sort-desc" aria-hidden="true"></em></td>
    <td>The date the medication item was issued.</td>
    <td><code>dd-Mmm-yyyy</code></td>
  </tr>
  <tr>
    <td style="text-align:center">3</td>
    <td><code>Medication Item</code></td>
    <td>Descriptive name of medication item (including dosage) (for example, <code>Ibuprofen 400mg tablets</code>).</td>
    <td><code>free-text</code></td>
  </tr>  
  <tr>
    <td style="text-align:center">4</td>
    <td><code>Dosage Instruction</code></td>
    <td>Dosage instructions for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Dosage Rate</li>
			<li>Schedule (when / how often)</li>
		</ul>
	<p>for example, <code>two to be taken daily</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>
  <tr>
    <td style="text-align:center">5</td>
    <td><code>Quantity</code></td>
    <td>Quantity details for the medication item. As a minimum, this <strong>MUST</strong> include:
		<ul>
			<li>Quantity</li>
			<li>Quantity unit</li>
		</ul>
	<p>for example, <code>14 capsule</code></p>
	</td>
	<td><code>free-text</code></td>
  </tr>   
  <tr>
    <td style="text-align:center">6</td>
    <td><code>Days Duration</code></td>
    <td>Duration of the medication issued in days.</td>
    <td><code>integer</code></td>
  </tr>
  <tr>
    <td style="text-align:center">7</td>
    <td><code>Additional Information</code></td>
    <td>If the medication record includes the information, the following details <strong>MUST</strong> be included (each item <strong>MUST</strong> be separated with a line break):
		<ul>
			<li><code><strong>CONTROLLED DRUG</strong></code> label in <strong>bold</strong> text </li>
			<li>Reason for the medication</li>
			<li>Linked problems / diagnoses</li>
			<li>Other supporting information</li>
		</ul>
	<p>The provider <strong>MAY</strong> include labels in addition to the ones specified to support additional text (for example, <code>Linked Problem : Ear Infection</code>).</p>
	</td>
    <td><code>free-text</code></td>
  </tr>  
</table>
</div>


## Additional medication information ##

### Ended medications ###

It is extremely important for the details regarding the ending of a medication to be available to a clinician, as this will highlight any clinical issues (for example, stopping a medication due to an allergy) and allow the clinician to make an efficient and informed clinical decision.

Details of change to follow as a comment:

- **Naturally ended**: Medication naturally came to an end, that is, no manual intervention via the user (auto system transition)
- **Cancelled**: Actively stopped acute medication by user
- **Discontinued**: Actively stopped repeat medication by user

Naturally Ended medications **MUST NOT** be included in the Discontinued Repeat Medication subsection and end date and reason **MUST NOT** be included in Additional Information in Recent Acute Medications or the Discontinuation Details in All Medication.

If a system provider cannot differentiate between naturally ended, discontinued and cancelled section/subsection, banner message(s) **MUST** be included as appropriate to describe the extent or limitation of compliance.


### Prescribed elsewhere ###

All subsections (except All Medication Issues) **MUST** include items which are recorded on the system as a prescription but prescribed elsewhere (for example, hospitals or special clinics) or 'Over The Counter' drugs taken by the patient and recorded on the system as a prescription. This Type column will identify a medication item as prescribed elsewhere by including the Agency Type after the medication type (Acute / Repeat) or 'Unknown Prescriber' where an agency type cannot be determined.

### GP2GP transfer ###

Repeat medications transferred as part of GP2GP **MUST** only be included in the Current Repeat Medications subsection if authorised by a clinician at the new practice, otherwise they are treated as not current. Therefore, they appear in All Medication and All Medication Issues, but not in Current Repeat Medication.
 


## HTML view ##

The following content highlights the expected HTML tags and format providers **MUST** use when generating the HTML content:

{% include accessrecord/medications.html %}

## Example view ##

<p data-height="2000" data-theme-id="light" data-slug-hash="bxOYYZ" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Medications" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/bxOYYZ/">Medications</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/bxOYYZ) for example of using AngularJS to generate table content." %}
