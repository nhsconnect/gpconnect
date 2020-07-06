---
title: ReferralRequest resource
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_referralrequest.html
summary: "FHIR resource for population guidance for ReferralRequest"
div: resource-page
---
## Introduction

The headings below list the elements of the ReferralRequest resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available in the [elements not in use section](accessrecord_structured_development_referralrequest.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [ReferralRequest profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1)." %}

## ReferralRequest elements

### id

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Id</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The logical identifier of the ReferralRequest resource.

### meta.profile

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>uri</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The ReferralRequest profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1)

### identifier

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Identifier</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

If the referral was made via the e-Referral Service and a Unique Booking Reference Number (UBRN) exists for the referral, then it **MUST** be included as an identifier.
The system identifier for this is `https://fhir.nhs.uk/Id/ubr-number`.

### basedOn

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(CarePlan, ProcedureRequest, ReferralRequest)</code></td>
    <td><strong>Optionality:</strong> Optional</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

Indicates any plans or prior referrals that this referral is intended to fulfill.

### status

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Code</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Fixed value of <code>unknown</code>.
Referrals 'entered in error' must not be included.

### intent

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Code</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Fixed value of <code>order</code>.

### priority

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Code</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

A mapping is applied to the priority codes to align it to the e-Referral Service priority types.
This **MUST** be populated where the source system has a referral priority which matches the e-Referral Service priority codes or can be mapped to those priority codes.
If there is a priority code for the referral but it is incompatible with the e-Referral Service priorities, this element **MUST** be excluded and the priority **MUST** be supplied in the <code>note</code> element.

### serviceRequested

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Optional</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

This **MUST NOT** be populated with the source system's main code for the referral, which **MUST** be returned in the <code>reasonCode</code> element.
This **MAY** be populated if the GP clinical system also holds a distinct entry for the type of service requested.

### subject

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Patient)</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

A reference to the patient who is the subject of the referral.

### context

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Encounter)</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The `Consultation` within which the referral was recorded.

### authoredOn

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>dateTime</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The main date for the referral as entered by the end user in accordance with the [date of referral guidance](accessrecord_structured_development_referralrequest_guidance.html#date-of-referral).

### requester

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>BackboneElement</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The details of the person, practitioner or organisation responsible for the decision to refer the patient or, if is not attributed specifically, then populate with the recorder.

### requester.agent

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Device, Organization, Patient, RelatedPerson, Practitioner)</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The preferred agent is the practitioner responsible for the decision to refer the patient.
If the referral is not attributed to a practitioner, then any of the other resource options **MAY** be used as most appropriate.
If the referral does not clearly identify responsibility for the referral decision or action, this **MUST** be the user who recorded the referral.

### requester.onBehalfOf

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Organization)</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

This **MUST** be populated if the <code>requester.agent</code> is a practitioner and the <code>Organization</code> associated with the referenced <code>Practitioner</code> is not the GP practice responsible for the referral.
This element **SHOULD** be absent if the <code>requester.agent</code> is not a practitioner.

### specialty

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Optional</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

This **MUST NOT** be populated with the source system's main code for the referral, which **MUST** be returned in the <code>reasonCode</code> element.
This **MAY** be populated if the GP clinical system holds a distinct entry for the clinical or practitioner specialty requested by the referral.

### recipient

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(HealthcareService, Organization, Practitioner)</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

This **MUST** be populated with the practitioner and/or organisation the patient has been referred to, if that is recorded in a suitable coded format.
If the referral recipient details are in a form which cannot be returned as a referenced resource, the details **MUST** be populated to the <code>note</code> as key value pairs.

### reasonCode

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> CodeableConcept</td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

This **MUST** be populated with the source system's main coded entry for the referral.
Additional, coded or text entries which are clearly captured as reasons for referral **MAY** be included.

### description

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>string</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The free text description associated with the referral.

### supportingInfo

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Any)</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

Reference to the referral letter(s) and any other supporting documents or resources which are not covered by other more specific elements, for instance this could include reference to linked observations or test results.

This does not apply to a linked problem.
The problem **MUST** be included in the bundle and reference to the <code>referralRequest</code>.
The <code>referralRequest</code> **MUST NOT** reference to the problem.

### note

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Annotation</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

Any additional information recorded against the referral which is not accommodated by other elements.
This could include additional categorisation of the referral or notes recorded against the referral after it has been made such as details of progress or outcomes.


<h2 style="color:#ED1951;"> Elements <strong>not in use</strong> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> definition </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(ActivityDefinition, PlanDefinition)</code></td>
  </tr>
</table>

This is not required by GP Connect.

<h3 style="color:#ED1951;"> replaces </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(ReferralRequest)</code></td>
  </tr>
</table>

Terminated referrals are not in scope so cannot be referenced.
Any association to a prior, completed referral can be made via the basedOn element.

<h3 style="color:#ED1951;"> groupIdentifier </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Identifier</code></td>
  </tr>
</table>

This is not required by GP Connect.

<h3 style="color:#ED1951;"> type </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
  </tr>
</table>

This element has not been defined for GP Connect use.
The <code>reasonCode</code> element **MUST** be used for the SNOMED CT coded referral code.

<h3 style="color:#ED1951;"> occurrence </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>dateTime, Period</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> reasonReference </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(ProblemHeader-Condition)</code></td>
  </tr>
</table>

A referral may have a linked problem which represents the reason for the referral.
This is required information where it exists, but the problem **MUST** be included and reference to the <code>referralRequest</code>.
The <code>referralRequest</code> **MUST NOT** reference to the problem.

<h3 style="color:#ED1951;"> relevantHistory </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Provenance)</code></td>
  </tr>
</table>

<br>
