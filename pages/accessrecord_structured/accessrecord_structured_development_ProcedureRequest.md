---
title: ProcedureRequest
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_ProcedureRequest.html
summary: "Guidance on the representation of pathology reporting in GP Connect"
---
## Introduction ##

The headings below list the elements of the ProcedureRequest resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_observation.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [ProcedureRequest profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1)." %} 

## ProcedureRequest resource elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the DiagnosticReport resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The DiagnosticReport profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DiagnostocReport-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DiagnosticReport-1)

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross care setting identifier which **MUST** be populated. The codeSystem for this identifier is  `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

This  **MUST**  be a GUID.

_Providing_  systems  **MUST**  ensure this GUID is globally unique and a persistent identifier (i.e. doesn’t change between requests and therefore stored with the source data).

Where  _consuming_  systems are integrating data from this resource to their local system, they  **MUST**  also persist this GUID at the same time.


### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The status of the ProcedureRequest. Set value of `active`. 

This is mandatory in the base FHIR resource. However as this resource in our model is not being used as a request but to hold data that would have been in a request submitted in a different format we have chosen to use the default value stated. 

### intent ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The status of the ProcedureRequest. Set value of `order`. 

This is mandatory in the base FHIR resource. 

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The tests requested by the requesting HCP.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the `Patient` who the DiagnosticReport is about.

### performer ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference (Practitioner/Organization)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

Reference to the resource for the Organization that produced the DiagnosticReport. A `practitioner` resource may also be referenced here but only where an `organization` is reference is provided.

### requester ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference (Practitioner/Organization)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

Reference to the resource for the Organization that requested the DiagnosticReport. A `practitioner` resource may also be referenced here but only where an `organization` is reference is provided.

### reasonCode ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>codeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

A coded finding of the test report or a textual representation where no code is available. Produced by the organisation that performed the tests.

### reasonReference ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A reference to a resource containing a coded finding of the test report. Produced by the organisation that performed the tests.

<br>

## Elements **not in use** ##

The following elements **MUST NOT** be populated:

### definition ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
  </tr>
</table>

### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
  </tr>
</table>

### replaces ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
  </tr>
</table>

### requistion ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
  </tr>
</table>

### priority ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
  </tr>
</table>

Out of scope for the current iteration.

### doNotPerform ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>boolean</code></td>
  </tr>
</table>

Out of scope for the current iteration.

### category ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

### occurrence[x] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime/Period/Timing</code></td>
  </tr>
</table>

Out of scope for the current iteration.

### asNeeded[x] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean/CodeableConcept</code></td>
  </tr>
</table>

### authoredOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
  </tr>
</table>

### performerType ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

Out of scope for the current itera

### supportingInformation ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

### specimen ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

### bodySite ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeablConcept</code></td>
  </tr>
</table>

### relevantHistory ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

