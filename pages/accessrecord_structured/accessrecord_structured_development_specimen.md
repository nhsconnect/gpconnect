---
title: Specimen
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_specimen.html
summary: "Guidance for populating and consuming specimen resource data in GP Connect"
div: resource-page
---
## Introduction ##

The headings below list the elements of the Specimen resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_specimen.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [specimen profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Specimen-1/_history/1.3)." %}

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

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.


### accessionIdentifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A business level identifier for the specimen supplied by the performing organisation - for example, the lab performing the test.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
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

The kind of material that forms the specimen.

Examples from substance in SNOMED:
87612001 | Blood (substance) |
53130003 | Venous blood (substance) |


### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the patient who the observation is about.

### receivedTime ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>instant</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The time when specimen was received for processing.

### collection ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Details of when/how the specimen was collected.

### collection.extension[fastingStatus] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept/Duration</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Whether or how long patient abstained from food and/or drink.

Where this is indicated in the incoming EDIFACT report it will be indicated with an 'F'. This **MUST** be used to populate the coding.text element.

### collection.collector ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference (Practitioner)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Reference to the resource for the practitioner who collected the specimen.

### collection.collected ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime/Period</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The date and time when the specimen was collected.

### collection.quantity ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>SimpleQuantity</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The quantity of the specimen that was collected.

### collection.bodysite ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The anatomical site of the specimen collection.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Notes/comments relating to the specimen.

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
