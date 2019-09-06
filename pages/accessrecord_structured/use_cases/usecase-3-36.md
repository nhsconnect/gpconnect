---
title: Referral to social prescribing
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.36.html
summary: "Use case for referral to social prescribing"
---

## Brief description

Social prescribing is a means of enabling GPs and other frontline healthcare professionals to refer people to 'services' in their community instead of offering only medicalised solutions. Often the first point of referral is a link worker or 'community connector' who can talk to each person about the things that matter to them. Together they can co-produce a social prescription that will help to improve their health and wellbeing.

The community activities range from art classes to singing groups, from walking clubs to gardening, and to many other interest groups. It is taking off across the country, particularly with people who are lonely or isolated; people with mild mental health issues (including dementia) who may be anxious or depressed; and, those who struggle to engage effectively with services. Very often these people have frequent repeat visits to their doctor or to their local emergency department - effectively trapping them in a 'revolving door' of services.

## Use case justification

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur
  - reduction in clinical time wasted, away from the patient, collecting and collating information
  - reduction in clinical time wasted, away from the patient, manually updating IT systems

Patient-focused:

  - increased patient safety due to the reduction in manual transcription errors
  - better patient experience as there is less likely to be a delay in referral
  - optimise the sign-posting of patients to the most appropriate endpoint taking into consideration patient-specific healthcare history and current concerns
  - better patient experience as they are not being asked for information which should already be available to the GP

## Primary actors

  - GP
  - social prescribing link worker
  - GP Connect
  - social prescribing IT system
  - GP clinical systems

## Secondary actors

  - patient
  - patient's carer (if applicable)

## Triggers

  - the GP recognises that the patient has unmet, non-clinical needs which are adversely impacting a long-term condition which can be addressed by social prescribing and a social prescribing service is available in the GP area

## Preconditions

  - the patient has been referred to a social prescribing service from their GP/primary care service
  - the patient's details have been verified and entered on the social prescribing IT system
  - the link worker has the correct/appropriate system access rights
  - the patient's GP (practice/federation) has agreed to share patient information via gp connect with the social prescribing service
  - the patient or patient's carer consents to this shared information being viewed/used
  - electronic interactions between GP clinical system/GP Connect/social prescribing IT system have been correctly configured

## Postconditions

  - **On success:**
    
      - the information provided by GP Connect is used to inform the link worker of all the background to the referral of the known social needs and the relevant medical conditions being managed such that the link worker can identify the optimum voluntary care sector (VCS) services to provide maximum benefit to the patient's health and well-being

  - **Guaranteed:**
    
      - the patient is appropriately assessed according to the information available from the referral letter, the patient (and carer if applicable) and further consultation and investigation as required

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
<td>The patient is referred to the social prescribing service by the GP and a patient record is created on the social prescribing system.</td>
</tr>
<tr class="even">
<td>Step 2</td>
<td>The Social Prescribing Link Worker accesses the patient record in the social prescribing system.</td>
</tr>
<tr class="odd">
<td>Step 3</td>
<td>The Social Prescribing Link Worker accesses GP Connect to retrieve the medical and other history from the patient's registered GP system.</td>
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
<li><p>Consultations (encounters) - could be time limited - for example, last x months of consultations</p>
<ul>
<li><p>Date of consultation</p></li>
<li><p>Title for consultation (to help identify consultations relevant to social needs to avoid reading more medical history than necessary).</p></li>
<li><p>Clinician</p></li>
<li><p>Details</p></li>
</ul></li>
<li><p>Medications (may only need certain types of medication such as anti-depressants, anti-psychotics, methadone).</p></li>
<li><p>Demographic data/contact details</p></li>
<li><p>Social history/employment details</p>
<ul>
<li><p>Date</p></li>
<li><p>Significant event effecting health or well-being (for example, family bereavement, loss of employment).</p></li>
</ul></li>
<li><p>Referrals/Agencies Involved (especially certain agencies such as IAPs).</p>
<ul>
<li><p>Date</p></li>
<li><p>Agency/Referred To</p></li>
<li><p>Purpose</p></li>
<li><p>Status (open/closed)</p></li>
</ul></li>
<li><p>Problems/long-term conditions</p></li>
<li><p>Drug/Alcohol Use</p></li>
<li><p>Current Care Plans</p>
<ul>
<li><p>What services are being provided</p></li>
<li><p>When are or were the services provided</p></li>
<li><p>Who are the services provided by</p></li>
<li><p>What is the intended outcome of the service</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>GP Connect presents the GP patient record to the social prescribing system.</td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>The social prescribing system presents the relevant parts of the GP record to the link worker.</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>The link worker navigates from the known problems to any linked consultation details or linked causes or scans for relevant record entries along a timeline of presenting problems. The link worker reviews relevant social context for the patient and employs keyword searches to find additional background details across the record based on the initial findings.</td>
</tr>
<tr class="odd">
<td>Step 9</td>
<td>The link worker uses the information gathered to check the directory of services for any potential VCS services to support the patient.</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td>The link worker makes relevant notes to facilitate an efficient and effective consultation with the patient.</td>
</tr>
<tr class="odd">
<td colspan="2"><strong>Alternative Path - Patient Record not shared</strong>.</td>
</tr>
<tr class="even">
<td>Steps 1 - 2</td>
<td>As above</td>
</tr>
<tr class="odd">
<td>Steps 3 - 8</td>
<td>Do not occur or fail</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>The link worker consults with the patient to gather information and then seeks to identify appropriate services.</td>
</tr>
<tr class="odd">
<td>Step 10</td>
<td>As required, the link worker contacts the referring GP to verify or complete information provided by the patient or to try to gather any additional information which may be relevant to recommending services.</td>
</tr>
</tbody>
</table>
