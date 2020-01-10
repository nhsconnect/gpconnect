---
title: AllergyIntolerance resource
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_allergyintolerance.html
summary: "Guidance for populating and consuming the AllergyIntolerance resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the AllergyIntolerance resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [AllergyIntolerance profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1/_history/1.2)." %}

## AllergyIntolerance elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the Medication resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The AllergyIntolerance profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1)

### extension[encounter] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code>Reference</code></td>
    <td><b>Optionality:</b>Required</td>
    <td><b>Cardinality:</b>0..1</td>
  </tr>
</table>

Contains a link to the encounter resource.

### extension[allergyEnd] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code>extension</code></td>
    <td><b>Optionality:</b>Required</td>
    <td><b>Cardinality:</b>0..1</td>
  </tr>
</table>

Contains the date and reason the allergy or intolerance was recorded as resolved.

Must be populated if the `clinicalStatus` is set to `resolved`.

### extension[allergyEnd].endDate ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code>dateTime</code></td>
    <td><b>Optionality:</b>Mandatory</td>
    <td><b>Cardinality:</b>1..1</td>
  </tr>
</table>

The date the allergy or intolerance was recorded as resolved.

Must be populated if the `clinicalStatus` is set to `resolved`.

### extension[allergyEnd].endReason ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b>Mandatory</td>
    <td><b>Cardinality:</b>1..1</td>
  </tr>
</table>

The reason why the allergy or intolerance has been resolved. In exceptional cases where for legacy data there is no endReason recorder in the system then this **MUST** be populated with the text 'No information available'.

### extension[evidence] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(DiagnosticReport)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Reference to confirmatory diagnostic report - for example, pathology RAST test result.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

There may be more than one identifier where data has been migrated across practices or provider systems and different provider specific identifiers have been assigned.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

### clinicalStatus ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

`active` for all active allergies. `resolved` for resolved allergies.

GP systems which support the concept of resolved/ended allergies **MUST** set the `clinicalStatus` of resolved allergies to `resolved` and populate the end date field, where an allergy or intolerance is resolved/ended.  

### verificationStatus ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of `unconfirmed`.

{% include important.html content="This value is mandatory in the base FHIR resource so cannot be removed. It is not a concept in GP systems and as such meaning **MUST NOT** be attributed to this field in consuming systems." %}

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Set to `allergy` for reactions which are allergenic in nature (immunological), a value of `intolerance` **MAY** be used to indicate adverse reactions (not immunologic in nature). Where the type is unknown the type element may be omitted.

Some systems allow explicit identification of adverse reactions and intolerances and the type **MUST** be used to make this distinction where it exists.

### category ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

Use `medication` for all drug allergy types, `environment` for all non-drug allergies. The other values in the ValueSet (food and biologic) **MUST NOT** be used.

It is expected that it will always be possible to assign a category of ‘medication’ for drug allergies or ‘environmental’ for all other types of allergy/intolerance. Generally, the choice in a given system is explicit. The GP suppliers MUST follow the categorisation already in use in populating the GP2GP message.

In some cases, the type of allergy/intolerance may be more general - for example, a system designated type of `Other` or equivalent. In such cases, if the allergy/intolerance entry interacts with prescribing decision support it **MUST** be assigned a category of `medication`. Otherwise, the category of `environment` **MUST** be used.

### criticality ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code>Code</code></td>
    <td><b>Optionality:</b>Required</td>
    <td><b>Cardinality:</b>0..1</td>
  </tr>
</table>

Distinguishes between life-threatening (high) and non-life-threatening (low) potential as well as unable-to-assess. It **MAY** be used in addition to severity within the reaction element to express severity - for example, systems that support a severity of life-threatening **MAY** set criticality to high.

It **MAY** be used in conjunction with reaction/severity by systems which support a severity of life-threatening or equivalent.

### code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The causative agent such as food, drug or substances that has caused or may cause an allergy, intolerance or adverse reaction in this patient.

Systems will evolve to use the specified vocabulary of SNOMED CT concepts from the specified subset. The subset includes products and concepts from the substance and product hierarchies and allows medication concepts from the dm+d SNOMED CT extension.

