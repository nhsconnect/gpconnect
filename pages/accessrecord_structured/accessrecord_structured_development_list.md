---
title: List
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_list.html
summary: "Guidance for populating and consuming the List resource"
div: resource-page
---

## Introduction ##

The headings below detail the elements of the `List` resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically detailed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [List profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1)." %}


## List elements ##

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

The List profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1)


### extension[warningCode] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Extension</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

A code or codes warning of an issue related to this list.

This extension is used to capture warnings that the list may be incomplete as data has been excluded due to confidentiality or may be missing due to data being in transit. It **MUST** be populated using the appropriate code from the table in the warning codes section on the [resource population fundamentals page](accessrecord_structured_development_resources_overview.html).


### extension[clinicalSetting] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Extension</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

For GP Connect this should be set to '1060971000000108 General practice service'.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Whether the list is `current`, `retired` or `entered-in-error`.

`current` **MUST** be used for all lists in GP Connect.

### mode ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Whether the List has a `mode` of `working`, `snapshot`, or `changes`.

`snapshot` **MUST** be used for all lists in GP Connect.

### title ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Descriptive name for the list. This will be taken from the 'display' element from the 'code' field.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The purpose of the list.

There are currently 3 possible purposes of a list in GP Connect that will be represented by the following SNOMED codes.
1. Medications and medical devices - 933361000000108
2. Allergies and adverse reactions - 886921000000105
3. Ended allergies - 1103671000000101

The above code for 'Ended allergies' should be used for resolved allergies. This code is new at the time of publishing this version of the specification and will be included in the October 2018 SNOMED release.

{% include tip.html content="Please see [CodeableConcept and common code systems](accessrecord_structured_development_resources_overview.html#codeableconcept-and-common-code-and-identifier-systems) when populating this element." %}

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to the patient.

### date ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

When the list was created.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The text versions of any warning messages included with the list. Where there are multiple warning messages their text is concatenated.

### entry ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Entries in the list. Entries are populated in no specific order.

See below for sub elements.

### entry.date ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

When the item was added to the list.

As GP Connect represents a snapshot at the time the request was made by the consuming system, this is not required to be populated.

### entry.item ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Any)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Actual entry.

Reference to the item that is part of the list.

### emptyReason ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Why the list is empty.

A FHIR code of `No Content Recorded` **SHALL** be used if a query returns no results to enter into a list. In this case, the 'note' field **SHALL** be populated with the text 'Information not available'.

## List elements not in use ##

The following elements **SHALL NOT** be populated:

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
  </tr>
</table>

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

### Source ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner, Patient, Device)</code></td>
  </tr>
</table>

### orderedBy ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

