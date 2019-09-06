---
title: Community pharmacist providing spirometry services
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.38.html
summary: "Use case for community pharmacist providing spirometry services"
---

## Brief description 

The community pharmacist is certified to provide spirometry tests. Providing this service to patients can reduce the workload on the local GP practice(s) so the practice(s) can focus on higher priority or more critical services and thus the local GP practice(s) refer patients to the community pharmacist for tests rather than conduct them themselves. This will most commonly be for patients with asthma to check that the condition is being managed well.

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

  - the patient attends a certified Spirometry service at a community pharmacy

## Preconditions 

  - the patient has been referred to the spirometry service from their GP/primary care service
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
<td>The patient is referred to the community pharmacist for spirometry service by the GP and a patient record is created on the community pharmacy IT system.</td>
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
<li><p>Consultations (encounters) *</p></li>
<li><p>Medications</p></li>
<li><p>Referrals (especially certain agencies such as IAPs) *</p></li>
<li><p>Problems / long term conditions</p></li>
<li><p>Test Results relating to Spirometry</p></li>
<li><p>Allergies</p></li>
</ul>
<p>Items marked * could be time limited for a repeat patient to only return information since the last spirometry test.</p></td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>GP Connect presents the GP patient record to the community pharmacy system.</td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>The community pharmacy system presents the relevant parts of the GP record to the community pharmacist.</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The community pharmacist reviews the patient medical history, discusses with the patient about their condition and management thereof and performs the spirometry test as well as taking any other measurements required.</td>
</tr>
<tr class="odd">
<td>Step 9</td>
<td>The community pharmacist reviews the test results to check they are in range and consistent with the patient's condition and circumstances.</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td>The community pharmacist records the test results and returns the results to the registered GP system.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path 1</strong></td>
</tr>
<tr class="even">
<td>Steps 1 - 8</td>
<td>As above</td>
</tr>
<tr class="odd">
<td>Step 9</td>
<td>The community pharmacist notes that the results are out of range and along with the information available determines a change of medication may be required.</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td>As above, but additionally includes a recommendation for a change of medication.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path 2</strong></td>
</tr>
<tr class="even">
<td>Steps 1 - 8</td>
<td>As above</td>
</tr>
<tr class="odd">
<td>Step 9a</td>
<td>The community pharmacist notes that there is information within the medical history which is not consistent with the patient's test results and the patient's description of management of their condition. For example, the patient has had a number of hospital admissions for respiratory problems, but appears to be managing their asthma well and the test results are good.</td>
</tr>
<tr class="even">
<td>Step 9b</td>
<td>The community pharmacist considers whether there could be alternative problems, for example are respiratory problems being caused by a different condition. The community pharmacist seeks other evidence in the medical history, such as allergies which are not managed by medication, and thus could indicate possible anaphylaxis as cause of some respiratory problems.</td>
</tr>
<tr class="odd">
<td>Step 10</td>
<td>As above, but additionally includes details of any further problems/diagnosis and/or recommends medication changes.</td>
</tr>
</tbody>
</table>
