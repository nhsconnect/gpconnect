---
title: Consultation
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_composition.html
summary: "Guidance for populating the commposition resource"
---

## Composition elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the Composition resource

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The Composition profile URL.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatroy</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross care setting identifier which MUST be populated. The codeSystem for this identifier is `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

**Is there any cross domain identifier for Composition ? Or should there be other than by convention ?**

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatroy</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed values of **preliminary** or **final**

The **preliminary** value may be used where the sourc system has the concept of draft or provisional consultations, otherwise the status will be **final**.

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Use fixed value code of **325851000000107 |Consultation encounter type (record artifact)|** to identify the Composition type as a GP Connect structured consultation rather than any other document type.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to the Patient resource for the patient whose patient record contains a consultation represented by this Composition resource.

### encounter ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Mandatory reference to the Encounter resource providing the context for the Consultation (Date/Doctor/Place ....)

### date ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The system rather than clinical date time for when the consultation was last edited i.e. the date time the consultation was last modified on the source system.

### author ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The system (audit trail) user attributed to the authoring or modification the consultation.

### title ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The type or name of the consultation as it appears to users of the source system.

### confidentiality ###

Not used in GP Connect

### attester ###

Not used in GP Connect

### custodian ###

Not used in GP Connect

### relatesTo ###

Not used in GP Connect

### event ###

Not used in GP Connect


## Top level Section ##

### Composition.section ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

Represents the top level topic/problem structure of a consultation or in the case of flat 'unstructured' consultations is used to group the resources representing record entries within the source consultation.

### extension.valueId or valueReference - reference may be better ###

TO DO add extension to allow resolution of problem link to composition section - will be back reference to problem id ... nb this is in the 1st instance intended to be used to resolve the problem reference e.g. problem references composition and consumer must then look for the section with the id that corresponds to the problem to make the linkage c

But also is this libnk needed - if standardisation means expanding linkages to child resources?

### Composition.section.title ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Where a consultation section is titled in the source system, carries the title of the consultation as displayed to users. This may be a user entered value or where consultation sections are driven by problems obstained from the term/rubric of the problem linked to the consultation section.

Will not be present where a consultation section is untitled on the source system or where the Consultation.section is conveying unstructured (flat) consultation structure.

### Composition.section.code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Use fixed value of **25851000000105 |Topic (EHR) (record artifact)|**

### Composition.section.text ###

Not used in GP Connect. Any textual rendering of the Composition content can be generated by a receiving system from the structured set of resources referenced within the top level Composition.section or .

### Composition.section.mode ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of **snapshot**.
Explicitly identified that each composition is a snapshot of the current consultation on the source system rather than an incremental update.

### Composition.section.orderedBy ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of **system** from http://hl7.org/fhir/list-order vocabulary.

By convention the order used is the default order subsections or entries are displayed by the native system at source.

### Composition.section.entry ###
<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Observation | AllergyIntolerance | MedicationRequest | ReferralRequest ... TO DO Constrain to finalised set of GP Connect resources)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

A top level section will have entries if it is used to express unstructured (flat) consultation content. Otherwise no entry references will be present.

TBD .... handling of TPP propblem to ... section to linkages possible etxension of section for id

### Composition.section.emptyReason ###

Not used in GP Connect. 

Where a system allows 'empty' sections to be recorded these should be suppressed in any query results in the same way that 'empty' consultations are suppressed.

### Composition.section.section ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>section</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

Each child **.section** of Composition.section is used to represent a sub-heading within a topic level of the source consultation. These are often referred to as SOAP headings but the set of headings/groupings supported by source system consultations is more diverse than the original SOAP classification.

The subssection level is optional because a top level **Composition.section** may be used to contain unstructured (flat) record entries.

A top level **Composition.section** must not be used to represent both unstructured (flat) record contentent and a structured consultation (SOAP Heading structured consultation), therefore **Composition.section.entry** and **Composition.section.section** attributes are mutually exclusive.

## Structured Consultation Content - SOAP Headings ##

Nested **Composition.section.section** attrivutes are used to represent structured consultation content organised around the SOAP heading model.

### Composition.section.section.title ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>string</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Provides the title text displayed for the Consultation sub-heading on the source system. Mandatory because all headings are named/titled.

### Composition.section.section.code ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

TBD - either give it a fixed value like 'Category' or actually attempt to code (but what is the value in this ... just going to get hodegpodeg ef meaningful mapping sbut also lots of other). Also diplication between rubric/text and .title.

### Composition.section.section.text ###

Not used in GP Connect. Any textual rendering of the Composition content can be generated by a receiving system from the structured set of resources referenced within each section.

TBD - demand on outcpome of narrative discussion

### Composition.section.section.mode ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of **snapshot**.
Explicitly identifies that each composition section and subsection is a snapshot of the current consultation on the source system rather than an incremental update.

### Composition.section.section.orderedBy ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of **system** from http://hl7.org/fhir/list-order vocabulary.

By convention the order used is the default order subsections or entries are displayed by the native system at source.

### Composition.section.section.entry ###
<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Observation | AllergyIntolerance | MedicationRequest | ReferralRequest ... TO DO Constrain to finalised set of GP Connect resources)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

Eaxch entry is a reference to the Resoirce representing the source record entry within the heading section.

### Composition.section.emptyReason ###

Not used in GP Connect. 

Where a system allows 'empty' sub-heading sections to be recorded these should be suppressed in any query results in the same way that 'empty' consultations are suppressed.

### Composition.section.section.section ###

Not used in GP Connect. There is no further section structure under the SOAP heading structure.

## TO DO ##
* Empty SOAP sections etc ...
* Encounter guidance, multiple attribution, primary etc ...
* Ordering - system order
* Coding
* Vision - SDA titles as prefix - does it matter
* Query MT Evolution encounters as exception to Evo does not have consultations ?
* MedicationRequest or statement and convention around appearance of MedicationStatement in Bundle
* Technical feasibility of generating references to pre and post when items are queried individually - how does that fit with supplier dataabases which would really need to be FHIR ready for text as well as codes to support this easily.


[1] https://en.wikipedia.org/wiki/SOAP_note
