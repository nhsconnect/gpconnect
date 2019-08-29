---
title: Out of hours (OOH) assessment of potential measles case
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.32.html
summary: "Use case for OOH assessment of potential measles case"
---

## Brief description

A child becomes unwell over the weekend. The child's parent/guardian is very concerned and contacts the out of hours service which is based at the hub which is not the child's registered practice and is using a different GP system. The parent explains that their child has a rash and a high temperature amongst other symptoms. The details are passed to the GP to assess the urgency and respond to the parent/guardian.

The GP considers the possibility of measles and so uses the GP Connect record to check whether the MMR vaccination has been administered and to its full course. The GP retrieves the immunisation history and searches for an MMR vaccination so as to inform further actions.

## Use case justification

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur
  - reduction in clinical time wasted, away from the patient, collecting and collating information

Patient-focused:

  - increased patient safety due to the reduction in manual transcription errors
  - better patient experience as they are not being asked for information which should already be available to the GP

## Primary actors

  - GP
  - GP Connect
  - GP clinical systems

## Secondary actors

  - patient
  - patient's parents or guardians

## Triggers

  - parent/guardian contacts an out of hours service and reports measles-like symptoms to the call handler who passes the information to the out of hours GP

## Preconditions

  - the patient's details have been verified and entered on the GP clinical system
  - the GP has the correct/appropriate system access rights
  - the patient's GP has agreed to share patient information via GP Connect
  - the patient's parent/guardian consents to this shared information being viewed/used
  - electronic interactions between GP clinical system/GP Connect/GP clinical system have been correctly configured

## Postconditions

  - **On success:**
    
      - the information provided by GP Connect is used to inform the GP of the likelihood of the child having measles and how best to seek further information from the parents/advice on an appointment in person

  - **Guaranteed:**
    
      - the child is appropriately assessed according to the information available from the parent/guardian and further consultation if required

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
<td>The GP received the information from the parent's/guardian's call to the out of hours service.</td>
</tr>
<tr class="even">
<td>Step 2</td>
<td>The GP accesses the child's temporary record.</td>
</tr>
<tr class="odd">
<td>Step 3</td>
<td>The GP accesses GP Connect to retrieve the medical and other history from the child's registered GP system.</td>
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
<li><p>Immunisation</p>
<ul>
<li><p>Date</p></li>
<li><p>Vaccine</p></li>
<li><p>Vaccine Type</p></li>
<li><p>Part (of course)</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>GP Connect presents the GP patient record to the GP system.</td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>The GP system presents the GP patient record to the GP.</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The GP scans the immunisations list for an MMR or single Measles vaccination.</td>
</tr>
<tr class="odd">
<td>Step 9</td>
<td>The GP identifies a record of full Measles vaccination (MMR or single).</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td>The GP responds to the out of hours contact knowing Measles is not the most likely diagnosis.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path - Measles vaccination refused.</strong></td>
</tr>
<tr class="even">
<td>Steps 1 - 7</td>
<td>As above</td>
</tr>
<tr class="odd">
<td>Step 8</td>
<td>The GP does not find a record of Measles vaccination in any form in the immunisation list.</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>The GP performs a search by vaccine type for Measles/MMR with no results found.</td>
</tr>
<tr class="odd">
<td>Step 10</td>
<td>The GP searches other sources for any information that could indicate the Measles/MMR vaccination is due to be administered elsewhere or has been refused (Consent/Refusal Records, Consultations, and so on.)</td>
</tr>
<tr class="even">
<td>Step 11</td>
<td>The GP requests consultation notes as per steps 3 - 7.</td>
</tr>
<tr class="odd">
<td>Step 12</td>
<td>The GP performs keyword searches for narrative relating to Measles or MMR.</td>
</tr>
<tr class="even">
<td>Step 13</td>
<td>The GP finds recent consultation notes concerning the MMR vaccination having been refused by the parents who intend to seek single vaccinations privately.</td>
</tr>
<tr class="odd">
<td>Step 14</td>
<td>The GP responds to the out of hours contact considering Measles a potential diagnosis and seeks further information from the parent as to whether the Measles vaccination has been administered and when it was administered as well as further discussion of the child's symptoms.</td>
</tr>
</tbody>
</table>
