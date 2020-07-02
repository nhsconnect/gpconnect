---
title: List
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_list.html
summary: "Guidance for populating and consuming the List profile"
div: resource-page
---

## Introduction ##

The headings below detail the elements of the `List` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically detailed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [List profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1/_history/1.6)." %}


## List elements ##

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>uri</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..*</td>
  </tr>
</table>

The List profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1)


### extension[warningCode] ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Extension</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

A code or codes warning of an issue related to this list.

This extension is used to capture warnings that the list may be incomplete as data has been excluded due to confidentiality or may be missing due to data being in transit. It **MUST** be populated using the appropriate code from the table in the warning codes section on the [resource population fundamentals page](accessrecord_structured_development_resources_overview.html).


### extension[clinicalSetting] ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Extension</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

For GP Connect this should be set to '1060971000000108 General practice service'.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Code</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Whether the list is `current`, `retired` or `entered-in-error`.

`current` **MUST** be used for all lists in GP Connect.

### mode ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Code</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Whether the List has a `mode` of `working`, `snapshot`, or `changes`.

`snapshot` **MUST** be used for all lists in GP Connect.

### title ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>String</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Descriptive name for the list. This will be taken from the 'display' element from the 'code' field.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The purpose of the list.

There are currently 9 possible purposes of a list in response to a query for a clinical area in GP Connect that will be represented by the following SNOMED codes.

| Purpose | SNOMED Code |SNOMED Preferred Term / List.title|
| ------ | ------ |
|Medications and medical devices | 933361000000108| Medications and medical devices |
|Allergies and adverse reactions | 886921000000105| Allergies and adverse reaction  |
|Ended allergies | 1103671000000101| Ended allergies |
|Immunisations | 1102181000000102| Immunisations |
|List of consultations | 1149501000000101 | List of consultations |
|Problems | 717711000000103| Problems |
|Uncategorised data | 826501000000100| Miscellaneous record |
|Outbound Referrals | 792931000000107| Outbound referral |
|Investigations | 887191000000108| Investigations and Results  |
|Diary Entries | 714311000000108 | Patient recall administration |

The above code for 'Ended allergies' should be used for resolved allergies.

{% include tip.html content="Please see [CodeableConcept and common code systems](accessrecord_structured_development_resources_overview.html#codeableconcept-and-common-code-and-identifier-systems) when populating this element." %}

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Patient)</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Reference to the patient.

### date ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>dateTime</code></td>
    <td><strong>Optionality:</strong> Optional</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

When the list was created.

### orderedBy ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Optional</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

What order the list is in.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Annotation</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

The text versions of any warning messages included with the list. Where there are multiple warning messages their text is concatenated.

### entry ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>BackboneElement</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..*</td>
  </tr>
</table>

Entries in the list. Entries are populated in no specific order.

See below for sub elements.

### entry.date ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Boolean</code></td>
    <td><strong>Optionality:</strong> Optional</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

When the item was added to the list.

As GP Connect represents a snapshot at the time the request was made by the consuming system, this is not required to be populated.

### entry.item ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Any)</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Actual entry.

Reference to the item that is part of the list.

### emptyReason ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>CodeableConcept</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Why the list is empty.

A FHIR code of `no-content-recorded` **MUST** be recorded in `emptyReason.code` if a query returns no results to enter into a list. In this case, `List.note` **MUST** be populated with the text 'Information not available'.

<h2 style="color:#ED1951;"> List elements <strong>not in use</strong> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> id </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Id</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> meta.versionId </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Id</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> meta.lastUpdated </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Instant</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> source </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Practitioner, Patient, Device)</code></td>
  </tr>
</table>
