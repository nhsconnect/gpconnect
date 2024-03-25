---
title: Immunization
redirect_to: https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Immunization-1?version=current
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_immunization.html
summary: "Guidance for populating and consuming the Immunization profile"
div: resource-page
---
## Introduction

The headings below list the elements of the `Immunization` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_immunization.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Immunization profile definition](https://simplifier.net/guide/gpconnect-data-model/Home/FHIR-Assets/All-assets/Profiles/Profile--CareConnect-GPC-Immunization-1?version=current)." %}

## Immunization elements

### id

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the `Immunization` profile.

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

### extension[parentPresent]

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>boolean</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Indicates whether a parent was present at the immunisation.

### extension[recordedDate]

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

This is the date the immunisation record (given or not given) was entered on the clinical system.
This may be an audit trail date or equivalent for the record.
If the immunisation has been transferred by GP2GP this **SHOULD** be the recorded date from the original record entry from the originating system.

### extension[vaccinationProcedure]

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The procedure code describing the vaccine that was administered or the situation code for a vaccination that was intended to be administered but was not done.
See the profile for the valid codes.

### identifier

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

### status

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed to the value `completed` for all Care Connect profiles.

### notGiven

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Value of `false` for vaccinations which have been given (or reported as given).
Value of `true` for vaccinations which were intended but not given.

### vaccineCode

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Vaccine product administered or intended to be administered.

Where the vaccine product that was administered is not known then the null flavour value code <code>UNK</code> **MUST** be populated.

### patient

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the patient due to be immunised.

### encounter

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The consultation within which this immunisation record was captured.
This may represent when the vaccination was administered, intended to be administered or when the registered practice was informed of an immunisation administered elsewhere.

### date

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The date (and time if applicable) when the immunization was administered or intended to be administered.
If the immunisation was administered elsewhere, this may be an estimated or partial date.

### primarySource

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Boolean</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

This indicates whether the record is based on information from the person who administered or intended to administer the vaccine.

This **MUST** be <code>true</code> where the immunisation record was recorded by the person who administered the vaccine or directly on behalf of the administrator of the vaccine (this includes recording the immunisation based on a complete, original, verifiable document from the administration of the vaccine).
This **MUST** be <code>false</code> where it is a secondary report of a vaccination for example the recollection of the patient, the patient's parent, carer or guardian or a secondary document.

As this relates to the context of the original source of the immunisation record, a record from a GP2GP transfer is still a primary record if it was originally recorded as primary.

If it is not known whether the record of the vaccination was made from a primary or secondary source, then return the default value of <code>true</code>.

### reportOrigin

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

This indicates the source of a secondary reported record.

This provides additional context to the source of the immunisation record where it is not based on information from the person who administered the vaccine.
The <code>reportOrigin</code> element can be absent if the record is NOT from a primary source, but the origin of the record is otherwise not recorded / known.

This **MUST** be absent where <code>primarySource</code> is <code>true</code>.

### location

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Location)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The GP practice, branch surgery or other location where the vaccination occurred or was intended to occur, if known.

If the immunisation record in the GP Clinical System does not record a location for the vaccination, but is linked to a consultation then

- if the vaccine was administered or was intended to be administered during the consultation the <code>location</code> **MUST** be populated with the location of the consultation
- if the vaccine was NOT administered or intended to be administered during the consultation and the location for the vaccination is therefore unknown, then a <code>location</code> **MUST** be absent

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
This **MUST** be absent for an intended vaccination which was not given.

### route

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The route through which the vaccine entered the body.
This **MUST** be absent for an intended vaccination which was not given.

### doseQuantity

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>SimpleQuantity</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The amount of the vaccine administered.
This **MUST** be absent for an intended vaccination which was not given.

### practitioner

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The person who recorded the vaccine as having been administered (or reason for not administering an intended vaccination) **MUST** be included.
This **MUST** also include the practitioner who administered the vaccine if different to who recorded the vaccination.

### practitioner.role

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b>Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The role of the referenced practitioner, if known.
Where the role is unknown this **MUST** be absent.

The code <code>EP</code> (Entering Provider) **MUST** be used to designate the practitioner as having recorded the vaccination (or reason not given).

The code <code>AP</code> (Administering Provider) **MUST** be used to designate the practitioner as having administered the vaccination or intending to if the vaccine was not given.

{% include note.html content="EP is not included in the extensible [value set for immunization.practitioner.role](http://hl7.org/fhir/stu3/valueset-immunization-role.html) (which includes only OP and AP codes). EP has been selected from the [parent valueset](http://hl7.org/fhir/stu3/v2/0443/index.html) as a more suitable code. Please use the display name 'Entering Provider' with this code, not the longer description from the value set" %}

### practitioner.actor

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the <code>practitioner</code> profile for who administered and / or recorded the vaccine.

Where there is only a single practitioner recorded against the immunisation record:

- if the practitioner recording the vaccination also administered it (or intended to), then associate a <code>practitioner.role</code> code <code>AP</code> (Administering Provider) with practitioner profile
- if the GP Clinical System cannot determine whether the practitioner administered the vaccine or just recorded the vaccination event or both, then do not return a <code>practitioner.role</code>

This is mandatory where the <code>practitioner.role</code> is populated.

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
This **MUST** be absent if <code>notGiven</code> is <code>true</code>.

### explanation.reasonNotGiven

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The reason why the immunization was not given, such as declined, contra-indicated, unfit or did not attend.
This **MUST** be absent if <code>notGiven</code> is <code>false</code>.

### vaccinationProtocol

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The protocol for the vaccination.
This **MUST** be absent if <code>notGiven</code> is <code>true</code>.

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

The number of doses in the series which are required for vaccination given (at the time it was given / not given).

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

Fixed value `count`

<h2 style="color:#ED1951;"> Immunization elements <b>not in use</b> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> reaction </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

Any reaction to an immunization **MUST** be sent separately in an `AllergyIntolerance` profile.

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
