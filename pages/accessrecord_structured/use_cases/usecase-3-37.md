---
title: Community pharmacist providing diabetes services
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.37.html
summary: "Use case for community pharmacist providing diabetes services"
---

## Brief description 

The community pharmacist provides a diabetes service. Providing this service to patients can reduce the workload on the local GP Practice(s) so the Practice(s) can focus on higher priority or more critical services or provide greater convenience to the patient and thus the local GP Practice(s) refer patients to the community pharmacist.

## Use case justification 

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur
  - data can be formatted and filtered by the local system, so the clinician is presented the information they need in a suitable format
  - reducing the paper flow through departments by utilising the system workflow to manage tasks using staff time efficiently
  - reduction in clinical time wasted, away from the patient, collecting and collating information

Patient-focused:

  - increased patient safety due to the reduction in manual transcription errors
  - optimise the sign-posting of patients to the most appropriate endpoint taking into consideration patient-specific healthcare history and current concerns
  - better patient experience as they are not being asked for information which should already be available to the GP

## Primary actors 

  - GP
  - community pharmacist
  - GP Connect
  - community pharmacy IT system
  - GP clinical systems

## Secondary actors 

  - patient

## Triggers 

  - the patient attends a diabetes service at a community pharmacy

## Preconditions 

  - the patient has been referred to the diabetes service from their GP/primary care service
  - the patient's details have been verified and entered on the community pharmacy IT system
  - the community pharmacist has the correct/appropriate system access rights
  - the patient's GP (practice/federation) has agreed to share patient information via GP Connect with the community pharmacy
  - the patient consents to this shared information being viewed/used
  - electronic interactions between GP clinical system/GP Connect/community pharmacy IT system have been correctly configured

## Postconditions 

  - **On success:**
    
      - the information provided by GP Connect is used to inform the community pharmacist of all the patient's relevant medical history such that the community pharmacist can provide the best possible advice regarding the patient's condition

  - **Guaranteed:**
    
      - the patient is appropriately assessed according to the test results and any information the patient provides

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
<td>The patient is referred to the community pharmacist for diabetes service by the GP and a patient record is created on the community pharmacy IT system.</td>
</tr>
<tr class="even">
<td>Step 2</td>
<td>The community pharmacist accesses the patient record in the community pharmacy system.</td>
</tr>
<tr class="odd">
<td>Step 3</td>
<td>The community pharmacist accesses GP Connect to retrieve the medical history from the patient's registered GP system.</td>
</tr>
<tr class="even">
<td>Step 4</td>
<td>GP Connect requests GP patient record from the GP clinical system.</td>
</tr>
<tr class="odd">
<td>Step 5</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include (but not limited to):</p>
<ul>
<li><p>Consultations (encounters)</p>
<ul>
<li><p>Date</p></li>
<li><p>Details from consultations which might include information of conditions/diagnoses which would affect diabetes test results and whether GP/patient have accepted that a condition has impacted a test result.</p></li>
</ul></li>
<li><p>Medications</p></li>
<li><p>Problems / long term conditions / diagnoses</p></li>
<li><p>Test Results relating to diabetes</p>
<ul>
<li><p>Measure - for example, glucose levels, blood pressure, kidney function, liver function, etc.</p></li>
<li><p>Measured value</p></li>
<li><p>Date of measurement</p></li>
</ul></li>
<li><p>Allergies</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>GP Connect presents the GP patient record to the community pharmacy system.</td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>The community pharmacy system presents the relevant parts of the GP record to the community pharmacist.
<p>The test results are displayed in graph form by type of measure with indication of either normal max/min range values or highlighting out of range measurement values.</p></td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The community pharmacist reviews the test results looking for trends and/or changes/anomalies and checks with the patient whether the medication is being taken as advised (or any circumstances why it is not).
<p>The community pharmacist cross checks with the patient medical history where there are any changes or anomalies to see if there is an indication of the cause and whether any action had been taken.</p></td>
</tr>
<tr class="odd">
<td>Step 9</td>
<td>The community pharmacist assesses the information available and advises the patient to continue with current medication, advised adjustments or recommends a medication review with the GP.</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td>The community pharmacist records details of the advice given and any recommendations for changes to medication and justification for the proposed changes.</td>
</tr>
<tr class="odd">
<td>Step 11</td>
<td>The community pharmacy system passes the information to the GP system for action and/or as a record of the review.</td>
</tr>
</tbody>
</table>
