---
title: DiagnosticReport
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_DiagnosticReport.html
summary: "Guidance for populating and consuming patholgy data in GP Connect"
---


## Introduction ##

The headings below list the elements of the Observation resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_observation.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [AllergyIntolerance profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1)." %} 

## DiagnosticReport resource elements ##

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


### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A link to the ProcedureRequest that contains details of request that was made. Where present this may include details of who requested the tests and why the test was requested.

As currently test requests are not submitted in a FHIR format this is not the oigianl request but is currently used as a container to hold details that were present in the original request.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The status of the DiagnosticReport. In GP systems these are most likely to be 'final' however 'preliminary' reports are possible as for example, some work can be sub-contracted to other labs. If the system is not able to determine the status of a report then it should default to the 'unknown' value.

### category ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>
 
The general type of test report. A default value of <code>Laboratory</code> should be used if a more specific value is not available e.g. pathology, microbiology etc.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Due to the model that we have used the clinical code that represents the name of the test/analyte or test set will sit in an observation resource at either the 'Test group header' or 'Test result' level.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the `Patient` who the DiagnosticReport is about.

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The `Encounter` within which the DiagnosticReport was related to.

### issued ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>instant</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The date time that the DiagnosticReport was issued by the laboratory or other report provider.


### performer ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference (Practitioner/Organization)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

Reference to the resource for the Organization that produced the DiagnosticReport. A `practitioner` resource may also be referenced here but only where an `organization` is reference is provided.

### specimen ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Reference to the specimen(s) on which these results were based.

### result ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Reference to the result(s) which are contained in the DiagnosticReport. This may contain references to stan standalone test results, test group headers (which then reference further results) or a mixture of both.

In GP systems this will also contain a reference to an `observation` that contains the details of the time that the report was filed into the patient record. This will be identified as the `observation.code` element will be populated with the SNOMED code ??????

### codedDiagnosis ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>codeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

A coded finding of the test report. Produced by the organisation that performed the tests.

### conclusion ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Clinical Interpretation of test results in a text format and notes written by performing organisation in addition to the interpretation. For example, the sample has haemolysed or has leaked.

For clarity notes may be captured at a number of levels wihtin a DiagnosticReport. There may also be notes related to the specimen, test group header or individual test result. It is the consuming systems responsibility to make sure all relevant notes are displayed to the user.

### presentedForm ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Entire report as issued e.g. the original EDIFact message sent from the lab.

<br>
## Elements **not in use** ##

The following elements **MUST NOT** be populated:

### effective ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
  </tr>
</table>

The time that the report is considered effective or clinically relevant from can be determined from other dates within the report. It may be considered that the date the sample was collected `specimen.collection.collected` or for transfers between GP systems it may be the date it was filed into the GP record. This will be the `observation.effective` from the Observation referenced from `DiagnosticReport.result` where `observation.code` is set to ????????????

### imagingStudy ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

Out of scope for the current iteration.

### image ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

Out of scope for the current iteration.

