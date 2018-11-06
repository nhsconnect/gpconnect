---
title: Provider variance
sidebar: accessrecord_sidebar
permalink: accessrecord_provider_variance.html
summary: "Known provider variance to the Access Record capability"
---
<a href="#" class="back-to-top">Back to Top</a>

## Purpose ##

The purpose of this page is to identify the variances between provider response banner messages, to better aid consumers during development.


## Cross section/subsection banner variances ##

### GP transfer banner message ###

The following messages are returned by the provider systems when a GP to GP transfer is in progress:

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>Record is in transit and may be incomplete.</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Data may be incomplete due to a pending GP transfer.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>This patient has been registered since dd/mm/yyyy but there is no record of successful completion of the GP2GP process. Some information may not yet be incorporated into the local patient record.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>GP transfer underway - record may be incomplete due to the transfer.</td>
	  </tr>
	</tbody>
</table>


### Date banner message ###

The following messages are returned by the provider systems when a date filter is applied, please see each HTML view page for details on where date filters are applicable:

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>For the period 'dd-Mmm-yyyy' to 'dd-Mmm-yyyy'.</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>For the selected date range dd-Mmm-yyyy to dd-Mmm-yyyy subject to patient preferences and/or RCGP exclusions.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>For the period 'dd-Mmm-yyyy' to 'dd-Mmm-yyyy'.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>For the period 'dd-Mmm-yyyy' to 'dd-Mmm-yyyy'.</td>
	  </tr>
	</tbody>
</table>


### Exclusion banner message ###

The following messages are returned by the provider systems when data has been excluded from the dataset returned. Additional information has been provided to describe the message displayed at line item, where applicable.		

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="45%">Message</th>
			<th width="40%">Line item message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>Some patient data is hidden by sharing rules. The data in this section may be incomplete.</td>
		<td>Event has been made private by another organisation</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Data items removed due to patient preference, confidentiality and / or RCGP exclusions.</td>
		<td><i>N/A, EMIS do not support line item exclusion</i></td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>One or more items have been suppressed due to privacy exclusion rules</td>
		<td>***********</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Items excluded due to confidentiality, patient preferences and/or RCGP sensitive dataset exclusions.</td>
		<td>Excluded items</td>
	  </tr>
	</tbody>
</table>

## HTML view content banner variances ##

### Encounters ###

The following content section messages are returned by the provider systems for [encounters](accessrecord_view_encounters.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Contains information recorded during consultations with the patient.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Contains Appointment information and any related information recorded during the consultation; related items may also occur in other sections.</td>
	  </tr>
	</tbody>
</table>

### Clinical items ###

The following content section messages are returned by the provider systems for [clinical items](accessrecord_view_clinical_items.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Contains coded clinical items relating to a patients care e.g. procedures, test results, conditions.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>Read Chapter 1, Read Chapters A-Z.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Contains clinical items including, but not limited to, Procedures, Diagnoses, Symptoms, Conditions; may include items included in other sections such as Linked Problems.</td>
	  </tr>
	</tbody>
</table>

### Problems and issues ###

The following content section messages are returned by the provider systems for [problems and issues](accessrecord_view_problems.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>Section includes problem and summary items.</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Past medications may include prescriptions which have been cancelled or discontinued before the original prescribed end date. Contains items coded as problems within the patients record; Can also contain details on medications linked to problems if available.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>

#### Active problems and issues subsection ####

The following content subsection messages are returned by the provider systems for [active problems and issues](accessrecord_view_problems.html#active-problems-and-issues):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Contains items coded as problems within the patients record; Can also contain details on medications linked to problems if available.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>All problems included in Active Section.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Contains clinical items including, but not limited to, Procedures, Diagnoses, Symptoms & Conditions that have been designated as Problems used to link together related information.</td>
	  </tr>
	</tbody>
</table>

#### Inactive problems and issues subsection ####

The following content subsection messages are returned by the provider systems for [inactive problems and issues](accessrecord_view_problems.html#inactive-problems-and-issues):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Contains items coded as problems within the patients record; Can also contain details on medications linked to problems if available.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>


### Allergies and adverse reactions ###

The following content section messages are returned by the provider systems for [allergies and adverse reactions](accessrecord_view_allergies.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Historical Allergies and Adverse Reactions data is not supported by this system.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>

#### Current allergies and adverse reactions subsection ####

The following content subsection messages are returned by the provider systems for [current allergies and adverse reactions](accessrecord_view_allergies.html#current-allergies-and-adverse-reactions):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>All Allergies Listed in Current Section.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>

#### Historical allergies and adverse reactions subsection ####

The following content subsection messages are returned by the provider systems for [historical allergies and adverse reactions](accessrecord_view_allergies.html#historical-allergies-and-adverse-reactions):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Historical Allergies and Adverse Reactions data is not supported by this system.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>



### Medications ###

The following content section messages are returned by the provider systems for [medications](accessrecord_view_medications.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Non - BNF designated items e.g. local mixtures, have been excluded. <br/>
			May also contain immunisations issued as medications; <br/>
			Can also contain details on problems linked to medications if available. <br/>
			Medication Max Issues are not shared currently <br/>
			Past Medications may include prescriptions which have been cancelled or discontinued before the original prescribed end date</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>

#### Current medication issues subsection ####

There are no content subsection messages returned by the provider systems for [current medication issues](accessrecord_view_medications.html#current-medication-issues).


#### Current repeat medications subsection ####

The following content subsection messages are returned by the provider systems for [current repeat medications](accessrecord_view_medications.html#current-repeat-medications):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>The medication above is taken from a list of Repeat Medication Templates in the patient record which may have been amended since they were last issued. You should look at the Current Medication Issues section to see what the patient has been given.</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>

#### Past medications subsection ####

There are no content subsection messages returned by the provider systems for [past medications](accessrecord_view_medications.html#past-medications).




### Referrals ###

The following content section messages are returned by the provider systems for [referrals](accessrecord_view_referrals.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Contains referrals related to the patient.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Contains items relating to 'Referral for Further Care'; may include repeated entries due to duplicated data in the source system.</td>
	  </tr>
	</tbody>
</table>

### Observations ###

The following content section messages are returned by the provider systems for [observations](accessrecord_view_observations.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Contains Observations with numeric and other measurement ranges.</td>
	  </tr>
	</tbody>
</table>

### Immunisations ###

The following content section messages are returned by the provider systems for [immunisations](accessrecord_view_immunisations.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Contains coded immunisations on the patient record; some immunisations may exist as issued medications also. <br/>Content and Part not supported.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>

### Administrative items ###

The following content section messages are returned by the provider systems for [administrative items](accessrecord_view_administrative_items.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Message</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>This system does not support retrieval of Administrative Items data.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>Contains clinical items including, but not limited to, Procedures, Diagnoses, Symptoms, Conditions; may include items included in other sections such as Linked Problems.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Contains non-clinical items - including, but not limited to, administrative, occupational, social context, carer information, communications preferences, legal information, learning disability, advance decisions etc.</td>
	  </tr>
	</tbody>
</table>
