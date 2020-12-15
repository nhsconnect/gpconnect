---
title: Consultation
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_consultation_guidance.html
summary: "Guidance for the representation and consumption of consultations"
---

## Introduction

Consultations are one of the most important forms in which structured clinical information is recorded in the patient records within GP systems.

However, there is no standard structure or format for recording consultations that is common across all systems.

This presents a challenge in developing a common set of FHIR profiles that are capable of representing the consultation structures that exist within participating systems.

It is also a challenge for provider systems in expressing native consultations in a standardised form as well as being a challenge for consumers in understanding those structures.

It is important to define what we mean by consultation. Not all clinical information is recorded consistently across systems within structures that can be classed as consultations. Therefore, it is important to note that a consultation-oriented query alone will not return all of the clinical information held within a patient record.

This document is designed to address these challenges:

-   it provides a clear definition of what is meant by consultation in the context of the current set of participating provider systems
-   it identifies the limitations of consultation-based queries in isolation as a method for retrieving all elements of patient records
-   it describes the set of consultation structures available in provider systems and guidance for populating the FHIR resources required to represent these structures in a consistent manner that is processable by consumers
-   it provides guidance for consumer systems processing the FHIR resources representing consultation structures on source systems as to the variances between representations and the correct handling of these structures

## What is a consultation?

For GP Connect, a consultation is the structure within which source systems group one or more clinical record entries which occurred at the same time and for the same or similar purpose attributed to or asserted by the same actor.

- the provider system determines under what circumstances to create a consultation - this may vary between provider systems
- consultations do not exclusively represent clinician-patient encounters, although they are commonly used for that purpose
- consultations may record purely administrative or communications triggered events on source systems (for example, repeat medication administration, a pathology report filed into the patient record via messaging workflow)
- consultations are generally assigned and attributed to what can loosely be termed a 'Date/Doctor/Place/Type' (Encounter), although these attributes may be overridden or refined in the context of individual record entries within the consultation
- consultations may or may not have associated structure (for example, the ability to decompose a consultation into multiple topics/subjects/problems and within each 'topic' further group clinical content under headings (SOAP headings) in line with long standing clinical note taking practice)
- consultations may also be recorded in non-structured form - that is, a grouping of clinical record entries under the same 'Date/Dr/Place/Type' but without additional structure (topics or SOAP headings)
- consultations may incorporate a range of different record entries (for example, measurements, test results, textual narrative, structured narrative, coded observations, medications)

## Logical structure

Consultations follow a common logical structure:

-   Context

    Each consultation has context data that describes when and where the consultation took place, the patient it covered, and who else was involved (such as a doctor). This information is usually generated automatically by the provider system but it may include some manually recorded values.

-   Topics

    A Consultation will be split into one of more topics. Each topic describes an area of discussion (or activity) that took place in the Consultation.

    A topic may (or may not) have a title.

    A topic may (or may not) be related to a specific problem in the patient’s record. In these cases, all the discussions and activities recorded under that topic are in regard to that problem.

-   Headings

    A topic may be split into one of more headings (sometimes referred to as SOAP headings). Each heading covers a specific part of the Consultation process about that topic.

    There is no national standard for headings so they will reflect the headings available in the provider clinical system.

-   Clinical items

    Within each heading there may be one or more clinical items. Grouped together and in order, these clinical items describe in full all the details recorded under that heading of the consultation.

    Any type of clinical item may form part of the consultation (medications, allergies, immunisations, uncategorised data, and so on).

-   Topics without headings

    A topic can be created without headings. In these cases, the clinical items are recorded directly under the topic the same way they are recording under a heading.

## Approach

The logical structure of a Consultation is reflected in FHIR using the `Encounter` and `List` profiles.

