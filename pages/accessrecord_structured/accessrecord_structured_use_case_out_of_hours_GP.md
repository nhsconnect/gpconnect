---
title: Access for out-of-hours GP
keywords: access record structured, use case, retrieve
tags: [accessrecord_structured,use_case]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_use_case_out_of_hours_GP.html
summary: "Use case for out-of-hours GP accessing patient’s medications, allergies and problems"
---

## Use case ##

**Out-of-hours (OOH) GP accesses medications, allergies and problems.**

A patient calls the out-of-hours GP complaining of pain and asking for painkillers.

The OOH GP wants to check:
-	what medications the patient is already taking
-	what they were prescribed for
-	when they were last issued, and how many
-	what allergies the patient may have

The GP has access to an electronic patient record system (EPR). The flow of information is from the GP practice clinical system to the OOH EPR. Data needs to be supplied using SNOMED CT codes.<br>
This use case will take place every time an OOH GP appointment takes place. The expected volume of this happening is to be determined.

## Use case justification ##

Without this information the OOH GP will have to make a judgement on whether it is safe to prescribe the medication the patient is asking for.

## Primary actors ##

-	OoH GP
-	OoH EPR

## Secondary actors ##

-	patient

## Triggers ##

-	clinical consultation

## Preconditions ##

-	the patient is registered on the OOH EPR; NHS number is available
-	the OOH EPR can access the GP information 
-	the OOH GP has the relevant permissions to access the information 
-	the patient has consented to share the information
-	the information is real-time

## Postconditions ##

**On success:**

-	the GP is able to prescribe the most appropriate medication

**Guaranteed:**

-	the GP will make a clinical decision based on the information they have
-	access is recorded for auditing purposes
-	information on which decisions are made is available for critical incident review/medico-legal investigation

## Basic flow with alternative and exception flows ##


<table>
	<tr>
		<th>Step number</th><th>Step description</th>
	</tr>
	<tr>
		<td>Step 1</td><td>OOH GP accesses patient  information on their EPR.</td>
	</tr>
	<tr>
		<td>Step 2</td><td>The  EPR identifies the patient’s GP practice endpoint using Spine Directory Service  (SDS)/Personal Demographics Service (PDS) lookup.</td>
	</tr>
	<tr>
		<td>Step 3</td><td>The  EPR requests to see the patient’s medications and allergies from their  registered GP practice. <br>The requirement  is for the full history of the patient’s medications. It will be the  responsibility of the EPR to present them in a clear way to the OOH GP.</td>
	</tr>
	<tr>
		<td>Step 4</td><td>Spine  Security Proxy (SSP) checks that organisation to organisation sharing  agreement exists between requesting organisation (OOH GP) and the patient’s  register GP practice, and that the interaction (for example, Get Problem/Condition)  is part of the sharing agreement.</td>
	</tr>
	<tr>
		<td>Step 5</td><td>GP  practice clinical system checks patient permissions and consent to share.</td>
	</tr>
	<tr>
		<td>Step 6</td>
		<td>The  EPR receives the Do Not Resuscitate Problem/Condition. The  following information is returned with the following information:<br/>
			<br/>
			<b>Medications</b>
			<ul>
				<li> Medication Name</li>
				<li> Medication Form</li>
				<li> Route</li>
				<li> Dose</li>
				<li> Medication frequency</li>
				<li> Additional instructions</li>
				<li> Do not discontinue warning</li>
				<li> Reason for medication</li>
				<li> Medication recommendations</li>
				<li> Medication status</li>
				<li> Medication change</li>
				<li> Reason for medication change</li>
				<li> Medicine administered</li>
				<li> Reasons for non-administration</li>
				<li> Relevant previous medications</li>
				<li> Medical devices</li>
			</ul>
			
			<br/>
			<b>Allergies</b>
			<ul>
				<li> Allergic  Substance</li>
				<li> Reaction  Type</li>
				<li> Reaction  Severity</li>
				<li> Date  Added</li>
				<li> Reported  By (clinician, patient) – preferred but optional</li>
				<li> Confirmed  by Clinician – preferred but optional</li>
			</ul>
			
			<br/>
			<b>GP  Connect API Search Criteria</b>
			<ul>
				<li>Search  MedicationStatement by:
					<ul>
						<li>Patient  (using NHS Number)</li>
						<li>Status  (active and completed)</li>
						<li>LastIssueDate  (see above for timeframes)</li>
					</ul>
				</li>
				<li>Include  MedicationOrder by:
					<ul>
						<li>All  Medication Orders linked to the MedicationStatement</li>
					</ul>
				</li>
				<li>Search  Allergies by:
					<ul>
						<li>Patient  (using NHS number)</li>
					</ul>
				</li>
			</ul>
			
			<br/>
			*Taken from <a href="pages/accessrecord_structured/Medication%20record.pdf" >Standards for  structure and content of medications and medical device records: technical  annex 2013</a> 
		</td>
	</tr>
	<tr>
		<td>Step 7</td><td>The  EPR will record the information locally.</td>
	</tr>
	<tr>
		<td>Step 8</td><td>The  information will be presented to the OOH GP. <br><br><b>Note:</b> This use case deliberately uses the supplied data  for presentation to the OOH GP only. Future use cases may look at using the  data supplied for decision support. However those  will only be progressed once the system is bedded and has a proven record of  retrieving the information without introducing errors.</td>
	</tr>
	<tr>
		<td>Step 9</td><td>The  information is recorded on the EPR for use in critical incident review/medico-legal  investigation.</td>
	</tr>
	<tr>
		<td>Step 2a</td><td>GP practice is not found on  SDS.</td>
	</tr>
	<tr>
		<td>Step 2b</td><td>The EPR advises the OOH GP  that it cannot access the patient’s GP practice record as the GP practice  cannot be found.</td>
	</tr>
	<tr>
		<td>Step 4a</td><td>SSP sharing agreement  between ‘to’ organisation and ‘from’ organisation doesn’t exist.</td>
	</tr>
	<tr>
		<td>Step 4b</td><td>The EPR advises the OOH GP  that it cannot access the patient’s GP practice record as it does not have  permission to access the data.</td>
	</tr>
	<tr>
		<td>Step 5.1a</td><td>The patient is not found on  the GP practice clinical system.</td>
	</tr>
	<tr>
		<td>Step 5.1b</td><td>The EPR advises the OOH GP  that it cannot access the patient’s GP practice record as the patient is not  registered at the GP practice.</td>
	</tr>
	<tr>
		<td>Step 5.2a</td><td>The patient has not  consented to the sharing of medical data from the GP practice.</td>
	</tr>
	<tr>
		<td>Step 5.2b</td><td>The EPR advises the OOH GP  that it cannot access the patient’s GP practice record as the patient has  refused permission.</td>
	</tr>
</table>

**Supporting document**

- [Out-of-hours GP access to patient record process](pages/accessrecord_structured/Out-of-hours%20GP%20access%20to%20patient%20record%20process.pdf)
