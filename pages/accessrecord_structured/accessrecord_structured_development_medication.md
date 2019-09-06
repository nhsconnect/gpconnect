---
title: Medication
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication.html
summary: "Guidance for populating and consuming the Medication profile"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `Medication` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Medication profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1)." %} 

## Medication elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the `Medication` profile.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The Medication profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1)

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The code that identifies the medication or medical device.

A SNOMED dm+d code **MUST** be supplied, if available.

{% include tip.html content="Please see [CodeableConcept and common code systems](accessrecord_structured_development_resources_overview.html#codeableconcept-and-common-code-and-identifier-systems) when populating this element." %}

## Medication elements not in use ##

The following elements **SHALL NOT** be populated:

### meta.versionId ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
  </tr>
</table>

### meta.lastUpdated ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Instant</code></td>
  </tr>
</table>

### package ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

Also do not populate any sub-elements of package.
