---
title: Paramedic
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.40.html
summary: "Use case for paramedic"
---

## Brief description 

A paramedic is visiting a patient who has collapsed at home and needs to ascertain whether the patient has a Do Not Resuscitate (DNR) order recorded on the GP system, and the date it was recorded. Ideally, the paramedic would be able to see DNR history and associated information such as whether the patient and family are aware of the decision.

They should also be able to access an uploaded document, if it exists.

The paramedic has access to a mobile EPR system.

The flow of data will be from the GP practice clinical system to be viewed via the mobile EPR system.

Data needs to be supplied using SNOMED CT codes.

This use case will take place every time a paramedic with access to a mobile EPR system treats a patient. The expected volume of this happening is to be determined.

## Use case justification 

Although a paramedic may make an independent clinical decision about whether to resuscitate, it is best practice to check whether earlier decisions have been made. Decisions are currently recorded on paper forms which are left with the patient. In an urgent situation it is often hard to locate the document, which means that patients can receive inappropriate and undignified treatment.

## Primary actors 

- paramedic
- mobile EPR system

**Secondary actors 

- patient

**Triggers 

- attending paramedic is informed/is aware that a patient has collapsed and is unconscious (may be en route or in attendance)

## Preconditions 

  - patient is registered on mobile EPR; NHS Number is available
  - the mobile EPR can access the GP information
  - the paramedic has the relevant permissions to access the information
  - the patient has consented to share the information
  - DNR is recorded as one of a set of possible clinical codes in the patient's medical record on the GP system

## Postconditions 

  - **On success:**
    
      - the patient receives the most appropriate and timely treatment

  - **Guaranteed:**
    
      - the patient receives safe treatment
      - access is recorded for auditing purposes
      - information on which decisions are made is available for critical incident review/medico-legal investigation

## Basic flow with alternative and exception flows 

<table>
<thead>
<tr class="header">
<th width="10%"><strong>Step</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr class="even">
<td>Step 1</td>
<td>Paramedic accesses patient information on their mobile EPR.</td>
</tr>
<tr class="odd">
<td>Step 2</td>
<td>The EPR identifies the patient's GP practice endpoint using PDS/SDS lookup.</td>
</tr>
<tr class="even">
<td>Step 3</td>
<td>The EPR requests to see all “Do Not Resuscitate” clinical codes and their accompanying data record for the patients from their registered GP practice.
<p>The API call includes a list of SNOMED CT codes to be looked for.</p></td>
</tr>
<tr class="odd">
<td>Step 4</td>
<td>Spine Security Proxy (SSP) checks organisation to organisation sharing agreement exists between requesting organisation (Paramedic) and the patient's register GP practice, and that the interaction (for example, Get Problem/Condition) is part of the sharing agreement.</td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>GP practice clinical system checks patient permissions and consent to share.</td>
</tr>
<tr class="odd">
<td>Step 6</td>
<td>The EPR receives any Do Not Resuscitate clinical codes that are found.
<p>The following information is returned with the DNR clinical codes:</p>
<ul>
<li><p>That there is a DNR clinical code on the system</p></li>
<li><p>Is the DNR active</p></li>
<li><p>When the DNR was recorded</p></li>
<li><p>Full history of the DNR (if it has changed back and forth in the past)</p></li>
<li><p>Who has been made aware of the DNR (does the family know)</p></li>
</ul>
<p>The following information is an optional return if it is supported/available:</p>
<ul>
<li><p>Any documents recorded with the DNR clinical code (for example, a signed instruction from the patient)</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 7</td>
<td>The EPR will present the DNR and accompanying information to the paramedic.</td>
</tr>
<tr class="odd">
<td>Step 8</td>
<td>The paramedic takes account of this information in their treatment of the patient.</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>The DNR information is recorded on the EPR for use in critical incident review/medico-legal investigation.</td>
</tr>
<tr class="odd">
<td>Step 2a</td>
<td>GP practice is not found on SDS.</td>
</tr>
<tr class="even">
<td>Step 2b</td>
<td>The EPR advises the paramedic that it cannot access the patient's GP practice record as the GP practice cannot be found.</td>
</tr>
<tr class="odd">
<td>Step 4a</td>
<td>SSP sharing agreement between 'to' organisation and 'from' organisation doesn't exist.</td>
</tr>
<tr class="even">
<td>Step 4b</td>
<td>The EPR advises the paramedic that it cannot access the patient's GP practice record as it does not have permission to access the data.</td>
</tr>
<tr class="odd">
<td>Step 5.1a</td>
<td>The patient is not found on the GP practice clinical system.</td>
</tr>
<tr class="even">
<td>Step 5.1b</td>
<td>The EPR advises the paramedic that it cannot access the patient's GP practice record as the patient is not registered at the GP practice.</td>
</tr>
<tr class="odd">
<td>Step 5.2a</td>
<td>The patient has not consented to the sharing of medical data from the GP practice.</td>
</tr>
<tr class="even">
<td>Step 5.2b</td>
<td>The EPR advises the paramedic that it cannot access the patient's GP practice record as the patient has refused permission.</td>
</tr>
<tr class="odd">
<td>Step 6a</td>
<td>There is no DNR clinical coding recorded.</td>
</tr>
<tr class="even">
<td>Step 6b</td>
<td>The EPR advises the paramedic that there is no DNR recorded for the patient.</td>
</tr>
</tbody>
</table>

