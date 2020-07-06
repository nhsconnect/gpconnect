---
title: Observation - test group header
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_observation_testGroup.html
summary: "Guidance for populating and consuming Observation resource where used in a test group header GP Connect"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `Observation` resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available in the [elements not in use section](accessrecord_structured_development_observation.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Observation profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1/_history/1.4)." %}

## Test group header - `Observation` resource elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Id</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The logical identifier of the observation resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>uri</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The observation profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1)

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Identifier</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Code</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The status of the test group header.

In GP systems, these are most likely to be 'final'. However, 'preliminary' reports are possible as, for example, some work can be sub-contracted to other labs. If the system is not able to determine the status of a test group header then it should default to the 'unknown' value.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodableConcept</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The clinical code that represents the name of the test group - for example, Full blood count.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Patient)</code></td>
    <td><strong>Optionality:</strong> Optional</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

A reference to the patient who the observation is about.

### performer ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference (Practitioner/Organisation)</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

Reference to the resource for the Organization that carried out the tests. A `Practitioner` resource may also be referenced here but only where an `organization` is reference is provided.


### comment ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>string</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Notes that relate to the test group header that were written by the performing `organization`.

For example, the sample has haemolysed or has leaked.

### specimen ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Reference to the specimen on which these results were based.

### related ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>BackboneElement</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

Reference(s) to the test result(s) observation(s) that make up the test group.

This **MUST** be qualified using the related.type 'has-member'.

<br>

## Elements **not in use** ##

The following elements **MUST NOT** be populated:

### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>reference</code></td>
  </tr>
</table>

### category ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### context ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### effective[x] ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
  </tr>
</table>

### issued ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### value ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### dataAbsentReason ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### interpretation ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### bodysite ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### method ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### device ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>

### ReferenceRange ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>


### component ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>
