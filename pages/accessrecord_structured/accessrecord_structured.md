---
title: Introduction
keywords: getcarerecord, structured
tags: [getcarerecord, structured] 
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured.html
summary: "Introduction to the Access Record Structured capability"
---

## Purpose ##

To meet strategic objectives to enable greater collaboration and sharing of information through IT system interoperability across health and care systems, the Access Record Structured capability enables a system to consume a patient’s GP record in a machine-readable format, removing the need to transcribe information from one system to another. The API will build upon the foundations of the Access Record HTML capability, which provides access to the patient’s GP record in a human-readable HTML format. 

## Scope ##

The Access Record Structured capability will expose data for a number of clinical areas. The initial release supports:

1. Medications
2. Allergies

{% include roadmap.html content="Subsequent releases are to be scoped" %}

## Example scenarios ##

 - A healthcare professional views a patient’s GP record during a clinical appointment. By sending the clinical data in a structured format the local system can reformat and present the data in a way that best supports the local clinician.
 - A patient is admitted into an acute hospital trust. As part of admission a full set of the patient’s current medication and allergy information is retrieved from the patient’s GP record and imported into the hospital system. By sending the clinical data in a structured format the local system can import the data, reducing the level of data entry required by the local clinician. 
 - During the triage of a patient using a decision support tool the local system imports the patient’s clinical information from their GP record. The data is received in a structured format that allows the system to import the data and use it to support the triage process.  

## API use cases ##

The following API use cases are included in this capability:

- [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html)

## Profiled FHIR resources ##

See the [FHIR resources](accessrecord_structured_development_resources_list.html) page for details of the FHIR profiles used in this capability.

## Spine interactions ##

The Access Record Structured capability message set includes the following set of Spine interactions:

| Operation                 | Interaction ID            | 
|---------------------------|---------------------------| 
| [Get Structured Record](accessrecord_structured_development_retrieve_patient_record.html) | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getstructuredrecord-1` |




