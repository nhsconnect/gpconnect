---
title: DocumentReference
keywords: structured design
tags: [design,structured]
sidebar: access_documents_sidebar
permalink: access_documents_development_documentreference.html
summary: "Guidance for populating and consuming the DocumentReference resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the DocumentReference resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the [DocumentReference profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1/_history/1.2)." %}

## DocumentReference elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Id</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

The logical identifier of the DocumentReference resource.


### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>uri</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..*</td>
  </tr>
</table>

The DocumentReference profile URL.

Fixed value `https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1`

### masterIdentifier ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Id</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Master Version Specific Identifier. This unique identifier is used to identify the version of the document

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Identifier</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..*</td>
  </tr>
</table>

This is for business identifiers.
This is sliced to include a cross-care setting identifier which **MUST** be populated. The codeSystem for this identifier is  `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.
This **MUST** be a GUID.

_Providing_  systems **MUST** ensure this GUID is globally unique and a persistent identifier (that is, it doesn’t change between requests and, therefore, is stored with the source data).

Where  _consuming_  systems are integrating data from this resource to their local system, they **MUST** also persist this GUID at the same time.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>code</code></td>
  </tr>
</table>

current | superseded | entered-in-error
This field will always have default value of current as only the latest version of the document is retrieved.

### type ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>codeableConcept</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Kind of document, a value **SHOULD** be taken from the SNOMED refset 999000391000000109. Other classifications of documents should be sent as `text`.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(CareConnect-GPC-Patient-1 | CareConnect-GPC-Practitioner-1)</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

A reference to the patient who is the subject of the document.

### created ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> DateTime</td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Creation/Edit datetime of the document.

### indexed ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Instant</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

When the GP Practice added the document to their clinical system.

### author ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference ( CareConnect-GPC-Practitioner-1 | CareConnect-GPC-Organization-1 )</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Who and/or what authored the document.


### custodian ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(Organisation)</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Organisation which maintains this document.


### description ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>string</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Human-readable description (title).

### content.attachment.url ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>url</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

URL to retrieve the document, this **MUST** be populated when the document is available. It is a reference to the document data i.e. the binary resource.

### content.attachment.size ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>unsignedInt</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Size of the file.

### content.attachment.title ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>string</code></td>
    <td><strong>Optionality:</strong> Optional</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

To be used when only a placeholder for a document is available. This **MUST** be populated with the reason why the file isn't available.

### content.format ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>coding</code></td>
    <td><strong>Optionality:</strong> Mandatory</td>
    <td><strong>Cardinality:</strong> 1..1</td>
  </tr>
</table>

Format/content rules for the document.

### context.encounter ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(CareConnect-GPC-Encounter-1)</code></td>
    <td><strong>Optionality:</strong> Required/Optional</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Reference to the consultation the document was created/attached in.

### context.practiceSetting ###

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>codeableConcept</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Additional details about where the content was created (for example, clinical specialty).


<h2 style="color:#ED1951;"> Elements <strong>not in use</strong> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> docStatus </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference(preliminary | final | appended | amended | entered-in-error)</code></td>
  </tr>
</table>

This is not required by GP Connect.

<h3 style="color:#ED1951;"> class </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>codeableConcept</code></td>
  </tr>
</table>

Categorization of document is not required by GP Connect.

<h3 style="color:#ED1951;"> authenticator </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>Reference ( CareConnect-GPC-Practitioner-1 | CareConnect-GPC-Organization-1 )</code></td>
  </tr>
</table>

Who/what authenticated the document is not required by GP Connect.

<h3 style="color:#ED1951;"> content.attachment.data </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>base64Binary</code></td>
  </tr>
</table>
Data of the attachment is not required by GP Connect as it will be populated in FHIR binary resource. 

<h3 style="color:#ED1951;"> relatesTo </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>code</code></td>
  </tr>
</table>
replaces | transforms | signs | appends
Relationships to other documents is not required by GP Connect.

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong><code>Reference(CareConnect-GPC-Patient-1)</code></td>
    <td><strong>Optionality:</strong> Required</td>
    <td><strong>Cardinality:</strong> 0..1</td>
  </tr>
</table>

Patient demographics from source.

<h3 style="color:#ED1951;"> securityLabel </h3>

<table class='resource-attributes'>
  <tr>
    <td><strong>Data type:</strong> <code>codeableConcept</code></td>
  </tr>
</table>

Document security-tags is not required by GP Connect.

<br>
