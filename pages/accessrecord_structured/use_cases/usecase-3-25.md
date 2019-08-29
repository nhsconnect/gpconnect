---
title: Parental consent differs for immunisation
keywords: usecase, structured
tags: [usecase, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_usecase_3.25.html
summary: "Use case for parental consent differs for immunisation"
---

## Brief description

A child, Sue, is brought to a vaccination appointment by her father Bill. Bill is registered at the practice, but Sue is registered elsewhere. Sue is registered at the same practice as her mother Lucy (Bill and Lucy are separated). Bill explains that Sue is living with him for the time being and that he has agreed with Lucy to bring Sue to his practice. Bill explains that this is a temporary arrangement whilst Lucy recovers from recent surgery and so does not want to change Sue's registered practice.

Joel (practice nurse) calls up the medical records for Sue. Joel needs to check the immunisation history to ensure that the vaccination has not previously been administered and that there are no other indicators that the vaccination is not applicable for Sue.

Lucy/Sue's registered practice is local to Joel/Bill's practice and they have a data sharing agreement and can access each other's records via GP Connect.

Lucy has previously refused this vaccination for Sue, but Bill has not declared this \[1\].

## Use case justification

Clinical and administration:

  - access to accurate information at the point of care reducing the opportunity for errors to occur
  - reduction in clinical time wasted, away from the patient, collecting and collating information

Patient-focused:

  - increased patient safety due to the reduction in manual transcription errors
  - better patient experience as they are not being asked for information which should already be available to the practice nurse

## Primary actors

  - practice nurse
  - GP Connect
  - GP clinical systems

## Secondary actors

  - patient
  - patient's parents or guardians

## Triggers

  - child and parent attend appointment for a vaccination or attend a vaccination clinic

## Preconditions

  - the patient's details have been verified and entered on the GP clinical system
  - the practice nurse has the correct/appropriate system access rights
  - the patient's GP has agreed to share patient information via GP Connect
  - the patient's parent consents to this shared information being viewed/used
  - electronic interactions between GP clinical system/GP Connect/GP clinical system have been correctly configured

## Postconditions

  - **On success:**
    
      - the parent's wishes are fully adhered to and the vaccination is given or withheld appropriately

  - **Guaranteed:**
    
      - the child is appropriately assessed for the vaccination and the vaccination is given or withheld appropriately based on available medical history

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
<td>Sue and Bill attend the practice</td>
</tr>
<tr class="even">
<td>Step 2</td>
<td>Joel requests access to Sue's GP record via GP Connect</td>
</tr>
<tr class="odd">
<td>Step 3</td>
<td>Joel calls back information from GP Connect relating to
<ul>
<li><p>Allergies</p></li>
<li><p>Vaccinations</p></li>
<li><p>Conditions/Problems</p></li>
<li><p>Observations</p></li>
</ul></td>
</tr>
<tr class="even">
<td>Step 4</td>
<td>Joel searches for the specific vaccine to be administered and verifies that Sue has not already received the vaccination</td>
</tr>
<tr class="odd">
<td>Step 5</td>
<td>Joel notices within Sue's record a recent refusal for the vaccination to be administered</td>
</tr>
<tr class="even">
<td>Step 6</td>
<td>Joel looks for additional narrative to understand the reason for the Refusal
<p>Joel calls back information from GP Connect relating to</p>
<ul>
<li><p>Consultations/Encounters</p></li>
</ul>
<p>and finds details which explain that Lucy has refused the vaccination and disagrees with Bill over this</p></td>
</tr>
<tr class="odd">
<td>Step 7</td>
<td>Joel looks for any additional information related to this and finds a recent consultation which notes that Lucy had a further conversation with her GP about the vaccination and was giving the matter further consideration</td>
</tr>
<tr class="even">
<td>Step 8</td>
<td>Bill says that Lucy is now in agreement for the vaccine to be given, but there is no information on Sue's record to verify this</td>
</tr>
<tr class="odd">
<td>Step 9</td>
<td>Joel decides to contact Lucy to verify whether she now consents</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td>Joel speaks to Lucy who confirms that she has considered the additional information from the GP and discussed with Bill and Sue and now consents to the vaccination</td>
</tr>
<tr class="odd">
<td>Step 11</td>
<td>Joel records the consent and, having also checked that there is no allergy or other adverse information, administers the vaccination</td>
</tr>
<tr class="even">
<td colspan="2"><strong>Alternative Path - Refusal Upheld</strong></td>
</tr>
<tr class="odd">
<td>Steps 1 - 9</td>
<td>As main flow above</td>
</tr>
<tr class="even">
<td>Step 10</td>
<td>Joel speaks to Lucy who says there has been some confusion and that she is still considering the additional information from the GP and is not yet able to withdraw the refusal</td>
</tr>
<tr class="odd">
<td>Step 11</td>
<td>Joel informs Bill that he cannot administer the vaccine and records the details of the discussions</td>
</tr>
<tr class="even">
<td colspan="2"><strong>Alternative Path - Refusal Information is not shared</strong></td>
</tr>
<tr class="odd">
<td>Steps 1 - 4</td>
<td>As the main flow above</td>
</tr>
<tr class="even">
<td>Step 5</td>
<td>Joel discusses the possible side effects of the vaccination with Bill who acknowledges these and gives his consent for the vaccination to be administered. Joel finds no record of Lucy's objection and so is unaware of it.</td>
</tr>
<tr class="odd">
<td>Step 6</td>
<td>Joel records the consent and, having also checked that there is no allergy or other adverse information, administers the vaccination.</td>
</tr>
<tr class="even">
<td><p>Some time</p>
<p>later…</p></td>
<td>Lucy calls the practice and complains that the vaccination was given against her wishes (which were recorded on Sue's main record but were not shared via GP Connect).</td>
</tr>
</tbody>
</table>

1.  “Although the consent of one person with parental responsibility for a child is usually sufficient (see Section 2(7) of the Children Act 1989), if one parent agrees to immunisation but the other disagrees, the immunisation should not be carried out unless both parents can agree to immunisation or there is a specific court approval that the immunisation is in the best interests of the child.” Source: [Green Book Chapter 2](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/144250/Green-Book-Chapter-2-Consent-PDF-77K.pdf)
