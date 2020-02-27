---
title: Diary entry
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_diaryentry.html
summary: "Guidance for populating and consuming the Diary Entry profile"
div: resource-page
---
## Introduction

The headings below list the elements of the `Diary Entry (ProcedureRequest)` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_diaryentry.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [ProcedureRequest profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ProcedureRequest-1)." %}

## Diary Entry (ProcedureRequest) elements

### id

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the `Diary Entry (ProcedureRequest)` profile.

### meta.profile

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The `Diary Entry (ProcedureRequest)` profile URL.

Fixed value **profile**

### identifier

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data).
This **MUST** be scoped by a provider specific namespace for the identifier.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

### status

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The provider **MUST** only include incomplete diary entries - that is, complete or cancelled **MUST NOT** be included.

The <code>status</code> **MUST** only be <code>active</code>.

### intent

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The <code>intent</code> **MUST** only be <code>plan</code>.

### code

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The planned event, action or activity.

### subject

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The patient the diary entry relates to.

### context

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A reference to the consultation from which the diary entry originates - that is, the consultation which the diary entry was created within.

### occurence

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime | Period</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The date or date range when the diary entry is planned to occur.

### authoredOn

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The date the diary entry was entered into the original source system. This may be the audit or equivalent created date for the diary entry.

### requester

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The person or system who entered the diary entry into the original source system.

### requester.agent

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner | Organization | Device)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

This **MUST** be the practitioner who entered the diary entry in the original source system, if it was entered by a user.
If the diary entry was system generated and it is not possible to meaningfully associate the diary entry to a system user then this **MUST** be a <code>Device</code> representing the providing system or an <code>Organization</code> representing the GP practice responsible for creating the record.

### reasonCode

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The reason the action recorded in the diary entry is needed.
This is the trigger reason for the diary entry not the action of the diary entry.

### supportingInfo

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Observation)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Additional clinical information linked to the diary entry **MAY** be included, except a linked problem which **MUST** be included in the bundle as a <code>ProblemHeader(Condition)</code> which references the diary entry, not vice versa.

### note

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Free text narrative to describe the reason for the diary entry or the action / activity required by the diary entry.
This is for additional content beyond the <code>code</code> and <code>reasonCode</code> coded elements and is not intended to duplicate the content of those elements.

<h2 style="color:#ED1951;"> ProcedureRequest elements <b>not in use</b> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> priority </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> doNotPerform </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> category </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> asNeeded </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean | CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> requester.onBehalfOf </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organization)</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> performerType </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> performer </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Device | RelatedPerson | Patient | Organization | Practitioner | HealthService)</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> reasonReference </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Observation | Condition)</code></td>
  </tr>
</table>

A diary entry may have a linked problem which represents the reason for the diary entry.
This is required information where it exists, but the problem **MUST** be included and reference the diary entry.
The diary entry **MUST NOT** reference to the problem.

<h3 style="color:#ED1951;"> specimen </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Specimen)</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> bodySite </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> relevantHistory </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Provenance)</code></td>
  </tr>
</table>

<br>
