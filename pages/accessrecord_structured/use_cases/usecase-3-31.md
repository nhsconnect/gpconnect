---
title: Community cardiac nurse
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.31.html
summary: "Use case for community cardiac nurse"
---

## Brief description 

The community cardiac nurse provides rehabilitation and care for patients recovering from cardiac illness, heart operations, heart attacks and heart failure. This may be through clinics or home visits. The aim is to provide a breadth of support to aid recovery and prevent re-admissions to hospital.

The community care nurse needs access to a variety of information which may already be captured in health systems, such as the GP record. The community care nurse will utilise the information to populate elements of the clinical assessment. The community care nurse may also request tests and medication changes via the GP and may wish to track progress on these or view the results. The GP record may contain information to support decision making such as allergy information, social history or mental capacity. The community nurse will need to monitor certain information to see trends - for example, changes over time to a medication dosage, blood pressure results. The community care nurse will also monitor for general wellbeing to check the necessary care and support is being delivered.

Providing access to the structured data will enable the consumer system to incorporate features such as pulling data directly into the clinical assessment, displaying information alongside the clinical assessment to aid decision making and task management, pulling back specific information such as blood test result or mapping information to show trends.

## Use case justification 

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur
  - reduction in clinical time wasted, away from the patient, collecting and collating information
  - reduction in clinical time wasted, away from the patient, manually updating IT systems
  - data can be formatted and filtered by the local system, so the clinician is presented the information they need in a suitable format
  - share more relevant data, pertinent to the role of the professional involved and improve care delivery

Patient-focused:

  - increased patient/clinician time due to reduction in clinician time spent collecting and transcribing information away from the patient
  - increased patient safety due to the reduction in manual transcription errors
  - better patient experience as they are not being asked for information which should already be available to the community healthcare service

## Primary actors 

  - Community healthcare team
  - GP Connect
  - GP clinical systems
  - Community healthcare system

## Secondary actors 

  - patient

**Triggers 

  - patient has been referred to the Community Cardiac Service for rehabilitation for some form of heart condition

## Preconditions 

  - the patient's details have been verified and entered on the community healthcare system (or created by an electronic referral)
  - the community cardiac nurse has the correct/appropriate system access rights
  - the patient's GP has agreed to share patient information via GP Connect
  - the patient consents to this shared information being viewed/used
  - electronic interactions between GP clinical system/GP Connect/community healthcare system have been correctly configured

