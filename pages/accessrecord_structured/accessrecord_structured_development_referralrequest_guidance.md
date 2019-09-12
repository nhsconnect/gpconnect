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

A referral may be considered as a detailed document containing relevant medical history, presenting needs, problem management to date, current medications and allergies, etc. 
This profile does not contain such clinical background for the patient being referred, although details may be referenced from the resource, for example reference to a referral letter.

The referral is a record of the event of a referral being made or the intention to refer the patient. 
It does not reflect the acceptance of the referral by the recipient or any onward progress of the referral unless described in the referral notes.

## Referral classification

GP Clincial Systems have taken a variety of approaches to the classification of referrals.
The FHIR <code>ReferralRequest</code> has multiple elements to support the classification of referrals.
Requirements analysis and PRSB documentation identifies a demand for a clear classification structure to the referral details.
PRSB cites a high-level classification of a referral to a service and reason for referral.

The referred to service has further classification of department, specialty, subspecialty, educational institution, mental health, etc.
The reason for referral includes diagnosis, treatment, transfer of care due to relocation, investigation, second opinion, management of the patient (e.g. palliative care), provide referrer with advice / guidance.

Analysis was undertaken as to whether the data in GP Clinical Systems, SNOMED CT terminology and FHIR resources could be aligned to achieve a reliable and meaningful classification structure in line with PRSB defintions.

### GP Clinical Systems

There is limited commonality across GP Clinical Systems as to the meta data associated with their referral classification.

All GP Clinical Systems support at least one READ / SNOMED CT coded field as the main code for the referral. 
This may be constrained to a referral procedure code hierachy (descendants of <code>3457005 | Patient referral (procedure) |</code>) or open to a wide selection of codes covering at least clinical findings and procedures.
GP Clinical Systems that constrain to the referral procedure codes (for a new referral entry) may contain other codes due to GP2GP transfers or legacy data.
The main referral code can therefore be either a reason for referral or referred to service.

Analysis of a large referral recordset across two GP Systems providers identified the following common examples for the main coded classification of the referral:
* Refer to physiotherapist
* Referral to musculoskeletal clinic
* Refer for ultrasound investigation
* Referral to community mental health team
* Refer for MRI
* Advice and guidance request sent
* Full blood count - FBC
* Abdominal pain

The GP System may have additional non-READ / SNOMED CT coded classification fields with fixed or locally configured valuesets.
These are often optional fields. 
These fields may have valuesets which span reason for referral and referred to service.

All GP Clinical Systems also support links between the referral and:
* problems
* referral letters or other attached documents

### FHIR Referral Classification Elements

The <code>ReferralRequest</code> resource has several elements covering the classification of the referral:
* <code>type</code>
* <code>serviceRequested</code>
* <code>specialty</code>
* <code>reasonCode</code>
* <code>reasonReference</code>

None of the above elements are mandatory.
<code>serviceRequested</code>, <code>specialty</code> and <code>reasonCode</code> are fairly distinct, but <code>type</code> appears to have significant overlap with all those elements. 

The scope of the main referral code across GP Clinical Systems spans these <code>ReferralRequest</code> elements, that is there is not a strong alignment to any single element.

### Referrals and SNOMED CT

The SNOMED CT 'is a' hierachy <code>3457005 | Patient referral (procedure) |</code>) was considered as a potential valueset for referrals.
However, it includes pre-coordinated referral concepts of various patterns which span all the classification elements listed above:
* Referral to institution (for example, hospital)
* Referral to speciality (for example, department)
* Referral to specialist (for example, professional)
* Referral to administrative service (for example, diabetic register)
* Referral for procedures
* Referral for findings / disorders
* Referral statuses (for example, referral accepted by, referral cancelled by, etc.)

SNOMED content in this area will not support retrieval bahaviour, for example
* <code>183523005 | Referral to gastroenterology service (procedure) |</code> and <code>306308009 | Referral to gastrointestinal surgeon (procedure) |</code> are unrelated
* <code>892201000000106 | Fast track referral for suspected lower gastrointestinal cancer</code> and <code>276401000000108 | Fast track referral for suspected colorectal cancer (procedure) |</code> are siblings rather than the former subsuming the latter

The terminology in its current form is therefore unlikely to support the structured classification (as it crosses over such classification) and is not suited to structured retrieval queries. 

### Design Design for Classification

The analysis provided no clear structure to apply to classification of referrals which the current data in GP Clinical Systems can support.
The referrals SNOMED terminology does not lend itself to give benefit to a structured classification.
The main coded classification of a referral in GP Clinical Systems does not clearly align to any element of the <code>referralRequest</code>.
 
It does not seem practical to enforce a structure to the existing data for referral classification.
The <code>reasonCode</code> has been selected for populating with the main coding of the referral because it:
* is a codeableConcept
* supports multiple values
* is more suited to a wide valueset than alternative elements

Providers **MUST** therefore return their main READ / SNOMED CT code for the referral in the <code>reasonCode</code>.
Providers **MUST** return all other referral classification coding, but **MAY** populate the <code>serviceRequested</code>, <code>specialty</code>. <code>reasonCode</code> and / or <code>note</code> element(s) as appropriate to the nature of its data.

## Referrals via the NHS e-Referral Service

Referrals made via the NHS e-Referral Service (eRS) **MUST** be included by the provider where they are recorded in the GP Clinical System.
The Unique Booking Reference Number (UBRN) **MUST** be included as an <code>identifier</code> if it is captured against the referral record.
Consumers should be aware that referral details may be limited for referrals via eRS or may be more likely to vary from the resulting referral.
Examples of limited details;
* <code>recipient</code> is not specified
* <code>reasonCode</code> is non-specific for example, 'Referral for futher care'

## Referrer Details

The provider **MUST** populate the <code>requester</code> with the practitioner who recorded the referral, if available.
This may be a clinician or a member of the administrative staff.
The role, organisation and contact details for the referrer **MUST** be included with the bundled resource as available.

If the organisation referenced from the bundled <code>practitioner</code> resource is not the GP Practice responsible for the referral, then the <code>onBehalfOf</code> element **SHOULD** reference to an <code>organization</code> resource for the GP Practice responsible for the referral.

## Referral status

GP Clinical Systems support recording of a status for a referral or derive a status according the actions which have been undertaken for the referral.
However, the statuses are not standardised across GP Clinical Systems. 
It is also understood that the GP Practice may only be aware of a status change retrospectively and that the status of referrals are not routinely maintained in many GP Practices.

Providers **MUST** set the <code>status</code> of the referral as <code>unknown</code> for all referrals.

Consumers **MUST NOT** portray the referrals as indicating current involvement by recipients or any other interpretation of the status of the referral.

Where details of the progress or outcome of the referral are captured in the GP Clinical System in a structured form they **SHOULD** be populated in the <code>note</code> element as appropriate key value pairs.

## Referral priority

This is the priority given by the GP Practice for the referral.
This may differ from the priority given to the referral by the recipient.

The <code>priority</code> is a restricted valueset and has been mapped to the eRS priority codes. 
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
