---
title: Observation - test result
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_observation_testResult.html
summary: "Guidance for populating and consuming the observation to represent test result data in GP Connect"
div: resource-page
---


## Introduction ##

The headings below list the elements of the `Observation` resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available in the [elements not in use section](accessrecord_structured_development_observation.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [observation profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1/_history/1.4)." %}

## Test result - `Observation` resource elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Id</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The logical identifier of the `Observation` resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>uri</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The Observation profile URL.

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

The status of the test result.

In GP systems, these are most likely to be 'final'. However, 'preliminary' reports are possible as, for example, some work can be sub-contracted to other labs. If the system is not able to determine the status of a test group header, then it should default to the 'unknown' value.

### category ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodableConcept</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

The general type of test result. A default value of <code>Laboratory</code> should be used if a more specific value is not available - for example, pathology, microbiology, and so on.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodableConcept</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The clinical code that represents the name of the test result or test analyte.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Patient)</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

A reference to the patient who the observation is about.

### effective[x] ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>dateTime/Period</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The date and time when the test was performed.

### issued ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>instant</code></td>
    <td><strong>Optionality:</strong> Manadatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The date and time that the result was issued by the laboratory or other report provider.

Is this is not provided for an individual result then it should inherit the date from the DiagnosticReport.


### performer ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference (Practitioner/Organisation)</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

Reference to the resource for the organisation and/or practitioner that performed the test.

### value[x] ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Many</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The value of the test. This may be in the form of, but is not limited to, one of the following datatypes: a quantity, string or an attachment.

### dataAbsentReason ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The reason why a result/value has been omitted.

### interpretation ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

A human-readable clinical summary relating to a test result and/or additional notes provided by the laboratory - for example, the specimen has haemolysed or has leaked.

### comment ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>string</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Lab notes in addition to the interpretation. For example, the sample has haemolysed or has leaked.

### bodysite ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The body part that was tested/observed.

### method ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The method of testing/observation that was used.

### specimen ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Reference to the specimen on which these results were based.

### referenceRange ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>BackboneElement</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

The reference range provides a guide for interpretation of the results.

### related ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>BackboneElement</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Reference to the test group header observation if the result is part of a test group.

This **MUST** be qualified using the related.type 'derived-from'.

<br>

## Elements **not in use** ##

The following elements **MUST NOT** be populated:

### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>reference</code></td>
  </tr>
</table>

### context ###

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


### component ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> BackboneElement</td>
  </tr>
</table>
