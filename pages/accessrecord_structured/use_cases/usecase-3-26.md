---
title: Mental Health new referral daily triage
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.26.html
summary: "Use case for mental health new referral daily triage"
---

## Brief description

The mental health service holds a daily triage where the team comes together to review new referrals. The main (but not sole) source of referrals is from GPs. Currently the referrals are unstructured (paper based). The format of these referrals is inconsistent. The extent and quality of information varies significantly. Whilst some will be concise and informative, others will lack key information which it is likely the GP record holds, and others will contain extensive detail making the most salient points difficult to access quickly. The triage team are in the process of defining a “minimum dataset” they wish to request for the referral details.

It is thought that the referral process could be improved if the referral information could be captured in the GP systems in accordance with the minimum dataset and transmitting to the mental health service system in a structured format.

## Use case justification

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur
  - reduction in clinical time wasted, away from the patient, collecting and collating information
  - reduction in clinical time wasted, away from the patient, manually updating IT systems
  - reducing the paper flow through departments by utilising the system workflow to manage tasks using staff time efficiently

Patient-focused:

  - security of patient information is maintained and improved through the reduction of paper-based 'patient identifiable documents' in use within departments
  - increased patient/clinician time due to reduction in clinician time spent collecting and transcribing information away from the patient
  - increased patient safety due to the reduction in manual transcription errors
  - better patient experience as they are not being asked for information which should already be available to the mental health service

## Primary actors

  - Mental Health Triage Team (Mental Health Practitioner, Clinical Psychologist, etc.)
  - GP Connect
  - GP clinical systems
  - Mental Health Service system (PARIS)

## Secondary actors

  - patient

**Triggers

  - GP has referred a patient to the community mental health service

## Preconditions

  - the patient's details have been verified and entered on the community mental health system (or created by an electronic referral)
  - the mental health practitioner has the correct/appropriate system access rights
  - the patient's GP has agreed to share patient information via GP Connect
  - the patient consents to this shared information being viewed/used
  - electronic interactions between GP clinical system/GP Connect/community mental health system have been correctly configured

## Postconditions

  - **On success:**
    
      - the patient's referral details are made available to the triage team in a concise manner

  - **Guaranteed:**
    
      - the triage team will assess the patient needs based on the information available

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
<td>Patient is referred to the community mental health service.</td>
</tr>
<tr class="even">
<td>Step 2</td>
<td>A patient record is either retrieved on the community mental health system (previous patient) or a new patient record is created.</td>
</tr>
<tr class="odd">
<td>Step 3</td>
<td>The triage team access GP Connect to retrieve the referral information from the GP system.</td>
</tr>
<tr class="even">
<td>Step 4</td>
<td>GP Connect requests GP patient record from the GP clinical system.</td>
</tr>
<tr class="odd">
<td>Step 5</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include:</p>
<ul>
<li><p>Referral details (the current referral and any previous referrals to mental health services)</p>
<ul>
<li><p>Referral from</p></li>
<li><p>Date of referral</p></li>
<li><p>Type (for example, referral for mental health counselling)</p></li>
<li><p>Referral to</p></li>
<li><p>Summary of reason for referral</p></li>
<li><p>Outcome (for example,  Therapy offered and degree of success)</p></li>
</ul></li>
<li><p>Relevant medical history</p>
<ul>
<li><p>Relevant diagnosis</p></li>
<li><p>Indicator as to formal diagnosis or otherwise</p></li>
</ul></li>
<li><p>Risk (current and history)</p>
<ul>
<li><p>Harm to self or others</p></li>
<li><p>Details</p></li>
<li><p>Severity</p></li>
</ul></li>
<li><p>Motivation to engage</p>
<ul>
<li><p>Patient or other</p></li>
<li><p>Motivation level</p></li>
<li><p>Outcomes to be achieved</p></li>
<li><p>Reason to achieve the outcome</p></li>
<li><p>Patient expectations of the referral</p></li>
</ul></li>
<li><p>Medications</p>
<ul>
<li><p>Details of all current medications</p></li>
<li><p>History of psychotropic medications or others related to mental health conditions</p></li>
</ul></li>
<li><p>Social history (current and history)</p>
<ul>
<li><p>Substance abuse</p></li>
<li><p>Alcohol abuse</p></li>
</ul></li>
<li><p>Support systems in place (professional and family/non-professional)</p>
<ul>
<li><p>Contact name/role</p></li>
<li><p>Involvement</p></li>
<li><p>Influence on patient</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>GP Connect presents the GP patient record to the community mental health system.</td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>The community mental health system imports the information and presents it to the user/triage team.</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The triage team assess the referral and allocate the referral to the relevant professional for assessment or return to the GP requesting more relevant information.</td>
</tr>
</tbody>
</table>
