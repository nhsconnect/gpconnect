---
title: Encounter
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_encounter.html
summary: "Guidance for populating and consuming the Encounter profile for Consultations"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `Encounter` profile and describes how to populate and consume them for Consultations.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [Encounter profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Encounter-1)." %}

## Encounter elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the `Encounter` profile.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The `Encounter` profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Encounter-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Encounter-1)

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross-care setting identifier which **MUST** be populated. The system identifier for this is `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Where the consultation record has been finalised on the provider system set to `finished`.

Where the consultation record has been saved onto the provider system in a draft (or equivalent) status, set to `unknown`.

Existing vocabulary is driven by use of Encounter for appointment style encounters rather than provision of consultation context.
Hence, use the most appropriate value from limited set available.

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Carries the consultation type as displayed by the system. This may be a SNOMED CT code or free text.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to <code>Patient</code> profile representing the patient against whom the source consultation/encounter was recorded.


### participant ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

This **MUST** be populated with the Reference(Practitioner) of the person that recorded the consultation on the system with <code>participant.type</code> value of <code>AUTH</code> from the vocabulary.

Where there are additional participants, will always be populated with at least one <code>participant.individual</code> Reference(Practitioner) with <code>participant.type</code> value of <code>PPRF</code> from the vocabulary.
This should reference a `Practitioner` profile representing the individual with primary attribution for the consultation/encounter (usually the single primary attributed user shown in system journals or other views).

Other participants, such as registrars, trainees or other parties present, may be referenced but with a participation type of <code>PART</code>.

No other values of participation type should be used.

The authorship of the consultation/encounter - that is, the actual user who entered the information on the system should be expressed via <code>List.source</code>.

### period ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Period</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

If recorded, <code>period.start</code> is mandatory and should be populated with the date and time the consultation started.

<code>period.end</code> should be populated where the encounter end date and time is known or calculated and populated where the duration is known.

The audit trail date time of the consultation is carried by the associated consultation list via <code>List.date</code>.

The <code>period</code> attribute may be omitted where the effective/clinical date for the consultation on the source system is not recorded (for example, an unknown date and time).

### length ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Duration</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Specifies the length of the consultation.
Should be calculated and populated where an end time for the consultation is known.

### location ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Location)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

References an instance of the `Location` profile that provides more detail on where the consultation/encounter took place - for example, branch surgery.

<code>location.status</code> and <code>location.period</code> are not used.

### serviceProvider ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organization)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Reference to the responsible organisation for the consultation/encounter.

<br>

<h2 style="color:#ED1951;"> Elements <b>not in use</b> </h2>

The following elements **SHALL NOT** be populated.

<h3 style="color:#ED1951;"> statusHistory </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> class </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Coding</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> classHistory </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> priority </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> episodeOfCare </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(EpisodeOfCare)</code></td>
  </tr>
</table>

The current scope of GP Connect excludes episode of care.

<h3 style="color:#ED1951;"> incomingReferral </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(ReferralRequest)</code></td>
  </tr>
</table>

The current scope of GP Connect excludes inbound referrals.

<h3 style="color:#ED1951;"> appointment </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Appointment)</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> reason </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

The reason for the consultation will be associated to the <code>appointment</code>.

<h3 style="color:#ED1951;"> diagnosis </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

The diagnosis will be associated to the consultation via the <code>list</code> profile.

<h3 style="color:#ED1951;"> account </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Account)</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> hospitalization </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> partOf </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
  </tr>
</table>