<table class='resource-attributes'>
  <tr>
    <td width="15%"><strong>Logical Structure</strong></td>
    <td width="15%"><strong>FHIR Profile</strong></td>
    <td width="70%"><strong>Description</strong></td>
  </tr>
  <tr>
    <td>Context</td>
    <td>Encounter</td>
    <td>The Context information is held in the Encounter profile.</td>
  </tr>
  <tr>
    <td>-</td>
    <td>List</td>
    <td>The clinical information is grouped and organised within multiple List profiles. The top level list contains references to each of the Topics within the Consultation.</td>
  </tr>
  <tr>
    <td>Topic</td>
    <td>List</td>
    <td>Each Topic is held as a List containing references to each of the Headings under the Topic.<br>Where a Topic does not contain Headings the List directly references Clinical Items.</td>
  </tr>
  <tr>
    <td>Heading</td>
    <td>List</td>
    <td>Each Heading is held as a List containing references to each of the Clinical Items under the Heading.</td>
  </tr>
  <tr>
    <td>Clinical Items</td>
    <td>Appropriate FHIR profile</td>
    <td>Each Clinical Item will be head in the appropriate FHIR profile as defined elsewhere in this specification.</td>
  </tr></table>

## Consultation structure

<object type="image/svg+xml" data="images/access_structured/Consultation_FHIR_Resource_Model.svg" style="max-width:100%;max-height:100%;display:block;margin: 0 auto;" alt="Consultation FHIR Resource Model"></object>
<br/>

\* Cardinalities in the above diagram are based on a principle of suppressing empty consultations and subsections at source.

<br>

<div class="screen-reader-text">
A consultation FHIR resource model diagram summarises the previous description of consultation structure. In addition, it shows that a consultation or record entry may be attributed to more than one actor acting in a different role. It states that record entries may appear directly within a consultation without being embedded in the topic/heading structure. By convention, an artificial topic level will be generated to accommodate record entries recorded within this flat structure. A consultation may exhibit both styles but be represented within different topics. The diagram also says that each heading may contain multiple record entries of different types represented by an appropriate FHIR resource.
</div>

<object type="image/svg+xml" data="images/access_structured/Consultation_Structure.svg" style="max-width:200%;max-height:200%;display:block;margin: 0 auto;" alt="Consultation Structure"></object>

	
<div class="screen-reader-text">
The diagram shows a consultation split into topics with headings and entries. Record entries may also appear directly within a consultation outside the topic/section level. Entries are handled directly within a generated topic level. The logical structure of a Consultation is reflected in FHIR using the Encounter and List profiles. Consultations may incorporate a range of different record entries, such as observations.
</div>

## Consultation notes

Consultation notes are the human readable version of the clinical information recorded under each heading. They may or may not be accompanied by a clinically coded version of the information.

There are two primary ways that consultation notes are recorded on native GP systems:

-   Consultation notes for a heading are recorded as a single piece of free text. Any clinical coded information under the same heading is associated to that text as a whole.

<p style="text-align:center; font-size:22px; color:#005eb8">
	Model One
</p>
<div class="blue-diagram">
	The patient has Temperature 36.7 C Patient looks flushed. <br/>
	Arterial oxygen saturation room air at rest 96%. Respiratory rate <br/>
	16 / min Taken over 30 seconds. Pulse irregularly irregular 70 / min <br/>
	Swelling lower legs bilaterally. Mild pitting oedema. Chest <br/>
	clear. Heart sounds normal. No distress. Abdomen normal. <br/>
	No cervical lymphadenopathy. Throat normal. Ears normal.
</div>
<p></p>
<div class="blue-diagram">
	Uncategorised - 703421000 - Temperature <br/>
	36.7 C <br/>
</div>
<p></p>
<div class="blue-diagram">
	Uncategorised - 1097811000000100 - Arterial oxygen <br/>
	saturation breathing room air at rest <br/>
	96%
</div>
<p></p>
<div class="blue-diagram">
	Uncategorised - 86290005 - Respiratory rate <br/>
	16 / min <br/>
