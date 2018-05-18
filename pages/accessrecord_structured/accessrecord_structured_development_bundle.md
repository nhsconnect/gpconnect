---
title: Bundle
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_bundle.html
summary: "Guidance for populating and consuming the Bundle resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the Bundle resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with: the underlying [Bundle population illustration diagram](accessrecord_structured_development_retrieve_patient_record.html#bundle-population-illustrated) and the [Bundle profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1)." %} 

## Bundle elements ##

The logical identifier of the Bundle resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The Bundle profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-GetStructuredRecord-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-GetStructuredRecord-Bundle-1)

### meta.lastUpdated ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>instant</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The date and time when the Bundle was created.

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>type</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The type of the Bundle.

Fixed value of `collection`.

### entry ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Items that make up the Bundle.

See below for subelements of this BackboneElement.

### entry.resource ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Resource</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A Resource carried within the Bundle.  This can any type of resource, for example Patient, Organization, AllergyIntolerance.
