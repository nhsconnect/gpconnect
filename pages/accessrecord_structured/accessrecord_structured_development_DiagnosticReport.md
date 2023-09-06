---
title: DiagnosticReport
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_DiagnosticReport.html
summary: "Guidance for populating and consuming investigations data in GP Connect"
div: resource-page
---


## Introduction ##

The headings below list the elements of the `DiagnosticReport` resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_diagnosticReport.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [DiagnosticReport profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DiagnosticReport-1/_history/1.3)." %}

## `DiagnosticReport` resource elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the `DiagnosticReport` resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The `DiagnosticReport` profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DiagnostocReport-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DiagnosticReport-1)

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). An identifier scoped by a provider specific namespace **MUST** be included.
If there is a lab report ID, and if it is scoped to the NHS PMIP Report Numbers CodeSystem (from [HL7 UK Issued OIDs](https://www.hl7.org.uk/standards/object-identifiers-oids/hl7-uk-issued-oids/)) and it could be used to assist in matching lab reports this **SHOULD** also be included. In this case `identifier.system` would be `urn:oid:2.16.840.1.113883.2.1.4.5.5`.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

A link to the ProcedureRequest that contains details of a request that was made. Where present this may include details of who requested the tests and why the test was requested.

As currently test requests are not submitted in a FHIR format this is not the original request but is currently used as a container to hold details that were present in the original request.

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

The general type of test report. A default value of <code>Laboratory</code> should be used if a more specific value is not available - for example, pathology, microbiology.

Consuming systems need to be aware that where more detailed categories are provided the categorisation may vary. How laboratories categorise in the UK is not consistent, and this needs to be taken into account if any type of filtering is being considered.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Due to the model that we have used, the clinical code that represents the name of the test/analyte or test set will sit in an observation resource at either the 'Test group header' or 'Test result' level.

As this item is mandatory in FHIR then suppliers should populate it with the SNOMED ConceptID `721981007` for `Diagnostic studies report`.

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
    <td><b>Data type:</b> <code>reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A reference to the `Encounter` profile representing the consultation the test report is associated to.

### issued ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>instant</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The date and time that the DiagnosticReport was issued by the laboratory or other report provider.

### performer ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner | Organization)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Reference to the resource for the Organization or Practitioner that produced the DiagnosticReport. A `practitioner` resource may  be referenced here but only where an `organization` is reference is provided.

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

Reference to the result(s) which are contained in the DiagnosticReport.
This may contain references to standalone test results, test group headers (which then reference further results) or a mixture of both.

Test results which are part of a test group will not be referenced by this element, the reference will be to the test group which will in turn reference the test results.

In GP systems this will also contain a reference to an `observation` that contains the details of the time that the report was filed into the record.
This will be identified as the `observation.code` element will be populated with the SNOMED code `37331000000100` for `Comment note`.

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

Clinical Interpretation of test results in a text format and notes written by performing organisation in addition to the interpretation. For example, the specimen has haemolysed or has leaked.

For clarity notes may be captured at a number of levels within a DiagnosticReport. There may also be notes related to the specimen, test group header or individual test result. It is the consuming systems responsibility to make sure all relevant notes are displayed to the user.

<br>
<h2 style="color:#ED1951;"> Elements <b>not in use</b> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> effective </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Period</code></td>
  </tr>
</table>

Out of scope for the current iteration.

<h3 style="color:#ED1951;"> imagingStudy </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
  </tr>
</table>

Out of scope for the current iteration.

<h3 style="color:#ED1951;"> image </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

Out of scope for the current iteration.

<h3 style="color:#ED1951;"> presentedForm </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
  </tr>
</table>

Out of scope for the current iteration.