</div>
<p></p>
<div class="blue-diagram">
	Uncategorised - 271637005 - Pulse irregularly irregular <br/>
	70 / min <br/>
</div>
<br/>


-   Consultation notes for a heading are recorded as a collection of observations, each with a clinical code and or text. When read together in order they produce the consultation notes.
    Note – this may be entering free text format dynamically identifying codes or through forms where there are specific fields for codes and free text.


<br/>
<p style="text-align:center; font-size:22px; color:#005eb8">
	Model Two
</p>
<div class="blue-diagram">
	Uncategorised - 703421000 - Temperature <br/>
	36.7 C <br/>
	Patient looks flushed
</div>
<p></p>
<div class="blue-diagram">
	Uncategorised - 1097811000000100 - Arterial oxygen <br/>
	saturation breathing room air at rest <br/>
	96%
</div>
<p></p>
<div class="blue-diagram">
	Uncategorised - 86290005 - Respiratory rate <br/>
	16 / min <br/>
	Taken over 30 seconds
</div>
<p></p>
<div class="blue-diagram">
	Uncategorised - 271637005 - Pulse irregularly irregular <br/>
	70 / min <br/>
</div>
<p></p>
<div class="blue-diagram">
	Uncategorised - 37331000000100 - Comment Note <br/>
	Swelling lower legs bilaterally. Mild pitting oedema. Chest <br/>
	clear. Heart sounds normal. No distress. Abdomen normal. <br/>
	No cervical lymphadenopathy. Throat normal. Ears normal.
</div>

<br/>
When reflecting these in FHIR it is important they these two methods are represented in a way that retains the structural information they contain, does not create any unintended clinical meaning and can be viewed / imported. This is done by taking any free text in model one and representing it as uncategorised data and positioning it as the first clinical item under the heading.
<br/>
<br/>
<div class="flex-container">
  <div class="flex-child">
	<p style="text-align:center; font-size:22px; color:#005eb8">
		From Model One
	</p>
	<div class="blue-diagram-full">
		The patient has Temperature 36.7 C Patient looks flushed. <br/>
		Arterial oxygen saturation room air at rest 96%. Respiratory rate <br/>
		16 / min Taken over 30 seconds. Pulse irregularly irregular 70 / min <br/>
		Swelling lower legs bilaterally. Mild pitting oedema. Chest <br/>
		clear. Heart sounds normal. No distress. Abdomen normal. <br/>
		No cervical lymphadenopathy. Throat normal. Ears normal.
	</div>
	<p></p>
	<div class="blue-diagram-full">
		Uncategorised - 703421000 - Temperature <br/>
		36.7 C <br/>
	</div>
	<p></p>
	<div class="blue-diagram-full">
		Uncategorised - 1097811000000100 - Arterial oxygen <br/>
		saturation breathing room air at rest <br/>
		96%
	</div>
	<p></p>
	<div class="blue-diagram-full">
		Uncategorised - 86290005 - Respiratory rate <br/>
		16 / min <br/>
	</div>
	<p></p>
	<div class="blue-diagram-full">
		Uncategorised - 271637005 - Pulse irregularly irregular <br/>
		70 / min <br/>
	</div>
  </div>
  
  <div class="flex-child">
	<p style="text-align:center; font-size:22px; color:#005eb8">
		From Model Two
	</p>
	<div class="blue-diagram-full">
		Uncategorised - 703421000 - Temperature <br/>
		36.7 C <br/>
		Patient looks flushed
	</div>
	<p></p>
	<div class="blue-diagram-full">
		Uncategorised - 1097811000000100 - Arterial oxygen <br/>
		saturation breathing room air at rest <br/>
		96%
	</div>
	<p></p>
	<div class="blue-diagram-full">
		Uncategorised - 86290005 - Respiratory rate <br/>
		16 / min <br/>
		Taken over 30 seconds
	</div>
	<p></p>
	<div class="blue-diagram-full">
		Uncategorised - 271637005 - Pulse irregularly irregular <br/>
		70 / min <br/>
	</div>
	<p></p>
	<div class="blue-diagram-full">
		Uncategorised - 37331000000100 - Comment Note <br/>
		Swelling lower legs bilaterally. Mild pitting oedema. Chest <br/>
		clear. Heart sounds normal. No distress. Abdomen normal. <br/>
		No cervical lymphadenopathy. Throat normal. Ears normal.
	</div>
  </div>
