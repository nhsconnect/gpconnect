---
title: 111/999 call handler
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.39.html
summary: "Use case for 111/999 call handler"
---

## Brief description 

A patient calls 111/999 and the call handling system is able to interrogate the GP system to search for information that the patient is end of life.

The flow of information will be from the GP system to the call handling system.

Data needs to be supplied using SNOMED CT codes.

This use case will take place every time a call takes place. The expected volume of this happening is to be determined.

Similar use cases could be developed to flag other key conditions that would impact how a call is handled such as the patient being diagnosed with Learning Difficulties, Diabetic, etc.

## Use case justification 

If a call handler is aware that the caller is an end of life patient they will amend their response to the call ensuring that the patient gets the most appropriate outcome.

Currently, without this information, they have to go through the pathways modules and follow the dispositions which are produced.

## Primary actors 

- 111/999 call handler
- call handling system

## Secondary actors 

- patient

## Triggers 

- the information is searched for automatically once the patient's ID has been established

## Preconditions 

  - the patient's NHS Number is available to the call handling system
  - the call handler has the relevant permissions to access the information
  - the call handling system is able to interact automatically with the GP system (or proxy)
  - the information is presented to the call handler early in the call
  - the patient has consented to share their data
  - end of life is recorded as one of a set of possible clinical codes in the patient's medical record on the GP system
  - there is an agreed workflow for patients with an end of life status which the call handler is able to follow

## Postconditions 

  - **On success:**
    
      - the patient receives advice/treatment which is timely and the most appropriate for their needs

  - **Guaranteed:**

	- the patient receives advice/treatment which is safe
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
<td>Call handler searches for and finds the patient on their call handling system.</td>
</tr>
<tr class="odd">
<td>Step 2</td>
<td>Once the patient is identified the call handling system automatically starts the process to check for an end of life condition.</td>
</tr>
<tr class="even">
<td>Step 3</td>
<td>The call handling system identifies the patient's GP practice endpoint using PDS/SDS lookup.</td>
</tr>
<tr class="odd">
<td>Step 4</td>
<td>The call handling system requests to see any End of Life Problem/Conditions record for the patient from their registered GP practice.
<p>The API call includes a list of SNOMED CT codes to be looked for.</p></td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>Spine Security Proxy (SSP) checks organisation to organisation sharing agreement exists between requesting organisation (call centre) and the patient's register GP practice, and that the interaction (for example, Get Problem/Condition) is part of the sharing agreement.</td>
</tr>
<tr class="odd">
<td>Step 6</td>
<td>GP practice clinical system checks patient permissions and consent to share.</td>
</tr>
<tr class="even">
<td>Step 7</td>
<td>The call handling system receives the End of Life clinical codes that are found.
<p>The following information is returned with the following information:</p>
<ul>
<li><p>That there is an EOL clinical code that is active on this date.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td>Step 8</td>
<td>The call handling system will present the EOL information to the call hander and moves to the EOL workflow.</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>The EOL information and the switch to the EOL workflow is recorded on the call handling system for use in critical incident review/medico-legal investigation.</td>
</tr>
<tr class="odd">
<td>Step 3a</td>
<td>GP practice is not found on SDS.</td>
</tr>
<tr class="even">
<td>Step 3b</td>
<td>The call handling system follows the standard workflow.
<p>Note - the call handler is not presented with any error message as this would distract them from the task in hand.</p></td>
</tr>
<tr class="odd">
<td>Step 5a</td>
<td>SSP sharing agreement between 'to' organisation and 'from' organisation doesn't exist.</td>
</tr>
<tr class="even">
<td>Step 5b</td>
<td>The call handling system follows the standard workflow.</td>
</tr>
<tr class="odd">
<td>Step 6.1a</td>
<td>The patient is not found on the GP practice clinical system.</td>
</tr>
<tr class="even">
<td>Step 6.1b</td>
<td>The call handling system follows the standard workflow.</td>
</tr>
<tr class="odd">
<td>Step 6.2a</td>
<td>The patient has not consented to the sharing of medical data from the GP practice.</td>
</tr>
<tr class="even">
<td>Step 6.2b</td>
<td>The call handling system follows the standard workflow.</td>
</tr>
<tr class="odd">
<td>Step 7a</td>
<td>There is no Do Not Resuscitate (DNR) problem/condition recorded.</td>
</tr>
<tr class="even">
<td>Step 7b</td>
<td>The call handling system follows the standard workflow.</td>
</tr>
</tbody>
</table>

