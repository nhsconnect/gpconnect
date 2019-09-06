---
title: Health visitor's appointment during pregnancy (antenatal)
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.41.html
summary: "Use case for health visitor's appointment during pregnancy (antenatal)"
---

## Brief description 

Before the first appointment for a health visitor referral the health visitor needs to collect all information about the patient in order to provide the best possible care during pregnancy. The health visitor seeing the patient will have full access to the patient’s GP record ensuring that the patient receives the best possible standard of care.

## Use case justification 

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur

  - reduction in clinical time wasted, away from the patient, collecting and collating information

  - reduction in clinical time wasted, away from the patient, manually updating IT systems

  - reducing the paper flow through departments/organisations by utilising the systems workflow to manage tasks using staff time efficiently

Patient-focused:

  - security of patient information is maintained and improved through the reduction of paper-based “Patient Identifiable Documents” in use within departments

  - increased patient/clinician time due to reduction in clinician time spent collecting and transcribing information away from the patient

  - increased patient safety due to the reduction in manual transcription errors

  - better patient experience as they are not being asked for information which should already be available to the clinician

## Primary actors 

- health visitor
- community system
- GP Connect
- GP clinical system

## Secondary actors 

- patient

## Triggers 

- patient is referred to the community health visitor after confirmation of pregnancy

## Preconditions 

  - the patient’s details have been verified and entered on the community system
  - health visitors have the correct/appropriate system access rights
  - the patient’s GP has agreed to share patient information via GP Connect
  - the patient allows this shared information to be viewed/used by GP staff
  - electronic interactions between community system/GP Connect/GP clinical system have been correctly configured

## Postconditions 

  - **On success:**

  - **Guaranteed:**
    
      - all the relevant available information on the patient’s medical history has been viewable on the community system used by health visitors

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
<td>Patient is referred to the community services due to pregnancy.</td>
</tr>
<tr class="odd">
<td>Step 2</td>
<td>Patient attends appointment with health visitor at 20 weeks.</td>
</tr>
<tr class="even">
<td>Step 3</td>
<td>The health visitor logs into their usual community system.</td>
</tr>
<tr class="odd">
<td>Step 4</td>
<td>Health Visitor searches for patient via NHS Number.</td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>The community system will request the patient’s relevant sections of the patient’s record that are held in the patient's registered GP practice system via the GP Connect service.</td>
</tr>
<tr class="odd">
<td>Step 6</td>
<td>GP Connect and the GP practice system will check that the community organisation is allowed access to the data and that the patient has not objected to their data being shared.</td>
</tr>
<tr class="even">
<td>Step 7</td>
<td><p>GP clinical system provides all relevant requested sections.</p>
<ul>
<li><p>Mental health issues</p></li>
<li><p>Alerts (warnings) – certain conditions, safeguarding, domestic abuse</p></li>
<li><p>Diagnosis</p></li>
<li><p>Problems</p></li>
</ul>
<p>Mother only</p>
<ul>
<li><p>Informed when woman is pregnant.</p>
<ul>
<li><p>Confirmation that the woman is pregnant.</p></li>
<li><p>Many women may visit GP rather than community when find out they are pregnant, not always easy to get this information.</p></li>
</ul></li>
</ul>
<ul>
<li><p>Instances of miscarriage</p>
<ul>
<li><p>This is useful for antenatal as plan their first visit at 22 weeks.</p></li>
<li><p>Not a good experience for patient if health visitor arrives not knowing the woman has had a miscarriage.</p></li>
<li><p>Currently they need to ring the GP to check these before appointments.</p></li>
</ul></li>
</ul></td>
</tr>
<tr class="odd">
<td>Step 8</td>
<td>The community system imports all information supplied from the GP practice. This data is now available for clinicians to review and maintain.</td>
</tr>
<tr class="even">
<td>Step 9</td>
<td>The medical data retrieved by the health visitors from other sources is manually added to the community system.</td>
</tr>
<tr class="odd">
<td><strong>Alternative Path</strong></td>
<td></td>
</tr>
<tr class="even">
<td>Step 6a</td>
<td><p>Where there are not the appropriate permissions to share the data, GP connect returns an error message saying the information cannot be returned.</p>
<p>The pharmacy technician will retrieve the information using the SCR, Leeds Care Record and direct requests to the GP practice. They will then manually enter the data.</p></td>
</tr>
</tbody>
</table>
