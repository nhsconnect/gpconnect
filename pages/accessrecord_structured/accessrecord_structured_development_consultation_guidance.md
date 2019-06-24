---
title: Consultation
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_consultation_guidance.html
summary: "Guidance for the representation and consumption of Consultations"
---

## Introduction

Consultations are one of the most important forms in which structured clinical information is recorded in the patient records within GP systems.

However there is no standard structure or format for recording Consultations that is common across all systems. 

This presents a challenge in developing a common set of FHIR profiles that are capable of representing the Consultation structures that exist within participating systems.

It is also a challenge for Producer systems in expressing native Consultations in a standardised form as well as being a challenge for Consumers in understanding those structures.

It is important to define what we mean by Consultation. Not all clinical information is recorded consistently across systems within structures that can be classed as Consultations therefore it is important to note that a Consultation oriented query alone may not return all of the clinical information held within a patient record.

This document is designed to address these challenges.

-   It provides a clear definition of what is meant by Consultation in the context of the current set of participating Producer systems.
-   It identifies the limitations of Consultation based queries in isolation as a method for retrieving all elements of patient records.
-   It describes the set of Consultation structures available in producer systems and guidance for populating the FHIR resources required to represent these structures in a consistent manner that is processable ny consumers.
-   It provides guidance for consumer systems processing the FHIR resources representing Consultation structures on source systems as to the variances between representations and the correct handling of these structures.

## What is a Consultation ?

A Consultation is the structure within which source systems group one or more clinical record entries which occurred at the same time and for the same or similar purpose attributed to or asserted by the same actor.

-   Consultations do not exclusively represent Clinician-Patient encounters although they are commonly used for that purpose.
-   Consultations may record purely administrative or communications triggered events on source systems e.g. repeat medication administration, a pathology report filed into the patient record via messaging workflow. 
-   Consultations are generally assigned and attributed to what can loosely be termed a  'Date/Doctor/Place/Type' (Encounter), although these attributes may be overridden or refined in the context of individual record entries within the Consultation.
-   Consultations may or may not have associated structure e.g. the ability to decompose a Consultation into multiple topics/subjects/problems and within each 'topic' further group clinical content under headings (SOAP headings) in line with long standing clinical note taking practice ()
-   Consultations may also be recorded in non-structured form i.e. a grouping of clinical record entries under the same 'Date/Dr/Place/Type' but without additional structure (topics or SOAP headings)
-   Consultations may incorporate a range of different record entries e.g. measurements, test results, textual narrative, structured narrative, coded observations, medications. 

## Logical Structure

Consultations follow a common logical structure.

-   Context

    Each Consultation has a set of context information that describes when and where the Consultation took place, the patient it covered and who else was involved (such as a doctor).

-   Topics

    A Consultation will be split into one of more topics. Each topic describes an area of discussion (or activity) that took place in the Consultation.

    A topic may (but not always) be related to a specific problem in the patient’s record. In these cases, all the discussions and activities recorded under that topic are in regards to that problem.

-   Headings

    A topic may be split into one of more headings (sometimes referred to as SOAP headings). Each heading covers a specific part of the Consultation process about that topic.

    There is no national standard for headings so they will reflect the headings available in the provider clinical system.

-   Clinical Items

    Within each heading there may be one or more clinical items. Grouped together and in order these clinical items describe in full all the details recorded under that heading of the Consultation.

    Any type of clinical item may form part of the Consultation (medications, allergies, immunisations, uncategorised data, etc). 

-   Topics without Headings

    A topic can be created without headings. In these cases, the clinical items are recorded directly under the topic the same way they are recording under a heading.

## Approach

![Consultation FHIR Resource Model ](images/access_structured/Consultation_FHIR_Resource_Model.png)

![Consultation Structure ](images/access_structured/Consultation_Stucture.png)

-   The Encounter resource and related resources like Location are adopted to provide the Consultation context (Date/Doctor/Type/Place)
-   List resources are adopted to provide Consultation structure. A top level List is utilised to represent the Consultation structure as a whole. The Consultation List references further List resources representing the Topic levels and in turn these reference List resource representing the SOAP heading levels. 
-   Some systems allow the recording of Consultation content outside of the Topic/Problem and Heading hierarchy i.e. a flat structure of record entries organised with the same 'Date/Dr/Place' context. These structures are handled by the generation of an Topic List to contain the record entries and entries are referenced directly from that section with no additional Heading subsections.

