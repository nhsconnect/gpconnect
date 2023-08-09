---
title: MedicationStatement
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medicationstatement.html
summary: "Guidance for populating and consuming the MedicationStatement profile"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `MedicationStatement` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [MedicationStatement profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1/_history/1.7)." %}

## MedicationStatement elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the `MedicationStatement` profile.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The MedicationStatement profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1)

### extension[lastIssueDate] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The date when the latest prescription under this plan was issued. This will not be populated where the Medication/Medical Device is Repeat Dispensed or Prescribed Elsewhere as these do not have issue information recorded in the GP system.

### extension[prescribingAgency] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

This details the care setting in which the medication or medical device was prescribed.

Currently this field will only support two coded entries, indicating whether the medication/medical device was prescribed by the GP practice or by another organisation. If the providing organisation has more details about the type of prescribing organisation (for example, that it was a dental practice or hospital), this **MUST** be included in the CodeableConcept.Text field.

In the future, the coded valueset will be built on to be more specific about where a medication/medical device was prescribed. For instance, if the patient was prescribed a medication by a hospital or bought a medication over the counter then this would be coded as well as in the text.

For repeat and repeat dispensed medications/medical devices, the value identifies the care setting where the medication plan (rather than any specific issue in the plan) was authorised.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Link to the MedicationRequest that this `MedicationStatement` is based on.

Every MedicationStatement **MUST** be based on a `MedicationRequest` with `intent` set to `plan`.

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The `Encounter` within which the medication/medical device was authorised.

As per base profile guidance.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The status of the authorisation.

Use one of `active`, `completed` or `stopped`:

- `active` represents an active authorisation - used for active repeat medications/medical devices
- `stopped` represents an authorisation which has been discontinued, cancelled or stopped
- `completed` represents an authorisation which has run its course

For repeat and repeat dispensed the status refers to the status of the plan (the entire cycle of prescriptions).

For acute, the status refers to the status of the prescription issue.

### medicationReference ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Medication)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The medication/medical device the authorisation is for.

The `Medication` profile provides the coded representation of the medication/medical device.

### effective ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Period</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The period the medication or medical device is authorised under this medication/medical device plan.
For items that are repeats and repeat dispensed this refers to the entire cycle of prescriptions made under the authorisation.
For acutes, this refers to the period of the prescription issue.

`Period.start` is **MANDATORY**.

The date from which the medication or medical device is authorised under this plan.

Use one of the following dates in order of descending preference:

- the authorised date as recorded in the patient record
  - for authorisation that were performed during a consultation this will be the date when the consultation took place
- the date of the first issue under the medication/medical device plan
- the date the medication/medical device plan was recorded onto the system (the audit date)

`Period.end` is **REQUIRED**.

The date when the authorisation under this plan ends.

Where the medication/medical device plan status is active, set to null.

Where the medication/medical device plan has ended use one of the following dates in order of descending preference:

- the end date recorded in the patient record
- the end date of the final issue under the medication/medical device plan. This is the start date of the final issue plus the expected supply duration.
- the date the plan was updated to ended
- the Period.start date
  - this option should only occur where data has been lost (for example, during the record transfer between two systems) and is used to ensure that an ended plan will always have an end date

### dateAsserted ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

When this medication statement was believed true.

Unless there is a distinct user-modifiable availability date/time for the authorisation, this is the audit trail date/time for when the authorisation was entered.

### informationSource ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient | Practitioner | RelatedPerson | Organization)  </code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Person or organization that provided the information about the taking of this medication

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Who the medication/medical device is for - that is, to whom it will be administered.

Reference to patient.

### taken ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Whether a medication/medical device was taken.

Providers **MUST** use a default value of `unk` – unknown.

This item is mandatory in the base FHIR profile, but GP systems do not record this detail. Therefore, we have been forced to pick a default value and this information should not be used.

This element has been included in this section as providers **MUST** populate it. However, as the data should not be used it has also been included in the ‘Do not use’ section below.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

All notes that are associated with this medication/medical device record.

All patient notes and prescriber notes at authorisation(plan) and issue(order) level **MUST** be included in this field. They **MUST** be concatenated and indicate the level the notes come from (for example, 1st Issue) and be prefixed with either ‘Patient Notes:’ or ‘Prescriber Notes:’ as appropriate.

Any other relevant medication notes, such as notes relating to medications which were not prescribed by the practice (over the counter, hospital prescribed or similar), **MUST** be indicated by prefixing the note with 'Additional Information: '.

### dosage ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Dosage</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

For provider systems that support fully structured dosage instructions a complete `Dosage` structure should be populated as per [guidance](accessrecord_structured_development_medication_guidance.html#populate-complete-dosage-structure-where-supported).

Where fully structured dosage instructions are not supported by provider systems `Dosage.text` and `Dosage.patientInstruction` should be populated as described below. All other elements that are part of the dosage datatype are optional, and may be populated in line with [ISN DAPB4013](https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections/dapb4013-medicine-and-allergy-intolerance-data-transfer)

### dosage.text ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Complete dosage instructions as text.

Where the dosage instructions have been changed during the lifetime of the Medication/Medical Device plan append the following warning text to end of the dosage instructions:

- "WARNING – Dosage has changed during the effective period. The latest change was made on DD-Mmm-YYYY”, where DD-Mmm-YYYY is the date the dosage was last changed.

In exceptional cases where for legacy data, over-the-counter treatments or hospital treatments there is no dosage recorded in the system then this **MUST** be populated with the text 'No information available' or 'Not recorded' as most appropriate to the circumstance.

### dosage.patientInstruction ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Additional instructions for patient - that is, RHS of prescription label.

<br><br>

<h2 style="color:#ED1951;"> MedicationStatement elements <b>not in use</b> </h2>

The following elements **SHALL NOT** be populated:

<h3 style="color:#ED1951;"> meta.versionId </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> meta.lastUpdated </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Instant</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> extension[ChangeSummary] </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Complex Extension</code></td>
  </tr>
</table>

This is not in scope for this version of GP Connect.

<h3 style="color:#ED1951;"> partOf </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(MedicationAdministration | MedicationDispense | MedicationStatement | Procedure | Observation)</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> category </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> derivedFrom </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Any)</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> reasonNotTaken </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> reasonCode </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

This information is available via linking to a Problem record.

<h3 style="color:#ED1951;"> reasonReference </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Condition | Observation)</code></td>
  </tr>
</table>

This information is available via linking to a Problem record.
