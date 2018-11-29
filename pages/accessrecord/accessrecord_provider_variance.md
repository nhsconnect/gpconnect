---
title: Provider variance
sidebar: accessrecord_sidebar
permalink: accessrecord_provider_variance.html
summary: "Known provider variance to the Access Record capability"
---
<a href="#" class="back-to-top">Back to Top</a>

## Purpose ##

The purpose of this page is to identify the variances between provider response banner messages, and detail any business rules applied, to better aid consumers during development.


## Cross section/subsection banner variances ##

{% include custominfocallout.html content="**Information:** TPP display the section message for all sections regardless of whether there is an exclusion applicable to that section." type="info" %} 

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


{% include custominfocallout.html content="**Information:** TPP only include a table line item message in the Encounters section (or Last 3 Encounters table in the Summary section) and only for items marked private (as opposed to those relating to the exclusion data set). All other sections will not identify if an entry is absent or not." type="info" %} 


### Incomplete dates ###

The following explains how the provider systems deal with incomplete dates, where applicable:

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
		<td>Incomplete dates will be returned with the incomplete element missing, for example, dates may be returned as 2008 or Apr 2009. For the chronology, incomplete elements are treated as the first day of the month and first month of the year respectively.</td>
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
		<td>Incomplete elements of a date will be returned as the first day of the month or the first month of the year as applicable e.g. a date entered as ??/??/2011 will be returned as 01 Jan 2011.</td>
	  </tr>
	</tbody>
</table>



## HTML view business rules and content banner variances ##

### Encounters ###

The following business rules apply for [encounters](accessrecord_view_encounters.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Rule</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>Encounters is a representation of the SystmOne journal which is a full chronology. It therefore covers more than the clinical narrative definition.</td>
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

The following business rules apply for [clinical items](accessrecord_view_clinical_items.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Rule</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>Returns practice-specific codes categorised as clinical. Codes are categorised as either clinical or administrative by default according to practice specific configuration. The default can be overridden by users.</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Includes all coded items (clinical and administrative) except those which will be returned as observations (have numeric or associated values).</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>Includes coded items from Read Chapter 1 with Read Chapters A-Z.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Coded items excluding Read Code Chapter 2 & codes starting ‘9’ & ‘0’, not filtering out Observations.</td>
	  </tr>
	</tbody>
</table>

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

The following business rules apply for [problems and issues](accessrecord_view_problems.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Rule</th>
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
		<td>Inactive Problems not supported; problems included in 'Active Problems' table. Includes active problem headers and priority 1 medical history. Significance not supported.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Low priority mapped to ‘Minor’; Medium mapped to ‘Routine’; High mapped to ‘Major’.</td>
	  </tr>
	</tbody>
</table>

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

The following business rules apply for [allergies and adverse reactions](accessrecord_view_allergies.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Rule</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>All allergies and adverse reactions will be recorded in the Current Allergies and Adverse Reactions subsection. Historical allergies and adverse reactions data is not supported by EMIS.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>All allergy and adverse reactions data will be recorded in the Current Allergies and Adverse Reactions subsection. Vision do not record end dates for allergies & adverse reactions, therefore a history view is not possible.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>N/A</td>
	  </tr>
	</tbody>
</table>

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

The following business rules apply for [medications](accessrecord_view_medications.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Rule</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>Acute/repeat issues are current until the scheduled end date (issue date plus days duration). Repeat templates are current until actively ended by a system user action.</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>An acute medication is current for 28 days from issue or the issue date plus the days duration plus 14 days, whichever is the greater. <br/>Repeat medication courses are subject to a local configuration setting. When enabled, repeat courses will automatically expire after a configurable period from the last issue date plus the course duration. The period can be set from days to years. <br/>Repeat medication issues are included as current whilst the repeat course is current (meaning, has not been stopped/expired). </td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>All acute medications stay in the current medication issues (acute) section for 1 year (from prescription date) before being moved to Past Medication.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>‘Current Medication Issues’ are repeat and acute medications in the patient’s ‘current’ list, the ‘Current Repeat Medications’ are repeat medications in the patient’s ‘current’ list and the ‘Past Medication’ are repeat and acute medications in the patient’s ‘removed’ list. A medication can be moved between ‘current’ and ‘removed’ lists <br/>
			<ul>
				<li>automatically if a drug hasn’t been issued for more than a configurable period, typically 6 months, it will be moved from ‘current’ to ‘removed’</li>
				<li>manually by the doctor in either direction</li>
			</ul>
		</td>
	  </tr>
	</tbody>
</table>

The following has been documented to explain the capture of cancelled/discontinued medication:

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Information</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>Acute medications will return an ‘Ended on’ label and the date ended in the Details column, repeat medications will return ‘Stopped:’ and the date stopped. A description from a coded list will be return along with any free text narrative if available.</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Does not distinguish between cancelled, discontinued or ended (always says expired for naturally ended).</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>Does not have a concept of cancelled. For discontinued medications they hold a date and reason within their system and this should be included in the details column. Note: INPS use the term de-activated in Vision as opposed to discontinued.</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Can only show that the medication has been actively stopped by a user. They do not hold the date or reason for the ending of a medication (these are not viewable in their GP system).</td>
	  </tr>
	</tbody>
</table>

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

There are no business rules associated with referrals.

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

There are no business rules associated with observations.

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
		<td>Contains observations with numeric and other measurement ranges.</td>
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

The following business rules apply for [immunisations](accessrecord_view_immunisations.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Rule</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>All immunisations recorded as Vaccinations are included. Immunisations recorded on SystmOne as Read codes (not using SystmOne's Vaccinations functionality) are not included in the Immunisations view. All Read coded immunisations will be included in the Encounters view.</td>
	  </tr>
	  <tr>
		<td><b>EMIS</b></td>
		<td>Includes a record of an invitation for a vaccination and consent / refusal for vaccinations in addition to immunisations administered.</td>
	  </tr>
	  <tr>
		<td><b>Vision</b></td>
		<td>N/A</td>
	  </tr>
	  <tr>
		<td><b>Microtest</b></td>
		<td>Microtest don't have a recognizable Immunisations 'table'; immunisations are extracted from their Recalls & History repositories based on the following Read Codes; <br/>
        7L1gz14b65670670068N8BMb.8BQ1.8I238MC8ME9DN9ki9Oo9OXZV03ZV04 where the code is less than five characters long it will include all codes below it in the Read2 hierarchy.</td>
	  </tr>
	</tbody>
</table>

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

The following business rules apply for [administrative items](accessrecord_view_administrative_items.html):

<table width="100%">
	<thead>
		<tr>
			<th width="15%">Supplier</th>
			<th width="85%">Rule</th>
		</tr>
	</thead>
	<tbody>
	  <tr>
		<td><b>TPP</b></td>
		<td>Returns practice-specific codes categorised as administrative. Codes are categorised as either clinical or administrative by default according to practice specific configuration. The default can be overridden by users. </td>
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
