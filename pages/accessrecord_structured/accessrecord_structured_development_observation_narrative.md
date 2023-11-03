---
title: Observation - narrative
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_guidance_observation_narrative.html
summary: "Guidance for the representation and consumption of Observation resource representing uncoded freetext narrative"
div: resource-page
---

## Introduction ##

There are many instances of uncoded free text narrative notes within patient records.

* Paragraphs of free text consultation notes perhaps associated with codes via the wider consultation context but not otherwise explicitly coded.
* Text which may or may not be associated with codes but where the association is inexact and it is considered better to express the notes text as a standalone item rather than bind the text (possibly incorrectly) to an associated coded resource. See [Consultation guidance](accessrecord_structured_development_consultation_guidance.html) for further information.
* Representing uncoded or structural elements in patient records for which no suitable resource or is currently available to represent the information and for which falling back to a coded `Observation` resource as the 'uncategorised' representation is inappropriate (for example, no appropriate codes are available to represent the source record entry as an observation).

Because FHIR&reg; does not provide an underlying resource suitable for representing this information, a profile of Observation is utilised to represent narrative text as an Observation Narrative.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Observation profile definition](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Observation-1?version=current)." %}

## Approach ##

The approach for all of these cases is to use an appropriate coded `Observation` resource to represent the free text.

Instances of Observation narrative are identified by Observation.code of **37331000000100  Comment note (record artifact)**

## Observation Elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the Observation narrative resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The Observation narrative profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1)

### meta.security ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Coding</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The security label(s) applicable to the resource.

See [FHIR resources](development_fhir_resource_guidance.html#resources-not-to-be-disclosed-to-a-patient) for more details on how to populate the element.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>status</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of `finished`.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of `37331000000100  Comment note (record artifact)`

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to `Patient` resource representing the patient against whom the narrative text was recorded.

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Optional reference to the `Encounter` resource representing the consultation context in which the narrative free text was recorded. Will not be populated where the free text was recorded outside of a consultation context.

### effectiveDateTime ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>DateTime</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The clinically relevant effective data or datetime for the narrative record entry.

Where the effective date is unknown or not recorded will be absent, otherwise it should be populated.

### issued ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Instance</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The audit trail timestamp representing when the narrative was last modified.

### performer ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The `Practitioner` resource representing the person responsible for recording the narrative.

### comment ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The free text narrative as plain text.

### related ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

This attribute is used to specify the sequence of the narrative in relation to other resources (for example, when an ordered set of resource is being used to express the structure of a consultation displayed at source). See [Consultation guidance](accessrecord_structured_development_consultation_guidance.html) for further information.

The **related.type** and **related.target** are used to represent the sequence. Only the **related.type** value of **'sequel-to'** is utilised.
