---
title: ProblemHeader (Condition)
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_problems.html
summary: "Guidance for populating and consuming the ProblemHeader (Condition) profile"
div: resource-page
---

## Introduction ##

The headings below list the elements of the ProblemHeader (Condition) profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [ProblemHeader profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ProblemHeader-Condition-1/_history/1.4)." %}

## ProblemHeader (Condition) elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the ProblemHeader (Condition) profile.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The ProblemHeader (Condition) profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ProblemHeader-Condition-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ProblemHeader-Condition-1)

### extension[actualProblem] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A reference to the profile containing the clinical item that has been escalated to create the Problem.

References may be created to `MedicationRequest`, `AllergyIntolerance`, `Immunization`, `Observation - Uncategorised`.

### extension[relatedProblemHeader] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>
A complex extension that details the relationship of this ProblemHeader (Condition) profile to another or a number of other ProblemHeader (Condition) profile.

### extension[relatedProblemHeader.type] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>
A complex extension that details the type of relationship this ProblemHeader (Condition) profile to another ProblemHeader (Condition) profile.

For each `relatedProblemHeader.target` the provider **MUST** supply a value of <code>parent</code>, <code>child</code> or <code>sibling</code>.

### extension[relatedProblemHeader.target] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>
A complex extension that contains a reference to a related ProblemHeader (Condition) profile.

### extension[relatedClinicalContent] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code>reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Contains references to clinical items and consultations that a user in the sending clinical system has chosen to link to this Problem.

When populating this field the provider system must include every clinical item in the patient record that provides information about the problem and includes:
* Clinical items that are directly linked to the problem in the provider system; and
* Clinical items that are within a consultation topic that is linked to the problem

When populating this field the provider system must include every consultation where the problem was discussed or information about the problem was recorded. This includes:
* consultations that are directly linked to the problem in the provider system; and
* consultations that created/updated a clinical item that has been linked to the problem

References may be created to `Encounter`, `MedicationRequest`, `AllergyIntolerance`, `Immunization`, `Observation - Uncategorised`.

### extension[problemSignificance] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The significance of the Problem.
All Problems **MUST** have a severity of <code>major</code> or <code>minor</code>. Where a provider system records more than two levels of severity any level of severity above minor is mapped to major.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

There may be more than one identifier where data has been migrated across practices or provider systems and different provider specific identifiers have been assigned.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

### clinicalStatus ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

All problems **MUST** have a clinicalStatus of <code>active</code> or <code>inactive</code>.

### category ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of <code>problem-list-item</code>.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The clinical code or text that represents the Problem.

These will be the same values that are held in the FHIR&reg; profile referenced by extension[actualProblem].

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the patient who has, or had, the Problem.

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Reference to the encounter where the Problem was initially created.

### onset ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The datetime when the Problem was first encountered.

For example if the patient reported a persistent cough started on the 1st May during a consultation on the 20th May, the onset date would be the 1st May.

### abatement ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The datetime when the Problem was no longer considered active.

### assertedDate ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The datetime that the Problem was recorded on the clinical system.

### asserter ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference (Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to the profile for the practitioner who recorded the Problem.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Notes about the Problem.

<br>
<h2 style="color:#ED1951;"> Condition elements <b>not in use</b> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> severity </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> verificationStatus </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> bodysite </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> stage </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> evidence </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>
