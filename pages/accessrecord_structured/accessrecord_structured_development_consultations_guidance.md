---
title: Consultation
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_guidance_consultation.html
summary: "Guidance for the representation and consumption of Consultations"
---

{% include structuredwarning.html %}

## Introduction ##
Consultations are one of the most important forms in which structured patient information is recorded in the patient records within GP systems.

However there is no standard structure or format for recording consultations that is common across all systems. This presents not only a challenge in developing a common set of FHIR profiles that are capable of representing the consultation structures that exist within participating systems but also a challenge for producing systems in expressing native consultations in a standardised form as well as being a challenge for consumers in understanding those structures.

It is also important to define what we mean by Consultation. Not all clinical information is recorded consistently across systems within structures that can be classed as Consultations therefore it is important to note that a Consultation oriented query (precise API TBD) may not return all of the clinical information within a patient record.

This document is designed to address these challenges.
* It provides a clear definition of what is meant by Consultation in the context of the current set of participating systems.
* It identifies the limitations of Consultation based queries in isolation as a method for retrieving all elements of patient records.
* It describes the set of Consultation structures available in producer systems and guidance for populating the FHIR resources required to represent these structures.
* It provides guidance for consumer systems processing the FHIR resources represnting Consultation structures on source systems as to the variances between representations and the correct handling of these structures.

## What is a Consultation ? ##
A Consultation is the structure within which source systems group one or more clinical record entries which occurred at the same time and for the same or similar purpose attributed or asserted by the same actor.

* Consultations do not exclusively represent Clinician-Patient encounters although they are commonly used for that purpose.
* Consultations may record purely administrative or communications triggered events on source systems e.g. repeat medication administration, a pathology report filed into the patient record via messaging.
* Consultations are generally assigned and attributed to what can loosely be termed a  'Date/Doctor/Place/Type' (Encounter), although these attributes may be overridden or refined in the context of individual record entries within the Consultation.
* Consultations may or may not have associated structure e.g. the ability to decompose a Consultation into multiple topics/subjects/problems and within each 'topic' further group clinical content under headings (SOAP headings) in line with long standing clinical note taking practice [1]
* Consultations may also be recorded in non-structured form i.e. a grouping of clinical record entries under the same 'Date/Dr/Place/Type' but without additional structure (topics or SOAP headings)
* Consultations may incorporate a range of different record entries e.g. measurements, test results, textual narrative, structured narrative, coded observations, medications

## Approach ##

[Reference out to diagram Consultation FHIR Resource Model ]
[Reference out to diagram Consultation Structure]
* The Encounter resource and related resources like Location are adopted to provide the consultation context (Date/Doctor/Place)
* The Composition resource is adopted to provide consultation structure. The top level Composition.section is utilised to represent the topic/problem level of the source consultation. Within each Composition.section child sections are used to represent headers (SOAP headings) and references to resources within each heading section reference resources representing each record entry within a section.
* Some systems allow the recording of Consultation content outside of the Topic/Problem and Heading hierarchy i.e. a flat structure of record entries organised with the same 'Date/Dr/Place' context. These structures are handled by the creation of an untitled Composition.section to contain the record entries and entries are referenced directly from that section with no additional Heading subsections.

## Suppression of Empty Consultations ##
On some systems all or almost all record entry is captured in the context of a Consultation, this coupled with default behaviours such as starting a consultation on opening a p[atient record, leads to the phenomenon of 'empty consultations' where the Data/Dr/Place/Type has been created as a default but there is no subsequent entry of any clinical information within the consultation.

Producer systems which allow empty consultations should not return empty Consultations in response to Consultation queries.

## What Information May Be Recorded Outside of Consultations ##
* Some systems do not restrict entry of clinical data to a consultation context i.e. it is possible to record clinical information about a patient without starting or initiating a consultation. 
* Such 'Non Consultation' behaviour does not imply any loss of information or structure by the source system i.e. the record items are still fully recorded and attributed
* But because they are recorded outside of a Consultation context they will not be returned by an API query directed at returning Consultation resorces (See Design Decisions Sections).

## Consumer Guidance ##
* Although the expression of full Consultation structure is provided by the specified protocols, it is recognised that many consumers simply want access to the resource referenced by the consultations rather than the Topic or SOAP heading structures. Consumers in the category may simply flatten the consultation structure or otherwise extract the resources referenced within the Composition carrying the consultation structure.

## Information Model ##
The underlying abstract information model is provided below.

## Consumer Cautions ##

* A consumer making Consultation oriented queries only **must not** expect to obtain all items in the patient record
* Other GP Connect APIs will provide full access to items in the patient record including all medications, all allergies, all problems up to an including get whole record queries.

## Design Decisions ##

* Systems which allow direct recording of data outside of Consultation contexts should not fabricate Consultations to return such data when Consultation queries are received as to do so would be generating information and structure which does not exist on the source system and which would obscure the genuine Consultation content that does exist. Systems in this category have clear distinctions between Consultations and other types of record content e.g. last X Consultations displayed in patient summaries and to synthesise consultations would distort this native behaviour.

## Category Mapping ##

|EmisWeb|SystmOne|Vision|
|----|-----|-----|
|Problem|
|History|History|
|Examination|Examination|Examination|
|Family History|
|Social|
|Comment|
|Medication|
|Follow up|
|Procedure|
|Test Request|
|Referral|
|Document|
|Allergy|
||Diagnosis|Diagnosis|
||Intervention|
||Plan|
|||Symptom|

1. All mandatory fields **MUST** be populated.

2. Required fields **MUST** always be populated where the data exists in the system apart from where a lexically identical value exists for an equivalent data item in one of the parent profiles. 

## Encounter elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the Encounter resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The Encounter profile URL.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross care setting identifier which MUST be populated. The codeSystem for this identifier is `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>status</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of **finished**. 

Existing vocabulary is driven by use of Encounter for appointment style encounters rather than provision of consultation context. Hence use most appropriate value from limited set available.

### statusHistory ###

Not used.

### class ###

Not used.

###  classHistory ###

Not used.

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Carries the consultation type as displayed by system via #.text#

TO DO - resolve potential for coding allowing for likely vaguess lack of exact mapping in available codes. Would need definition of appropriate vocabulary. Question value of coding but certainly something that may be of interest.

### priority ###

Not used.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to Patient resource representing the Patient against whom the source consultation/encounter was recorded.

### episodeOfCare ###

Not used

### incomingReferral ###

TO DO: interesting because SystemOne supports this linkage for inbound referrals

### participant ###

Yes - need to look at whether there are appropriate codes vocabularies to define author, primary performer erc ....

### appointment ###

Do we want it ????? Would seem a shame not to hasve it?


### period ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Period</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> </td>
  </tr>
</table>

**.start** is mandatory and should be populated with the displayed consultation date and time 

**.end** should be populated where the encounter end date and time is known or calculated and populated where the duration is known.

The audit trail date time of the consultation is carried by **Composition.date**

### length ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Duration</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> </td>
  </tr>
</table>

Specifies the length of the consultation. Should be calculated and populated where an end time for the consultation is known.

### reason ###

Not used

### diagnosis ###

Not used

### account ###

Not used

### hospitalization ###

Not used

### location ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Location)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

References an instances of the Location resource that provides more detail on where the Consultation/encounter took place e.g. Branch surgery.

**.status** and **.period** are not used

### serviceProvider ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organization)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to the responsible organisation for the encounter.

### partOf ###

Not used.

## Conposition elements ##



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



