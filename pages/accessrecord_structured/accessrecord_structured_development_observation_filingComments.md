---
title: Observation
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_observation_filingComments.html
summary: "Guidance for populating and consuming investigations data in GP Connect"
div: resource-page
---


## Introduction ##

The headings below list the elements of the `Observation` resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_observation.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [observation profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1/_history/1.7)." %}

## Filing comments - `Observation` resource elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the observation resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The observation profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1)

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

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

For filing comments this is a set value of 'unknown'.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of `37331000000100` for `Comment note`.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the patient who the observation is about.

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A reference to the `Encounter` profile representing the consultation the test report is filed against.

### effective[x] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime/Period</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The dateTime when the 'Test report', 'Test group' or 'Test result' was filed into the patient record.

### issued ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>instant</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The date time that the time/comment was recorded in the GP system.

### performer ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference (Practitioner/Organisation)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

Reference to the resource for the organisation and/or practitioner that filed the 'Test report', 'Test group' or 'Test result' was filed into the patient record.

### value[x] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Many</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Where a 'Test group' or 'Test result' has been filed the value should match the code from the 'Test group header' or 'Test result' resource respectively.

### comment ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Notes added by the GP practice clinician about the 'Test report', 'Test group' or 'Test result' that has been filed into the patient record.


### related ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Reference to the test result or test group header that the filing comments resource relates to.
Where the filing comments relate to the test report, the reference is made from the 'Test report' to the filing comment only.

This **MUST** be qualified using the related.type 'derived-from'.

<br>

## Elements **not in use** ##

The following elements **MUST NOT** be populated:

### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
  </tr>
</table>

### category ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodableConcept</code></td>
  </tr>
</table>

### dataAbsentReason ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

### interpretation ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

### bodysite ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>


### method ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

### specimen ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

### referenceRange ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

### device ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### component ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>