## Consultation Notes

Consultation notes are the human readable version of the clinical information recorded under each heading. They may or may not be accompanied by a clinically coded version of the information.

There are two primary ways that Consultation notes are recorded on native GP systems:

-   Consultation notes for a heading are recorded as a single piece of free text. Any clinical coded information under the same heading is associated to that text as a whole.

<IMG src="images/access_structured/Consultation_text_1a.png" alt="Free text with multiple clinical codes"  style="max-width:100%;max-height:100%;">

-   Consultation notes for a heading are recorded as a collection of observations, each with a clinical code and or text. When read together in order they produce the Consultation notes.
    Note – this may be entering free text format dynamically identifying codes or through forms where there are specific fields for codes and free text.

<center>
<IMG src="images/access_structured/Consultation_text_1b.png" alt="Clinical code and text"  style="max-width:35%;max-height:35%;">
</center>

 

When reflecting these in FHIR it is important they these two methods are represented in a way that retains the structural information they contain, does not create any unintended clinical meaning and can be viewed / imported. This is done by taking any free text in model one and representing it as unstructured data and positioning it as the first clinical item under the heading. 

<IMG src="images/access_structured/Consultation_text_2.png" alt="Consultation text in FHIR"  style="max-width:100%;max-height:100%;">

 

While there are difference between the two outputs, the Consultation notes can be derived from both by reading through each clinical item in order and merging the Term Text, Clinical Code, Values and Comment into a single narrative.

<IMG src="images/access_structured/Consultation_text_3.png" alt="Reconstituted Consultation Text"  style="max-width:100%;max-height:100%;">

## Example

<IMG src="images/access_structured/Consultation Example_V5.png" alt="Sequence diagram for retrieving a patient record"  style="max-width:100%;max-height:100%;">

*THe display of Snomed CT codes in the examples is for clarity only, it does not apply that Snomed CT codes would be directly expressed as text or displayed as text by receiving systems*

## Consultations containing unsupported clinical items

Depending on the GP Connect version supported by the provider system it can be possible for the Consultation to link to a clinical item that the provider system is not yet able to export with GP Connect. For example, if the Consultation contains a link to a referral record but the provider system does not yet support exporting referrals.

Where a provider system is not able to export a linked clinical item it will create a section.section.entry (or section.entry) entry with the:

-   Reference.Identifier set to null; and
-   Reference.Display set to “Clinical item not supported by the provider system.”

## Suppression of Empty Consultations, Topics and Headings

On some systems all or almost all record entry is captured in the context of a Consultation, this coupled with default behaviours such as starting a Consultation on opening a p\[atient record, leads to the phenomenon of 'empty' Consultations where the Data/Dr/Place/Type has been created as a default but there is no subsequent entry of any clinical information within the Consultation.

Producer systems which allow empty Consultations should not return empty Consultations in response to Consultation queries.

The same approach is followed for empty Topic and Heading levels recorded at source i.e. these should be suppressed by the producer.

## What Information May Be Recorded Outside of Consultations

-   Some systems do not restrict entry of clinical data to a Consultation context i.e. it is possible to record clinical information about a patient without starting or initiating a Consultation. 
-   Such 'Non Consultation' behaviour does not imply any loss of information or structure by the source system i.e. the record items are still fully recorded and attributed
-   But because they are recorded outside of a Consultation context they will not be returned by an API query directed at returning Consultation resorces (See Design Decisions Sections).

## Consumer Guidance

-   Although the expression of full Consultation structure is provided by the specified protocols, it is recognised that many consumers simply want access to the resources referenced by the Consultations rather than the Topic or SOAP heading structures. Consumers in the category may simply flatten the Consultation structure or otherwise extract the resources referenced within the List resources carrying the Consultation structure.

## Consumer Cautions

-   A consumer making Consultation oriented queries only **must not** expect to obtain all items in the patient record
-   Other GP Connect APIs will provide full access to items in the patient record including all medications, all allergies, all problems up to an including get whole record queries.

## Design Decisions

-   Systems which allow direct recording of data outside of Consultation contexts should not fabricate Consultations to return such data when Consultation queries are received as to do so would be generating information and structure which does not exist on the source system and which would obscure the genuine Consultation content that does exist. Systems in this category have clear distinctions between Consultations and other types of record content e.g. last X Consultations displayed in patient summaries and to synthesise Consultations would distort this native behaviour.
          
