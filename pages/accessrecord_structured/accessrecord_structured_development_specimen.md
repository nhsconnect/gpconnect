---
title: Pathology guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_specimen.html
summary: "Guidance for populating and consuming patholgy data in GP Connect"
---
## Introduction ##

The headings below list the elements of the Specimen resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_specimen.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [specimen profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Specimen-1)." %} 

## Specimen resource elements ##


### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the specimen resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The observation profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Specimen-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Specimen-1)

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross care setting identifier which **MUST** be populated. The codeSystem for this identifier is  `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

This  **MUST**  be a GUID.

_Providing_  systems  **MUST**  ensure this GUID is globally unique and a persistent identifier (i.e. doesn’t change between requests and therefore stored with the source data).

Where  _consuming_  systems are integrating data from this resource to their local system, they  **MUST**  also persist this GUID at the same time.


### accessionIdentifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Identifier assigned by the lab

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The availability of the specimen.

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>
 
The general type of test result. A default value of <code>Laboratory</code> should be used if a more specific value is not available e.g. pathology, microbiology etc.


### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the Patient who the observation is about.

### receivedTime###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>instant</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The time when specimen was received for processing
### collection ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The reference range provides a guide for interpretation of the results.

### collection.collector ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference (Practitioner/Organisation)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Reference to the resource for the Practitioner/Organisation that collected the specimen.

### collection.collectedcollected ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime/Period</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The dateTime when the the problem was first encountered.

The dateTime when the the problem was no longer considered active.

### collection.quantity ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>SimpleQuantity</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The reference range provides a guide for interpretation of the results.

### collection.bodysite ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The reference range provides a guide for interpretation of the results.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The reference range provides a guide for interpretation of the results.

## Elements **not in use** ##

The following elements **MUST NOT** be populated:

### parent ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
  </tr>
</table>

### request ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### collection.method ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### processing ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

### processing.description ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### processing.procedure ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### processing.additive ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### processing.time[x] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### container ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### container.identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### container.description ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### container.type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>


### container.capacity ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>

### container.specimenQuantity ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>


### container.additive[x] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
  </tr>
</table>
