---
title: Observation - uncategorised data
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_observation_uncategorisedData.html
summary: "Guidance for populating and consuming the Observation profile for uncategorised data"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `Observation` profile and describe how to populate and consume them for uncategorised data.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Observation profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1)." %}

## Observation Elements #

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the uncategorised data `Observation` profile.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The Observation profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1)

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross care setting identifier which MUST be populated. The system  identifier for this is `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

This **MUST** be a GUID.

Providing systems **MUST** ensure this GUID is globally unique and a persistent identifier (i.e. doesn’t change between requests and therefore stored with the source data).

Where consuming systems are integrating data from this profile to their local system, they **MUST** also persist this GUID at the same time.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>status</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of `final`.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The clinical code that represents the data within the observation.

Were the uncategorised data is free text without any clinical code set to 37331000000100 Comment note (record artifact).

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to `Patient` profile representing the Patient against whom the data was recorded.

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Optional reference to the `Encounter` profile representing the consultation context in which the uncategorised data was recorded.

### effectiveDateTime ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>DateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The datetime the observation was believed to be true.

The effective datetime is when the observation related to the patient was asserted. In many cases, this will be when the observation is recorded onto the system however there are situations where they can differ. For example, if an observation is asserted during a home visit that is then recorded on the clinical system the following day, the effective datetime is the when the consultation took place, not the date it was recorded.

### issued ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Instance</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The audit trail timestamp representing when the data was recorded.

### performer ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The `Practitioner` profile representing the clinician responsible for making the observation. Where this is not available, the person who recorded the data item is used.

### value[x] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Many</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The value of the observation. This may be in any of the forms defined in the profile.

### interpretation ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A human-readable clinical summary relating to a test result and/or additional notes provided by the laboratory - for example, the specimen has haemolysed or has leaked.

### comment ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

This **MUST** include any qualifiers to the code element that were present in the sending system. These should be reported as a code and value pair as specified in the [uncategorised data guidance](accessrecord_structured_development_uncategoriseddata_guidance.html).

It **MUST** also include any text relating to the observation.

### referenceRange ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The reference range provides a guide for interpretation of the results.

Where a reference range contains a less than '<' or greater than '>' operator it should be written to the referenceRange.text element as these operators are not supported in this context.

### related ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Contains any hierarchical information between uncategorised data items. 

* Populate `related.target` with a reference to the related item of uncategorised data
* Where the related item is a child of this item set `related.type` to `has-member`
* Where the related item is a parent of this item set `related.type` to `derived-from`

### component ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> BackboneElement</td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The only type of data that **MAY** use the component element is when a blood pressure is recorded as a pair of results.


<br>

<h2 style="color:#ED1951;"> Elements <b>not in use</b> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> basedOn </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> category </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> dataAbsentReason </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> bodysite </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> method </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> specimen </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> device </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>