</div>

<br/>

While there are differences between the two outputs, the consultation notes can be derived from both by reading through each clinical item in order and merging the Term Text, Clinical Code, Values and Comment into a single narrative.

<br/>

<div class="flex-container">
  <div class="flex-child">
	<p style="text-align:center; font-size:22px; color:#005eb8">
		From Model One
	</p>
	<div class="blue-diagram-full">
		The patient has Temperature 36.7 C Patient looks flushed. <br/>
		Arterial oxygen saturation room air at rest 96%. Respiratory rate <br/>
		16 / min Taken over 30 seconds. Pulse irregularly irregular 70 / min <br/>
		Swelling lower legs bilaterally. Mild pitting oedema. Chest <br/>
		clear. Heart sounds normal. No distress. Abdomen normal. <br/>
		No cervical lymphadenopathy. Throat normal. Ears normal. <br/>
		Temperature (703421000) 36.7 C <br/>
		Arterial oxygen saturation breathing room air at rest <br/>
		(1097811000000100) 96% <br/>
		Respiratory rate (86290005) 16 / min <br/>
		Pulse irregularly irregular (271637005) 70 / min
	</div>
  </div>
  <div class="flex-child">
	<p style="text-align:center; font-size:22px; color:#005eb8">
		From Model Two
	</p>
	<div class="blue-diagram-full">
		Temperature (703421000) 36.7 C Patient looks flushed <br/>
		Arterial oxygen saturation breathing room air at rest <br/>
		(1097811000000100) 96% <br/>
		Respiratory rate (86290005) 16 / min Taken over 30 seconds <br/>
		Pulse irregularly irregular (271637005) 70 / min <br/>
		Swelling lower legs bilaterally. Mild pitting oedema. Chest <br/>
		clear. Heart sounds normal. No distress. Abdomen normal. <br/>
		No cervical lymphadenopathy. Throat normal. Ears normal.
	</div>
  </div>
</div>
<br/>

## Example

<br/>
<object type="image/svg+xml" data="images/access_structured/Consultation_Example_v6.svg" style="max-width:60%;max-height:60%;display:block;margin: 0 auto;" alt="Sequence diagram for retrieving a patient record"></object>
<br/>

<div class="screen-reader-text">
This diagram is explained in the following text:
</div>

## Clinical item references ##

When a clinical item is linked to the consultation a reference to its FHIR® resource is held in the entry.item field of the appropriate list resource.

When linking to a clinical item that is held in a single FHIR resource the reference will be to that resource. When linking to the clinical item that is held across multiple resources (for example, Medication and Medical Device) the reference must be to the FHIR resource specified below.

* For a Medication or Medical Device prescription plan - reference the `MedicationRequest` (intent = plan) profile
* For a Medication or Medical Device prescription issue - reference the `MedicationRequest` (intent = order) profile
* For an Allergy – reference the `Allergy` profile
* For an Immunisation – reference the `Immunization` profile
* For Uncategorised Data – reference the `Observation` – Uncategorised profile
* For a Referral - reference the `ReferralRequest` profile
* For a Document - reference the `DocumentReference` profile
* For an Investigation - reference the `DiagnosticReport` profile
* For a Diary Entry - reference the `ProcedureRequest` profile

## Consultations containing unsupported clinical items

Depending on the GP Connect version supported by the provider system it can be possible for the consultation to link to a clinical item that the provider system is not yet able to export with GP Connect. For example, if the consultation contains a link to a referral record, but the provider system does not yet support exporting referrals.