In the interim this coded element will hold the primary code for the AllergyIntolerance which may in the case of drug allergies be a medication code or a pre-coordinated code which triggers decision support on the system.

Where the AllergyIntolerance has no coded representation in the source system, but is identified as such in the source record then the appropriate degrade code may be used and the text of the AllergyIntolerance placed in the text of the code.

{% include tip.html content="Please see [CodeableConcept and common code systems](accessrecord_structured_development_resources_overview.html#codeableconcept-and-common-code-and-identifier-systems) when populating this element." %}

### patient ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

A reference to the Patient who has, or had, the allergy or intolerance specified.

### onset.DateTime ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Date when allergy/intolerance first manifested. Currently restricted to values of dateTime for GP Connect.

This field **MUST** be populated where the GP system records an explicit onset date for an allergy.

### assertedDate ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The datetime the record was recorded or believed to be true.

The asserted date is when the allergy related to the patient was asserted. In many cases, this will be when the allergy is entered onto the system, although some systems may allow this date to be modified.

### recorder ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Who recorded the allergy in the clinical system.

### asserter ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>
Source of the information about the allergy.

### lastOccurrence ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Represents the date and/or time of the last known occurrence of a reaction event.

This data item may not currently be available from providing systems and in this circumstance **MAY** be omitted. Omission **SHOULD NOT** prejudice the ability of providers and consumers to process this element if and when it is available.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

All text associated with the AllergyIntolerance including user-entered notes and qualifiers is grouped together and expressed in this field, which ensures unmapped coded values or qualifiers are not lost.

Must be used to contain any textual data relevant to the allergy.

### reaction.manifestation ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

Conveys the reaction resulting from the allergy/intolerance as a code.

This element is mandatory in the FHIR base profile and so if no data is present please use the nullFlavour as outlined here.

Where no code is available, but a textual description of the reaction is available, then the nullFlavor UNC **MAY** be used and the textual description conveyed via reaction/description.

If no reaction has explicitly been recorded, but the reaction element is present to convey severity, then reaction/manifestation **SHOULD** be coded as the nullFlavor NI.

If the patient has been asked, but is unable to specify a reaction the nullFlavor, ‘ASKU’ **SHOULD** be used.

{% include tip.html content="Please see [CodeableConcept and common code systems](accessrecord_structured_development_resources_overview.html#codeableconcept-and-common-code-and-identifier-systems) when populating this element." %}

### reaction.description ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Conveys the textual description of the manifestation where no code is available.

A consuming system **MAY** concatenate the contents (appropriately labelled) with text in AllergyIntolerance.note if a textual description of the manifestation is not supported in the receiving system record structure.

### reaction.severity ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b><code>Code</code></td>
    <td><b>Optionality:</b>Required</td>
    <td><b>Cardinality:</b>0..1</td>
  </tr>
</table>

Severities of `Mild`, `Moderate`, `Severe` are mapped directly to the ValueSet. Map life threatening to `Severe` and populate criticality with `high`.

### reaction.exposureRoute ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The route by which exposure to the substance causing the reaction occurred. Utilise the dm+d route codes.

{% include tip.html content="Please see [CodeableConcept and common code systems](accessrecord_structured_development_resources_overview.html#codeableconcept-and-common-code-and-identifier-systems) when populating this element." %}


<h2 style="color:#ED1951;">AllergyIntolerance elements <b>not in use</b></h2>

The following elements **SHALL NOT** be populated:

<h3 style="color:#ED1951;">meta.versionId</h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;">meta.lastUpdated</h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Instant</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;">reaction.note</h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
  </tr>
</table>

`AllergyIntolerance.note` should contain all the consolidated text from the Allergy/Intolerance.


<h3 style="color:#ED1951;">reaction.onset[x]</h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
  </tr>
</table>

Onset explicitly supplied via `AllergyIntolerance.onset[dateTime]`.


<h3 style="color:#ED1951;">reaction.substance</h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

The causative is explicitly and specifically coded via AllergyIntolerance.
