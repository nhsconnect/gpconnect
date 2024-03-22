---
title: Bundle
redirect_to: https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-Searchset-Bundle-1?version=current
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_bundle.html
summary: "Guidance for populating and consuming the Bundle profile"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `Bundle` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with: the underlying [Bundle population illustration diagram](accessrecord_structured_development_retrieve_patient_record.html#bundle-population-illustrated) and the [Bundle profile definition](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--GPConnect-StructuredRecord-Bundle-1?version=current)." %}

## Bundle elements ##

The logical identifier of the `Bundle` profile.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

The Bundle profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1)

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

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A logical id for the bundle. This **MUST** be set to the same value as the `Ssp-TraceID` header in the request.

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

A resource carried within the Bundle.  This can any type of resource, for example `Patient`, `Organization`, `AllergyIntolerance`.

<h2 style="color:#ED1951;"> Bundle elements <b>not in use</b> </h2>

The following elements **SHALL NOT** be populated:

<h3 style="color:#ED1951;"> meta.versionId </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> meta.lastUpdated </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Instant</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> entry.fullUrl </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
  </tr>
</table>
