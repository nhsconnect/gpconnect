---
title: Condition ProblemHeader resource
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_problems.html
summary: "Guidance for populating and consuming the ProblemHeader resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the Immunization resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_allergyintolerance.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [ProblemHeader profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ProblemHeader-Condition-1)." %}

## Condition - problem header elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the ProblemHeader resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The ProblemHeader profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Condition-ProblemHeader-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Condition-ProblemHeader-1)

### extension[actualProblem] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A reference to the resource containing the clinical item that has been escalated to create the problem.

References may be created to MedicationRequest, AllergyIntolerance, Immunization, Observation - Uncategorised.

### extension[relatedProblemHeader] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>
A complex extension that details the relationship of this problem header resources to another or a number of other problem header resources.

### extension[relatedProblemHeader.type] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>
A complex extension that details the type of relationship this problem header resources to another problem header resources.

For each relatedProblemHeader.target the provider **MUST** supply a value of <code>Parent</code>, <code>Child</code> or <code>Sibling</code>.

### extension[relatedProblemHeader.target] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>
A complex extension that contains a reference to a related problem header resource.

### extension[relatedClinicalContent] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code> codableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

References to other resources that a user in the sending clinical system has chosen to link to this problem header resource.

When populating this field the provider system must include every item in the patient record that provides information about the problem and includes:
* Clinical items that are directly linked to the problem in the provider system; and
* Clinical items that are within a consultation topic that is linked to the problem

References may be created to MedicationRequest, AllergyIntolerance, Immunization, Observation - Uncategorised.

### extension[problemSignificance] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code> codableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The significance of the problem contained in the resource.
All problems **MUST** have a severity of <code>major</code> or <code>minor</code>. Where a provider system records more than two levels of severity any level of severity above minor is mapped to major.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross-care setting identifier which **MUST** be populated. The codeSystem for this identifier is  `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

This  **MUST**  be a GUID.

_Providing_  systems  **MUST**  ensure this GUID is globally unique and a persistent identifier (that is, it doesn’t change between requests and therefore stored with the source data).

Where  _consuming_  systems are integrating data from this resource to their local system, they  **MUST**  also persist this GUID at the same time.

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
    <td><b>Data type:</b> <code>CodableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of <code>problem-list-item</code>.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The clinical code or text that represents the problem header.

These will be the same values that are held in the FHIR&reg; resource referenced by extension[actualProblem].

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the patient who has, or had, the allergy or intolerance specified.

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

References to encounters that a user in the sending clinical system has chosen to link to this problem header resource.

When populating this field the provider system must include every consultation where the problem was discussed or information about the problem was recorded. This includes:
* consultations that are directly linked to the problem in the provider system; and
* consultations that created/updated a clinical item that has been linked to the problem

### onset ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The datetime when the problem was first encountered.

### abatement ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The datetime when the problem was no longer considered active.

### assertedDate ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The datetime that the problem was recorded on the clinical system.

### asserter ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference (Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to the resource for the practitioner who recorded the problem.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Notes about the problem.


<br>
## Elements **not in use** ##

The following elements **MUST NOT** be populated:

### severity ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

### verificationStatus ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
  </tr>
</table>

### bodysite ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### stage ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

### evidence ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>
