---
title: List - consultation structure
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_list_consultation.html
summary: "Guidance for populating and consuming the List profile for Consultations"
div: resource-page
---

## Overview

A two or three level <code>List</code> structure is used to represent structured consultations.

1.  **List (Consultation)**
2.  **List (Topic)**
3.  **List (Heading)**

List (Consultation) **SHALL** be coded as **325851000000107 |Consultation encounter type (record artifact)|**.
This top-level profile represents the structured consultation as a whole.

List (Topic) **SHALL** be coded as **25851000000105 |Topic (EHR) (record artifact)|**.
This level represents the Topic/Problem groupings within consultations.

List (Heading) **SHALL** be coded as **24781000000107 |Category (EHR) (record artifact)|**.
This level represents the headings (SOAP heading) levels of the consultation structure that contain record entries.

In the case of consultation which has a 'flat' structure, that is, contains record entries without a surrounding Topic/Heading structure, producer systems generate a List(Topic) level which links directly to record entries without the List(Heading) level.

Empty consultations and empty subsections (topics and headings) are suppressed at source and this is reflected in the cardinalities specified.

{% include important.html content="Any element not specifically detailed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [List profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1)." %}

## Common list attributes

The population of List attributes that are common to all of the consultation list types is described here.

### id

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>Id</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

The logical identifier of the `List` profile.

### meta.profile

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>uri</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

The `List` profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1)

### status

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>Code</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

Fixed value of `current`.

### mode

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>Code</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

Fixed value of `snapshot`.

### subject

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code> Reference(Patient)</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

Reference to the `Patient` profile for the patient whose patient record contains a consultation represented by this `List` profile.

The patient reference is provided by all Lists in the structure rather than the top-level List(Consultation) only.

### encounter

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

Mandatory reference to the `Encounter` profile providing the context for the consultation (Date/Doctor/Place ....)

The Encounter reference is provided by all Lists in the structure rather than the top-level List(Consultation) only.

### date

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>dateTime</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

The system rather than clinical date time for when the consultation was last edited, that is, the date time the consultation was last modified on the source system.

If no separate date time is recorded for consultation sub sections, the overall audit date of the consultation is replicated at all levels.

The clinically significant or effective consultation date is provided by the associated `Encounter` profile.

### orderedBy

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>CodeableConcept</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

Fixed value of `system` from vocabulary.

By convention, the order entries should appear is the default order subsections or entries are displayed by the native system at source.

## List (consultation)

The following attributes are specific to the List level representing the consultation as a whole.

### title

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>string</code></td>
                <td><b>Optionality:</b> Required</td>
                <td><b>Cardinality:</b> 0..1</td>
        </tr>
</table>

The type or name of the consultation as it appears to users of the source system.
This duplicates the consultation type/name provided at <code>Encounter.type</code>.

### code

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>CodeableConcept</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

Fixed value of `325851000000107 |Consultation encounter type (record artifact)|`

### entry

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>BackboneElement</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..*</td>
        </tr>
</table>

Will contain at least one reference to a `List` profile providing the Topic level of the consultation structure. They will be recorded in the same order that the topics appear when viewed in a consultation in the GP system.

## List (Topic)

The List level representing the Topic level of the consultation structure.

### extension(problemReference)

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>reference</code></td>
                <td><b>Optionality:</b> Required</td>
                <td><b>Cardinality:</b> 0..*</td>
        </tr>
</table>

References to any problems that have been linked to this section of the consultation in the sending clinical system.

These links will have been added by a clinician at the sending practice.

### title

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>string</code></td>
                <td><b>Optionality:</b> Required</td>
                <td><b>Cardinality:</b> 0..1</td>
        </tr>
</table>

The name of the corresponding Topic section in the source consultation if it is named.

### code

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>CodeableConcept</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

Fixed value of `25851000000105 |Topic (EHR) (record artifact)|`

### entry

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>BackboneElement</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..*</td>
        </tr>
</table>

Where information within the Topic is organised as sub-headings, <code>entry.list</code> will reference instances of the Category List level.  They will be recorded in the same order that the headings appear when viewed in a consultation in the GP system.

For consultations which have a flat structure (for example, clinical record entries made outside of the Topic and heading structure), an artificial Topic List is generated, and entries will reference profiles representing those record entries (such as, Allergies, Medications, Tests, and so on. They will be recorded in the same order that the items appear when viewed in a consultation in the GP system.

The two approaches are never mixed within the same Topic - that is, all entries will either reference `List(Category)` or profiles representing the source record entries, but not both.

## List (Heading)

The level of the consultation that represents the heading sections (SOAP headings) that contain clinical record entries.

### title

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>string</code></td>
                <td><b>Optionality:</b> Required</td>
                <td><b>Cardinality:</b> 0..1</td>
        </tr>
</table>

The name of the heading section on the source system represented by this List instance.

### code

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>CodeableConcept</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..1</td>
        </tr>
</table>

Fixed value of `24781000000107 |Category (EHR) (record artifact)|`

### entry

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>BackboneElement</code></td>
                <td><b>Optionality:</b> Mandatory</td>
                <td><b>Cardinality:</b> 1..*</td>
        </tr>
</table>

Each <code>entry.item</code> is a reference to a profile representing a clinical record entry in the source system - for example, medications, allergies, problems, diagnoses, and so on. They will be recorded in the same order that the items appear when viewed in a consultation in the GP system.

<h2 style="color:#ED1951;"> List elements <b>not in use</b> for consultations</h2>

The following elements **SHALL NOT** be populated:

<h3 style="color:#ED1951;"> identifier</h3>

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>identifier</code></td>
        </tr>
</table>

<h3 style="color:#ED1951;"> source </h3>

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
        </tr>
</table>

<h3 style="color:#ED1951;"> note </h3>

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>Annotation</code></td>
        </tr>
</table>

<h3 style="color:#ED1951;"> entry.flag </h3>

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>CodeableConcept</code></td>
        </tr>
</table>

<h3 style="color:#ED1951;"> entry.deleted </h3>

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>Boolean</code></td>
        </tr>
</table>

<h3 style="color:#ED1951;"> entry.date </h3>

<table class='resource-attributes'>
        <tr>
                <td><b>Data type:</b> <code>dateTime</code></td>
        </tr>
</table>
