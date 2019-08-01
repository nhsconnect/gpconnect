---
title: Immunization resource
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_immunization.html
summary: "FHIR resource for population guidance for immunization"
div: resource-page
---
## Introduction

The headings below list the elements of the Immunization resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_immunization.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Immunization profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Immunization-1)." %}

## Immunization elements

### id

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the Immunization resource.

### meta.profile

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The Immunization profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Immunization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Immunization-1)

### extension[parentPresent]

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>boolean</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Indicates whether a parent was present at the immunization.

### extension[recordedDate]

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

When the record of the immunization was created on the clinical system.

### extension[vaccinationProcedure]

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The procedure code describing the vaccine that was administered.

### identifier

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross-care setting identifier which **MUST** be populated. The codeSystem for this identifier is  `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

This **MUST** be a GUID.

_Providing_  systems **MUST** ensure this GUID is globally unique and a persistent identifier (that is, it doesn’t change between requests and, therefore, is stored with the source data).

Where  _consuming_  systems are integrating data from this resource to their local system, they **MUST** also persist this GUID at the same time.

### status

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed to the value <code>completed</code> for all CareConnect profiles.

### notGiven

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of <code>false</code>.

### vaccineCode

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Vaccine product administered.

Where the vaccine product that was administered is not known then one of the null values defined in the profile **MUST** be populated.

### patient

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the patient who had the immunisation specified.

### encounter

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The `Consultation` within which the immunisation was recorded.
This may be when the vaccination was administered or when an immunisation administered elsewhere was recorded.

As per base profile guidance.

### date

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The dateTime when the immunization was administered.
If the immunisation was administered elsewhere, this may be an estimated date.

### primarySource

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Default value of <code>true</code> for all profiles created from the Care Connect Immunization profiles.

Indicates the context that the data was recorded in.

### reportOrigin

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Indicates the source of a secondary reported record.

### location

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Location)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The GP practice, branch surgery or other location where the vaccination occurred.

### manufacturer

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organization)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The manufacturer of the vaccine.

### lotNumber

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The batch number of the vaccine.

### expirationDate

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>date</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The expiry date of the batch the vaccine is from.

### site

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The site on the body where the vaccine was administered.

### route

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The route through which the vaccine entered the body.

### doseQuantity

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>SimpleQuantity</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The amount of the vaccine administered.

### practitioner

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The details of the person who administered the vaccine are required.

### practitioner.role

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b>Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The role of the referenced practitioner.

### practitioner.actor

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the practitioner resource that administered the vaccine.
This is mandatory where the practitioner role is populated.

### note

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Notes about the immunization.

### explanation.reason

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The reason why the immunization was given, for example, travel, occupation, and so on.

### vaccinationProtocol

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The protocol for the vaccination.

### vaccinationProtocol.doseSequence

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>positiveInt</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

If the immunisation is achieved via a series of vaccinations, this is the position of the vaccine procedure in the series.

### vaccinationProtocol.description

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

A description for the vaccination protocol this vaccination is administered under.

### vaccinationProtocol.seriesDoses

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>positiveInt</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The number of doses in the series which are required for vaccination given (at the time it was given).

### vaccinationProtocol.targetDisease

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

The disease or diseases the patient is being immunised against.

### vaccinationProtocol.doseStatus

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality</b> Mandatory</td>
    <td><b>Cardinality</b> 1..1</td>
  </tr>
</table>

Fixed value <code>count</code>

<h2 style="color:#ED1951;"> Immunization elements <b>not in use</b> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> explanation.reasonNotGiven </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

Only Immunizations where <code>notGiven</code> is set to <code>false</code> are to be sent using the Immunization profile.
This means that there will never be cause to use <code>reasonNotGiven</code>.

<h3 style="color:#ED1951;"> reaction </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

Any reaction to an immunization **MUST** be sent separately in an <code>AllergyIntolerance</code> resource.

<h3 style="color:#ED1951;"> vaccinationProtocol.authority </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organization)</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> vaccinationProtocol.series </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> vaccinationProtocol.doseStatusReason </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<br>
