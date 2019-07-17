---
title: DocumentReference
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_documents.html
summary: "Guidance for populating and consuming the DocumentReference resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the DocumentReference resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the [DocumentReference profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1)." %}

## DocumentReference elements ##

The logical identifier of the DocumentReference resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

The DocumentReference profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1)

## DocumentReference elements not in use ##

The following elements **SHALL NOT** be populated:


### entry.fullUrl ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
  </tr>
</table>
