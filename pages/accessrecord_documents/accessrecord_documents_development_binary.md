---
title: Binary
keywords: documents design
tags: [design,documents]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_documents_development_binary.html
summary: "Guidance for populating and consuming the Binary resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `Binary` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Binary resource definition](https://www.hl7.org/fhir/STU3/binary.html)." %}

## Binary elements ##

The logical identifier of the `Binary` profile.

### contentType ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>type</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Mime type of the document.

### content ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>base64Binary</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The actual content of the document encoded using base64.

<h2 style="color:#ED1951;"> Bundle elements <b>not in use</b> </h2>

The following elements **SHALL NOT** be populated:

<h3 style="color:#ED1951;"> securityContext </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Any)</code></td>
  </tr>
</table>
