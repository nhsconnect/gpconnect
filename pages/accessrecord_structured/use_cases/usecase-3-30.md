---
title: Palliative care
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.30.html
summary: "Use case for palliative care"
---

## Brief description 

The community healthcare team needs to be aware of and support the end of life plans made by a patient and their representatives. The items relating to the palliative care need to be identified at the start of providing care and monitored for changes throughout the period of care. The details within the end of life plan will influence the care to be provided and the funding of that care. The elements of the end of life plan may change over time, so it is important to be able to check them quickly for the latest information.

Utilising structured record access enables a consumer system to draw together the necessary elements of the end of life plan, enable searching for specific elements and incorporate elements of the plan into local assessments or plan templates - for example, pull information into the Electronic Palliative Care Co-ordination System (EPaCCS) template.

## Use case justification 

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur
  - reduction in clinical time wasted, away from the patient, collecting and collating information
  - reduction in clinical time wasted, away from the patient, manually updating IT systems
  - data can be formatted and filtered by the local system, so the clinician is presented the information they need in a suitable format

Patient-focused:

  - increased patient/clinician time due to reduction in clinician time spent collecting and transcribing information away from the patient
  - increased patient safety due to the reduction in manual transcription errors
  - better patient experience as they are not being asked for information which should already be available to the community healthcare service

## Primary actors 

  - Community Healthcare Team
  - GP Connect
  - GP Clinical Systems
  - Community Healthcare System/EPaCCS

## Secondary actors 

  - patient
  - next of kin/carers/PoA

## Triggers 

  - patient has been referred to a Community Healthcare Team and is subject to an End of Life plan

## Preconditions 

  - the patient's details have been verified and entered on the community healthcare system (or created by an electronic referral)
  - the community healthcare nurse has the correct/appropriate system access rights
  - the patient's GP has agreed to share patient information via GP Connect
  - the patient consents to this shared information being viewed/used
  - electronic interactions between GP clinical system/GP Connect/community healthcare system have been correctly configured

## Postconditions 

  - **On success:**
    
      - the community healthcare team provide care in keeping with the wishes of the patient in their end of life plan

  - **Guaranteed:**
    
      - the community healthcare team will assess the patient needs based on the information available

## Basic flow with alternative and exception flows 

<table>
<thead>
<tr class="header">
<th width="10%"><strong>Step</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Step 1</td>
<td>Patient is referred to the community healthcare service.</td>
</tr>
<tr class="even">
<td>Step 2</td>
<td>A patient record is either retrieved on the community healthcare system (previous patient) or a new patient record is created.</td>
</tr>
<tr class="odd">
<td>Step 3</td>
<td>The community healthcare nurse accesses GP Connect to retrieve the palliative care information from the GP system.</td>
</tr>
<tr class="even">
<td>Step 4</td>
<td>GP Connect requests GP patient record from the GP clinical system.</td>
</tr>
<tr class="odd">
<td>Step 5</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include (plus any additional areas to cover the scope of step 7):</p>
<ul>
<li><p>Observations</p></li>
<li><p>Problems</p></li>
<li><p>Diagnoses / Conditions</p></li>
<li><p>Documents</p></li>
<li><p>Allergies</p></li>
<li><p>Medications</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>GP Connect presents the GP patient record to the community mental health system.</td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>The community healthcare system presents the information to the community healthcare nurse in a format to review or populates the information into its EPaCCS template so as to concisely identify the following information.
<ul>
<li><p>Advance Decisions / Living Will</p>
<ul>
<li><p>A copy of the Living Will</p></li>
<li><p>Details of individual decisions</p></li>
</ul></li>
<li><p>Power of Attorney</p>
<ul>
<li><p>Name</p></li>
<li><p>Contact Details</p></li>
<li><p>Authority to make life-sustaining decisions (true/false)</p></li>
</ul></li>
<li><p>Life expectancy prognosis</p></li>
<li><p>Gold Standard Framework (true / false)</p></li>
<li><p>Patient Understanding</p></li>
<li><p>Carer/Next of Kin details and understanding</p>
<ul>
<li><p>Name</p></li>
<li><p>Contact Details</p></li>
<li><p>Aware of prognosis</p></li>
<li><p>Aware of decisions</p></li>
</ul></li>
<li><p>DNACPR (true / false)</p></li>
<li><p>Preferred Place of Care</p></li>
<li><p>Preferred Place of Death</p></li>
<li><p>Additional Professional Contacts</p>
<ul>
<li><p>Name</p></li>
<li><p>Professional Group/Service provided</p></li>
<li><p>Contact Details</p></li>
</ul></li>
<li><p>Medication</p></li>
<li><p>Allergies</p></li>
<li><p>Test Results</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The community healthcare nurse reviews the end of life information from the GP clinical system to inform the care to be provided.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative path - existing patient with change to End of Life plan</strong></td>
</tr>
<tr class="even">
<td>Step 1</td>
<td>The community healthcare nurse is providing ongoing palliative care.</td>
</tr>
<tr class="odd">
<td>Step 2 - 7</td>
<td>As above</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The community healthcare nurse can see whether the GP clinical system has any records of changes to the patients end of life care plans or supporting information and can provide the appropriate care and support.</td>
</tr>
</tbody>
</table>
