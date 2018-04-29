---
title: MedicationStatement resource
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medicationstatement.html
summary: "Guidance for populating and consuming the MedicationStatement resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the MedicationStatement resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_medicationstatement.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [MedicationStatement profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1)" %} 

## MedicationStatement elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the MedicationStatement resource.

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

When the medication was last issued.

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

The `Encounter` within which the medication was authorised.

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

- `active` represents an active authorisation - used for active repeat medications
- `stopped` represents a repeat authorisation which has been discontinued/stopped
- `complete` **MUST** be used for all acute authorisations or any inactive repeat medications that have completed by running their course.

### medicationReference ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Medication)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The medication the authorisation is for.

The `Medication` resource provides the coded representation of the medication.

### effective ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime or Period</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Where a Period is used the start is **MANDATORY**. Where there is a defined expiry or end date in the sending system the end date **MUST** be supplied. For acute prescriptions no specific end date **MUST** be supplied.

### dateAsserted ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

When this medication statement was believed true.

Unless there is a distinct user modifiable availability date/time for the authorisation, this is the audit trail date/time for when the authorisation was entered.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Who the medication is for, i.e. who it will be administered to.

Reference to patient.

### taken ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Whether a medication was taken.

Providers **MUST** use a default value of `unk` – unknown.

### reasonCode ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The coded reason for authorising the medication.

### reasonReference ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Condition), Reference(Observation)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

References the condition or observation that was the reason for this authorisation.

Unless there is a specific linkage in the context of medication, indirect linkages to be handled via Problem list.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

All notes that are associated with this medication record.

All patient notes and prescriber notes at authorisation(plan) and issue(order) level **MUST** be included in this field. They **MUST** be concatenated and indicate the level the notes come from, e.g. 1st Issue and also be prefixed with either ‘Patient Notes:’ or ‘Prescriber Notes:’ as appropriate.

### dosage.text ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Complete dosage instructions as text.

### dosage.patientInstruction ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Additional instructions for patient, i.e. RHS of prescription label.

<br><br>

<h2 style="color:#ED1951;">MedicationStatement elements <b>not in use</b></h2>

The following elements **SHALL NOT** be populated:

<h3 style="color:#ED1951;"><b>partOf</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(MedicationAdministration, MedicationDispense, MedicationStatement, Procedure, Observation)</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect. 


<h3 style="color:#ED1951;"><b>category</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect. 


<h3 style="color:#ED1951;"><b>informationSource</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient, Practitioner, RelatedPerson, Organization)  </code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect. 


<h3 style="color:#ED1951;"><b>derivedFrom</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Any)</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect. 


<h3 style="color:#ED1951;"><b>taken</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect. 


<h3 style="color:#ED1951;"><b>reasonNotTaken</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect. 


<h3 style="color:#ED1951;"><b>medicationEpisodeChangeSummary</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Complex Extension</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect. 
