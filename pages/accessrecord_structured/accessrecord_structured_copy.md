---
title: Access Record Structured
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_copy.html
summary: "Introduction to the Access Record Structured capability"
---

## Overview ##

The Access Record Structured capability enables an NHS system to request and consume a patient’s GP record in a structured and coded format that is machine readable. 

## Purpose ##

The Access Record Structured capability enables the patient data to be made available via a standard API. Structured data allows the consuming system to import and process the patient data in whatever way it requires to best support patients and the healthcare professionals treating them. GP Connect does not place any specific restrictions on how the data is processed so long as the data is only used for the direct care of the patient and the system meets the specified GP Connect consumer requirements (including information governance and clinical safety standards).

## Problem Statement ##
To Do
## Scope ##

The Access Record Structured capability will expose data for a number of clinical areas. The initial release supports:

1. Medications
2. Allergies

{% include roadmap.html content="Subsequent releases are to be scoped" %}

## Example scenarios ##

 - A healthcare professional views a patient’s GP record during a clinical appointment. By sending the clinical data in a structured format the local system can reformat and present the data in a way that best supports the local clinician.
 - A patient is admitted into an acute hospital trust. As part of admission a full set of the patient’s current medication and allergy information is retrieved from the patient’s GP record and imported into the hospital system. By sending the clinical data in a structured format the local system can import the data, reducing the level of data entry required by the local clinician.
 - During the triage of a patient using a decision support tool the local system imports the patient’s clinical information from their GP record. The data is received in a structured format that allows the system to import the data and use it to support the triage process.  

## Versioning ##

To Do
