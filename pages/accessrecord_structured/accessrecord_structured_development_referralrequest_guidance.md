---
title: Outbound Referrals guidance
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_referralrequest_guidance.html
summary: "FHIR&reg; resource ReferralRequest"
---

## What is an Outbound Referral?

An outbound referral is a request for transfer of care or request to provide assessment, treatment or clinical advice on the care of a patient from the registered GP Practice to a third party as recorded in the GP system against the referral feature / categorised area. 
Self referrals may also be included where they otherwise meet the above definition and are recorded in an equivalent manner to an outbound referral by the GP Practice. 

The referral is a record of the event of a referral being made or the intention to refer the patient, but it does not reflect the acceptance of the referral by the recipient or any onward progress of the referral unless detailed in the referral notes.

## The type of referral

GP Clinical Systems do not follow standard ways to classify referrals in terms of the reason for the referral and the type of service the referral is made to. 
There is limited commonality across GP Clinical Systems as to meta data associated with these elements of a referral.
The GP Clinical Systems support at least one READ / SNOMED CT coded field as the primary code for the referral, but this is not constrained to a specific valueset in all circumstances.
As a result, there is not a direct alignment between the main codes which have been recorded for referrals and the elements of the <code>ReferralRequest</code> resource.

The <code>reasonCode</code> has been selected as the most suitable element to be populated with the referral code for the GP Connect profile.

Consumers should be aware that there is a wide scope of codes supported and they will include a mixture of concepts across referral procedures, test requests, findings and so on.

Examples of types of referral
* Refer to physiotherapist
* Referral to musculoskeletal clinic
* Refer for ultrasound investigation
* Referral to community mental health team
* Refer for MRI
* Advice and guidance request sent
* Full blood count - FBC
* Abdominal pain

## Referrals via the NHS e-Referral Service

Referrals made via the NHS e-Referral Service (eRS) **MUST** be included by the provider where they are recorded in the GP Clinical System.
The Unique Booking Reference Number (UBRN) **MUST** be included as an <code>identifier</code> if it is captured against the referral record.
Consumers should be aware that referral details more limited for referrals via eRS or may be more likely to vary from the resulting referral.
Examples of limited details;
* <code>recipient</code> is not specified
* <code>reasonCode</code> is non-specific for example, 'Referral for futher care'

## Referral status

GP Clinical Systems support recording of a status for a referral or derive a status according the actions which have been undertaken for the referral.
However, the statuses are not standardised across GP Clinical Systems. 
It is also understood that the GP Practice may only be aware of a status change retrospectively and that the status of referrals are not routinely maintained in many GP Practices.

Providers **MUST** set the <code>status</code> of the referral as <code>unknown</code> for all referrals.

Consumers **MUST NOT** portray the referrals as indicating acceptance of the referral, current involvement by recipients or any other interpretation of the status of the referral.

Where details of the progress or outcome of the referral are captured in the GP Clinical System in a structured form they **SHOULD** be populated in the <code>note</code> element as appropriate key value pairs.

## Referral priority

This is the priority given by the GP Practice for the referral.
This may differ from the priority given to the referral by the recipient.

The <code>priority</code> is a restrited valueset and has been mapped to the eRS priority codes. 
The source GP Clinical System may support priority values other than the eRS priority codes.
If the priority in the source system is not one of the eRS priority codes and cannot be mapped to an eRS priority code, then a <code>priority</code> **MUST NOT** be included and the source system priority **MUST** be included as a key value pair in the <code>note</code> element.

## Date of referral

All GP Clinical Systems have a user selection date field against a referral.
Providers **MUST** populate the <code>authoredOn</code> element with the user entered referral date.

Consumers should be aware that the date may have slightly different meaning according to the GP Clinical System and local practice for recording referrals.

## Using the <code>List</code> resource for referral queries

The result of a query for referral details **MUST** return a <code>List</code> containing references to all <code>ReferralRequest</code> resources that are returned.

The <code>List</code> **MUST** be populated in line with the guidance on <code>List</code> resources.

If the <code>List</code> is empty, then an empty <code>List</code> **MUST** be returned with an <code>emptyReason</code> with the value <code>noContent</code>.