Where a provider system is not able to export a linked clinical item, it will create a section.section.entry (or section.entry) entry with the:

-   `List.entry.item.display` set to “[Clinical area] items are not supported by the provider system.”

       Where [Clinical area] identifies the type of the clinical item that is not supported.

The example below shows references to two items, one for an observation and another for referrals that aren't supported by the provider system:

```json
{
  "item": {
    "reference": "Observation/6734572634"
  }
},
{
  "item": {
    "display": "Referral items are not supported by the provider system"
  }
}
```

## Consultations containing confidential items

Where a Consultation is marked as confidential it will (as per the structured requirements on confidentially) not be included returned data and the Confidential Items warning message will be included in the `List` containing the query response.

Where a Consultation is not marked as confidential but includes items that are marked as confidential or are considered sensitive, the following information is returned:
* the Consultation will be included in the response as normal
* the confidential item(s) will NOT be included in the response
* there will be NO reference to the confidential item(s) in the `List` profiles defining the Consultation structure
* the Confidential Items warning message will be included in the `List` for the relevant type of type data that was omitted (for example, if a piece of uncategorised data was excluded as it was confidential then the warning code would be in the list of uncategorised data that was returned as part of the query) - the warning will NOT be included in the `List` profiles defining the Consultation structure

In effect, there will be a warning message that items were excluded from the response due to confidentiality but there will be no indication from which Consultation(s) they were removed from.

## Draft Consultations

In some GP practice clinical systems, it is possible for the clinician to save a consultation record in a draft (or equivalent) status.

Consultations in this draft status **MUST** be included in the response. `Encounter.Status` is used to identify them as draft.

## Suppression of empty consultations, topics and headings

On some systems all or almost all record entry is captured in the context of a consultation. This, coupled with default behaviours such as starting a consultation on opening a patient record, leads to the phenomenon of 'empty' consultations where the Data/Dr/Place/Type has been created as a default but there is no subsequent entry of any clinical information within the consultation.

Provider systems which allow empty consultations should not return empty consultations in response to consultation queries.

The same approach is followed for empty topic and heading levels recorded at source - that is, these should be suppressed by the producer.

## What information may be recorded outside of consultations

-  some systems do not restrict entry of clinical data to a consultation context - that is, it is possible to record clinical information about a patient without starting or initiating a consultation
-   such 'Non-Consultation' behaviour does not imply any loss of information or structure by the source system - that is, the record items are still fully recorded and attributed
-   but because they are recorded outside of a consultation context, they will not be returned by an API query directed at returning consultation resources (see 'Design decisions' section below)

## Consumer guidance

-   Although the expression of full consultation structure is provided by the specified protocols, it is recognised that many consumers simply want access to the resources referenced by the consultations rather than the topic or SOAP heading structures. Consumers in the category may simply flatten the consultation structure or otherwise extract the resources referenced within the List resources carrying the consultation structure.

## Consumer cautions

-   A consumer making consultation-oriented queries only **MUST NOT** expect to obtain all items in the patient record.
-   Other GP Connect APIs will provide full access to items in the patient record including all medications, all allergies, all problems up to and including get whole record queries.

## Design decisions

-   Systems which allow direct recording of data outside of consultation contexts should not fabricate consultations to return such data when consultation queries are received, as to do so would be generating information and structure which does not exist on the source system, and which would obscure the genuine consultation content that does exist. Systems in this category have clear distinctions between consultations and other types of record content (for example, last X Consultations displayed in patient summaries and to synthesise consultations would distort this native behaviour).

## Using the `List` resource for consultation queries

The results of a query for consultation details **MUST** return a `List` containing references to all the `List` resources at the top consultation level which are identified by the SNOMED code **325851000000107 Consultation encounter type** and represent each consultation that is returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason.code` with the value `no-content-recorded`. In this case, `List.note` **MUST** be populated with the text 'Information not available'.
