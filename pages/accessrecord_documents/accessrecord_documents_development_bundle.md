---
title: Bundle
keywords: documents design
tags: [design,documents]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_documents_development_bundle.html
summary: "Guidance for populating and consuming the Bundle profile"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `Bundle` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Bundle profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1)." %}

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

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1)

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>type</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The type of the Bundle.

Fixed value of `searchset`.

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

A resource carried within the Bundle. This can be any type of resource, for example `Patient`, `Organization`, `DocumentReference`.

<h2 style="color:#ED1951;"> Bundle elements <b>not in use</b> </h2>

The following elements **SHALL NOT** be populated:

<h3 style="color:#ED1951;"> id </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
  </tr>
</table>

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