## Postconditions 

  - **On success:**
    
      - the community cardiac nurse plans and enacts the most appropriate care and support through the information on the patient's medical history and personal circumstances

  - **Guaranteed:**
    
      - the community cardiac nurse will assess the patient's needs based on the information available

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
<td colspan="2"><strong>Main Path - New Referral</strong></td>
</tr>
<tr class="even">
<td>Step 1</td>
<td>Patient is referred to the community cardiac service.</td>
</tr>
<tr class="odd">
<td>Step 2</td>
<td>A patient record is either retrieved on the community healthcare system (previous patient) or a new patient record is created.</td>
</tr>
<tr class="even">
<td>Step 3</td>
<td>The community cardiac nurse accesses GP Connect to retrieve the patient medical and other history from the GP system.</td>
</tr>
<tr class="odd">
<td>Step 4</td>
<td>GP Connect requests GP patient record from the GP clinical system.</td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include:</p>
<ul>
<li><p>Current Medications</p>
<ul>
<li><p>Date</p></li>
<li><p>Drug Name</p></li>
<li><p>Dosage</p></li>
<li><p>Issues</p></li>
</ul></li>
<li><p>Test Requests</p>
<ul>
<li><p>Date Requested</p></li>
<li><p>Type of Test (for example,  Blood Test)</p></li>
<li><p>Detailed Tests Requested</p></li>
</ul></li>
<li><p>Observations (Date and values for)</p>
<ul>
<li><p>Blood Test Results</p></li>
<li><p>Blood Pressure Measurements</p></li>
<li><p>Cholesterol Levels</p></li>
</ul></li>
<li><p>Open/Recent Referrals</p>
<ul>
<li><p>Date</p></li>
<li><p>Organisation/Professional</p></li>
<li><p>Service Requested/Care Provided</p></li>
</ul></li>
<li><p>Problems/Diagnoses/Conditions (Past Medical History - filtered to or enabling searching for items relevant to cardiac care such as hypertension, diabetes, asthma, etc.).</p></li>
<li><p>Care Plans</p>
<ul>
<li><p>Date</p></li>
<li><p>Event (only Medication Review required)</p></li>
</ul></li>
<li><p>Encounters</p>
<ul>
<li><p>Date</p></li>
<li><p>Purpose (for example, dressing change)</p></li>
<li><p>Clinician</p></li>
<li><p>Narrative</p></li>
</ul></li>
<li><p>Social History (including but not limited to)</p>
<ul>
<li><p>Smoking</p></li>
<li><p>Exercise</p></li>
<li><p>Diet</p></li>
<li><p>Alcohol</p></li>
</ul></li>
<li><p>Family History of Heart Conditions</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>Step 6</td>
<td>GP Connect presents the GP patient record to the community healthcare system.</td>
</tr>
<tr class="even">
<td>Step 7</td>
<td>The community healthcare system imports and/or displays the information according to its design and the data returned.</td>
</tr>
<tr class="odd">
<td>Step 8</td>
<td>The community cardiac nurse will review the information as imported into the clinical assessment/transfer the relevant information into the clinical assessment.</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>The community cardiac nurse can plan the appropriate care and support with the patient based on the available information.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path 1 - Check For Latest Seasonal Flu Vaccination</strong></td>
</tr>
<tr class="even">
<td>Step 1</td>
<td>Community Cardiac Nurse is due to meet the patient and seasonal flu vaccinations are due.</td>
</tr>
<tr class="odd">
<td>Steps 2 - 4</td>
<td>As main flow</td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include:</p>
<ul>
<li><p>Immunisations</p>
<ul>
<li><p>Invitation for Seasonal Flu Vaccine (incl. date of invite)</p></li>
<li><p>Vaccinations</p>
<ul>
<li><p>Type (for example, seasonal flu vaccine)</p></li>
<li><p>Date Administered</p></li>
<li><p>Refusal of Vaccination</p></li>
</ul></li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td>Steps 6 - 7</td>
<td>As main flow (information only needs to be displayed not imported)</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The community cardiac nurse will review the information and encourage the uptake of the seasonal flu vaccine if it is due and has not been administered.</td>
</tr>
<tr class="odd">
<td>End</td>
<td></td>
</tr>
<tr class="even">
<td colspan="2"><strong>Alternative Path 2 - Mental Capacity Check</strong></td>
</tr>
<tr class="odd">
<td>Step 1</td>
<td>Community Cardiac Nurse is meeting with the patient for the first time and needs to obtain consent for care but has concern about mental capacity.</td>
</tr>
<tr class="even">
<td>Steps 2 - 4</td>
<td>As main flow</td>
</tr>
<tr class="odd">
<td>Step 5</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include:</p>
<ul>
<li><p>Referrals (filtered to or enabling searching for referrals to services for memory tests or mental health)</p></li>
<li><p>Current Medications</p></li>
<li><p>Current Problems/Diagnoses/Conditions</p></li>
<li><p>Specific Current Mental Health status/issues</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Steps 6 - 7</td>
<td>As main flow (information only needs to be displayed not imported)</td>
</tr>
<tr class="odd">
<td>Step 8</td>
<td>Community Cardiac Nurse reviews the information for any content which would support a decision related to longer term or temporary mental capacity.</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>Community Cardiac Nurse uses own observations, conversations and information supported by the GP record to decide whether the patient has mental capacity or to temporarily defer the decision.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path 3 - Monitoring against a Medication Plan</strong></td>
</tr>
<tr class="even">
<td>Step 1</td>
<td>Community Cardiac Nurse is supporting the patient who is on a plan which increases the dosage of medication over time subject to no adverse reactions.</td>
</tr>
<tr class="odd">
<td>Steps 2 - 4</td>
<td>As main flow</td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include:</p>
<ul>
<li><p>Medication Issues (filtered to the medications on the plan)</p>
<ul>
<li><p>Date</p></li>
<li><p>Drug Name</p></li>
<li><p>Dosage</p></li>
</ul></li>
<li><p>Allergies/Adverse Reactions (relating to the period of the plan)</p></li>
<li><p>Recent Encounters (relating to the period of the plan)</p>
<ul>
<li><p>Date</p></li>
<li><p>Purpose</p></li>
<li><p>Clinician</p></li>
<li><p>Narrative</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td>Step 6</td>
<td>As main flow</td>
</tr>
<tr class="even">
<td>Step 7</td>
<td>The community health system displays the information received from GP Connect is an appropriate format to enable easy identification of trends (for example, graph(s) of dosage for a medication over time) and to establish whether the dosage increase is happening according to plan or any supporting evidence as to why the increase has not happened.</td>
</tr>
<tr class="odd">
<td>Step 8</td>
<td>The community cardiac nurse reviews the information and determines whether the plan is being followed or whether there are appropriate reasons why not</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>The community cardiac nurse acts to query why the medication has not been increased/review the medication, continues to support the patient with rehabilitation according to the plan or discharges the patient as the plan is complete.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path 4a - Blood Test Results</strong></td>
</tr>
<tr class="even">
<td>Step 1</td>
<td>Community Cardiac Nurse has requested blood tests via the patient's GP practice (standard process to book blood tests via the GP).</td>
</tr>
<tr class="odd">
<td>Steps 2 - 4</td>
<td>As main flow</td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include:</p>
<ul>
<li><p>Diagnostic Report (filtered for the latest blood tests by type / date or a known ID if applicable)</p>
<ul>
<li><p>Date</p></li>
<li><p>Test Description</p></li>
<li><p>Diagnostic Summaries</p></li>
<li><p>Results (as Observations)</p></li>
</ul></li>
<li><p>Observations (related to the Diagnostic Report)</p>
<ul>
<li><p>Blood test type</p></li>
<li><p>Result</p></li>
<li><p>Out of Range Indicator</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td>Step 6</td>
<td>As main flow</td>
</tr>
<tr class="even">
<td>Step 7</td>
<td>The community healthcare system reconstructs the diagnostic report from the GP Connect data.</td>
</tr>
<tr class="odd">
<td>Step 8</td>
<td>The community cardiac nurse reviews the report and determines is any actions are required as a consequence.</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>The community cardiac nurse discusses the results with the patient and any recommended actions.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path 4b - Blood Test Results Not Received</strong></td>
</tr>
<tr class="even">
<td>Steps 1 - 4</td>
<td>As Alternative Path 4a</td>
</tr>
<tr class="odd">
<td>Step 5</td>
<td>No results are returned by GP Connect (if requesting by a known value) or the latest diagnostic report for blood tests is prior to the latest request.</td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>Community healthcare system displays the results or no result message.</td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>The community cardiac nurse is aware that results have not been received for the related test request and searches for the test request.</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>GP clinical system provides the GP patient record to GP Connect.
<p>The GP patient record will include:</p>
<ul>
<li><p>Procedure Requests (filtered to blood test requests either by date range or a known value for the specific test request).</p>
<ul>
<li><p>Date Requested</p></li>
<li><p>Tests Requested</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td>Step 9</td>
<td>Community healthcare system displays the results or no result message.</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td>The community cardiac nurse can determine when to check again for the results or whether to check further regarding the test request.</td>
</tr>
</tbody>
</table>

Alternative Path 3 could have equivalent flows for observations instead of medication such as to monitor blood pressure measurements over time.
