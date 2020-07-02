---
title: Clinical summary
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.34.html
summary: "Use case for clinical summary"
---

## Brief description

A professional user of the Local Care Record ('Care professional') needs to review a patient's GP practice information:

  - clinical summary of the patient

A patient is admitted to hospital and the clinician responsible for the care of that patient in the hospital needs to review their care history in a clinical summary from the GP practice clinical system, to assist in determining the appropriate care provision and support. They have access to the Local Care Record (LCR), which shares clinical information relevant to the direct care of their patient from a variety of local hospital, community and GP organisations.

## Use case justification

Currently, when a patient's record is viewed in the LCR, their current clinical summary from the GP practice clinical system are presented as a static HTML view from a third-party supplier, which is rigid and not in keeping with the needs of professionals, the design of the system's user interface (UI), nor is it the preferred strategy for sharing of patient information within the LCR landscape. Electronically consuming the FHIR-compliant profiles for a patient to form a new summary from their GP practice clinical system will allow the LCR to:

  - share this data in a manner which is congruent and consistent with all other care partners
  - present the data in a manner which is appropriate for the care setting
  - share more relevant data, pertinent to the role of the professional involved and improve care delivery
  - present the data in a uniform and streamlined interface
  - provide a higher quality user experience
  - provide a higher fidelity audit record

In addition, it will be possible to potentially extend the Clinical Summary in the future with finer-grained information based on business need, in a simple and effective manner.

The system will be able to harness multiple FHIR objects in order to form a more accurate and concise depiction of the patient's Clinical Summary.

## Primary actors

- care professionals
- clinicians
- LCR subsystem

## Secondary actors

- patient

## Triggers

- at the point of direct care, during a consultation or care delivery setting, the professional/clinician is discussing the medical history with their patient.

## Preconditions

  - patient has been admitted onto the hospital's Patient Administration System (PAS) and has gone through identification including retrieving their NHS Number
  - the clinician has been advised by the local hospital's system that their patient has information available within the LCR
  - the clinician is logged into, and has a valid session with, the LCR
  - the clinician has relevant access and permission to view the patient's details in the LCR
  - the patient has been registered within the GP practice clinical system and has data available for sharing with other clinical systems. Note: if no such data is available, it will not be possible to initiate the basic flow
  - the GP practice clinical system exists within the Spine Security Proxy (SSP)

## Postconditions

  - **On success:**
    
      - the patient's Clinical Summary is taken from the GP practice clinical system and presented in the LCR

  - **Guaranteed:**
    
      - access and data returned is recorded for auditing purposes

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
<td>Clinician requests the 'Clinical Summary' for the patient using the LCR interface.</td>
</tr>
<tr class="odd">
<td>Step 2</td>
<td>The LCR identifies the patient's GP practice end point using PDS/SDS lookup.</td>
</tr>
<tr class="even">
<td>Step 3</td>
<td>The LCR requests the patient's 'Clinical Summary' from their registered GP practice.</td>
</tr>
<tr class="odd">
<td>Step 4</td>
<td>Spine Security Proxy (SSP) checks organisation to organisation sharing agreement exists between requesting organisation (LCR) and the patient's registered GP practice, and that the interactions required to build the Summary (for example, Get Problems, Get Allergies, etc.) are part of the sharing agreement.</td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>GP practice clinical system checks patient permissions and consent to share.</td>
</tr>
<tr class="odd">
<td>Step 6</td>
<td>The LCR receives the 'Clinical Summary' via the GP Connect service and presents the results to the clinician within the LCR user interface (UI).
<p>The following information is returned and presented in the LCR UI, as a minimum, for the Clinical Summary:</p>
<ul>
<li><p>Details of Current Problems</p></li>
<li><p>Current Medication</p></li>
<li><p>Allergies and Adverse Reactions (Risks &amp; Warnings)</p></li>
<li><p>Recent Test Results</p></li>
</ul>
<p>Additional information can be included depending on business need.</p></td>
</tr>
<tr class="even">
<td>Step 7</td>
<td>The clinician then reviews the information presented and determines the best course of action in response to the information. This may involve requesting additional data sets from GP Connect to supplement the data already presented within this list.</td>
</tr>
<tr class="odd">
<td><strong>Exceptions</strong></td>
<td></td>
</tr>
<tr class="even">
<td>Step 4a</td>
<td>SSP sharing agreement between 'to' organisation and 'from' organisation doesn't exist.</td>
</tr>
<tr class="odd">
<td>Step 4b</td>
<td>Exception is reported in LCR user interface; user is directed to contact local service desk for resolution.</td>
</tr>
<tr class="even">
<td>Step 5a</td>
<td>The patient has not consented to the sharing of medical data from the GP practice.</td>
</tr>
<tr class="odd">
<td>Step 5b</td>
<td>Exception is reported in the LCR user interface.</td>
</tr>
<tr class="even">
<td>Step 6a</td>
<td>A logic or integration exception occurs in the retrieval of data.</td>
</tr>
<tr class="odd">
<td>Step 6b</td>
<td>Exception is reported in the LCR user interface and is logged within the LCR's exception tracing database; user is directed to contact local service desk for resolution.</td>
</tr>
</tbody>
</table>

