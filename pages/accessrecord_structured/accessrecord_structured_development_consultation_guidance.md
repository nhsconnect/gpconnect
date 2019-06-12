---
title: Consultation
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_consultation_guidance.html
summary: "Guidance for the representation and consumption of Consultations"
---

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

## Logical Structure ##

Consultations follow a common logical structure.

* Context

Each consultation has a set of context information that describes when and where the consultation took place, the patient it covered and who else was involved (such as a doctor).

* Topics

A consultation will be split into one of more topics. Each topic describes an area of discussion (or activity) that took place in the consultation.

A topic may (but not always) be related to a specific problem in the patient’s record. In these cases, all the discussions and activities recorded under that topic are in regards to that problem.

* Headings

A topic may be split into one of more headings (sometimes referred to as SOAP headings). Each heading covers a specific part of the consultation process about that topic.

There is no national standard for headings so they will reflect the headings available in the provider clinical system.

* Clinical Items

Within each heading there may be one or more clinical items. Grouped together these clinical items describe in full the details of the consultation recorded under the heading.

Any type of clinical item may form part of the consultation (medications, allergies, immunisations, uncategorised data, etc). 

* Topics without Headings

A topic can be created without headings. In these cases, the clinical items are recorded directly under the topic the same way they are recording under a heading.

![Consultation Example ](images/access_structured/Consultation_Example.png)  <!-- .element height="50%" width="50%" -->

## Approach ##

![Consultation FHIR Resource Model ](images/access_structured/Consultation_FHIR_Resource_Model.png)
![Consultation FHIR Resource Model ](images/access_structured/Consultatiion_FHIR_Resource_Model.png)

{: .center-image }
![Consultation Structure ](images/access_structured/Consultation_Structure.png)
![Consultation Structure ](images/access_structured/Consultation_Stucture.png)

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

## Consumer Cautions ##

* A consumer making Consultation oriented queries only **must not** expect to obtain all items in the patient record
* Other GP Connect APIs will provide full access to items in the patient record including all medications, all allergies, all problems up to an including get whole record queries.

## Design Decisions ##

* Systems which allow direct recording of data outside of Consultation contexts should not fabricate Consultations to return such data when Consultation queries are received as to do so would be generating information and structure which does not exist on the source system and which would obscure the genuine Consultation content that does exist. Systems in this category have clear distinctions between Consultations and other types of record content e.g. last X Consultations displayed in patient summaries and to synthesise consultations would distort this native behaviour.
