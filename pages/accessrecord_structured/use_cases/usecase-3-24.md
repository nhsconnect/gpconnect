---
title: Practice nurse administering a vaccination
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.24.html
summary: "Use case for practice nurse administering a vaccination"
---

## Brief description

A practice nurse may administer a range of vaccinations. The vaccination may be of a specific type as part of a vaccination program for example, seasonal flu vaccination, or the vaccination may need to be determined according to discussion with the patient as to their specific circumstances - for example, travel vaccination. Most vaccinations will be administered to patients registered to the practice, but some circumstances may arise through hubs and specialist services (for example,  Yellow Fever vaccination). There are certain checks which need to be performed to ensure the vaccination they are giving is safe and appropriate for the patient. These checks can be assisted through access to the patient record.

## Use case justification

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur
  - reduction in transcription between systems and paper to IT, leading to a reduction in prescribing errors
  - reduction in clinical time wasted, away from the patient, collecting and collating information
  - reduction in clinical time wasted, away from the patient, manually updating IT systems
  - reducing the paper flow through departments by utilising the system workflow to manage tasks using staff time efficiently

Patient-focused:

  - security of patient information is maintained and improved through the reduction of paper-based 'patient identifiable documents' in use within departments
  - increased patient/clinician time due to reduction in clinician time spent collecting and transcribing information away from the patient
  - increased patient safety due to the reduction in manual transcription errors
  - better patient experience as they are not being asked for information which should already be available to the pharmacist

## Primary actors

  - practice nurse
  - GP Connect
  - GP clinical systems

## Secondary actors

  - patient
  - travel vaccination knowledge base

## Triggers

  - patient attends a GP practice for a vaccination

## Preconditions

  - the patient's details have been verified and entered on the GP system upon attendance
  - the practice nurse has the correct/appropriate system access rights
  - the patient's GP has agreed to share patient information via GP Connect
  - the patient consents to this shared information being viewed/used by the practice nurse
  - electronic interactions between GP clinical system/GP Connect/GP clinical system have been correctly configured

## Postconditions

  - **On success:**
    
      - the patient's medical record is made available to the practice nurse

  - **Guaranteed:**
    
      - the practice nurse will treat the patient based on the information available

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
<td>Patient attends the practice.</td>
</tr>
<tr class="even">
<td>Step 2</td>
<td>The practice nurse identifies need to establish the patient's medication history.</td>
</tr>
<tr class="odd">
<td>Step 3</td>
<td>The practice nurse accesses the GP system to retrieve GP patient record history. The GP system requests the GP patient record from GP Connect.</td>
</tr>
<tr class="even">
<td>Step 4</td>
<td>GP Connect requests GP patient record from the GP clinical system.</td>
</tr>
<tr class="odd">
<td>Step 5</td>
<td><p>GP clinical system provides the GP patient record to GP Connect.</p>
<p>The GP patient record will include:</p>
<ul>
<li><p>Allergies</p>
<ul>
<li><p>Check if allergic to vaccination ingredients (example: egg).</p></li>
</ul></li>
<li><p>Vaccinations</p>
<ul>
<li><p>Check if vaccination has already been given (or not).</p></li>
<li><p>Ability to sort/filter/search for a specific vaccine or vaccination type.</p></li>
<li><p>Review the details of the vaccination, including but not limited to:</p>
<ul>
<li><p>Date(s) administered</p></li>
<li><p>Vaccine</p></li>
<li><p>Vaccination type</p></li>
<li><p>Single or part of a course (sequence number).</p></li>
</ul></li>
</ul></li>
<li><p>Conditions/problems</p>
<ul>
<li><p>Check the patient is not immunosuppressed as some vaccinations are unsafe.</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>GP Connect presents the GP patient record to the GP system.</td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>The GP system presents the GP patient record to the practice nurse.</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The practice nurse uses the information to assist in determining if the vaccination is safe and appropriate.</td>
</tr>
<tr class="odd">
<td>Step 9</td>
<td>Subject to confirming it is safe to administer the vaccine, the practice nurse discusses the vaccination and any potential side effects. Practice nurse obtains consent to administer the vaccine.</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td><p>Practice nurse administers the vaccine and records.</p>
<ul>
<li><p>Details of the vaccine administered</p></li>
<li><p>Any pertinent background information, information given and details of consent.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path - Travel Vaccination</strong></td>
</tr>
<tr class="even">
<td>Step 4a</td>
<td>The practice nurse needs to determine the vaccine to be administered for a travel vaccination to determine what checks to perform. The practice nurse will establish the travel destination along with additional factors related to the trip which may impact the vaccinations required - for example, length of stay, type of accommodation, regions travelling to, purpose of travel. The practice nurse will check an online resource to get the latest recommendations (which may change over time) for the destination and circumstances.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path - Vaccination Criteria</strong></td>
</tr>
<tr class="even">
<td>Step 5a</td>
<td><p>The vaccination to be administered requires certain criteria/health checks for it to be safely administered.</p>
<ul>
<li><p>Observations</p>
<ul>
<li><p>Check for pertinent measurement(s) - for example, child's weight.</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path - Vaccine Not Administered</strong></td>
</tr>
<tr class="even">
<td>Step 8a</td>
<td>The medical checks indicate that the vaccine has already been administered and immunity has not expired or that it would be unsafe to administer the vaccine. Process stops and does not progress to Step 9. The vaccine is not administered.</td>
</tr>
<tr class="odd">
<td>Step 9a</td>
<td>The patient does not give consent to the vaccination. The practice nurse captures the refusal and any pertinent details. The process stops and does not progress to Step 10. The vaccine is not administered.</td>
</tr>
</tbody>
</table>
