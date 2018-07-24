---
title: Access Record HTML
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord.html
summary: "Introduction to the GP Connect Access Record HTML capability."
toc: false
---

## HTML View ##

{% include custominfocallout.html content="**Information:** For Direct Patient Care purposes only, the Primary Care record contains a wealth of useful information which can improve patient safety and efficiency if it is made interoperable (subject to IG and Clinical Safety requirements) across health care settings. <br/><br/>Access Record HTML is delivering the capability to view a patient record and **MUST NOT** be used as a means to store data. <br/><br/> Please refer to [NHS Digital - FAQ on legal access to personal confidential data - Definitions questions - How is Direct Patient Care defined?](http://content.digital.nhs.uk/article/3638/Personal-data-access-FAQs){:target='_blank'} for details of what constitutes direct patient care. " type="danger" %} 


### Purpose ###

In an unstructured and pre-rendered format (HTML), this capability will provide health professionals with access to a patient's primary care record by requesting sections or headings. Where appropriate, a date range can be defined to filter the retrieval of larger sections. These views can be incorporated directly into Electronic Patient Record systems.

Significant effort has already been made to unify the HTML section views from all four principal suppliers but it is expected that this will be an iterative process during development, UAT and FoT.

The content displayed in the HTML views has then been used as a common baseline of available data to guide the structured and coded 'Access Record' approach.


### Scope ###

The information "sections" in scope for care record access are:

1. Summary
2. Encounters
3. Clinical Items
4. Problems and Issues
5. Allergies and Adverse Reactions
6. Medications
7. Referrals
8. Observations
9. Immunisations
10. *Administrative Items*<sup>*</sup>
11. Patient Demographics (minimal)
12. Patient's GP Practice and Organisation (minimal)

{% include customcallout.html content="**Important:** The 'Clinical Items' section exists as it is not currently possible to reliably distinguish procedures, diagnoses, symptoms and other clinically coded items into their own sections due to the way they are stored in the primary care record Principal systems. <br/><br/>Initially some sections of the patient care record (marked above with a <sup>*</sup>) may not initially be available from all primary care record Principal systems. " type="warning" %}

### Use Cases ###

- Extended access GP practices can view all of the patients primary care views even when the record is held on a different GP system.
- Other care settings (e.g. 111, Physio, Community, Emergency, Acute/Secondary, Social) can view the patients GP record (those held by the patients recorded GP practice) to better inform care decisions they may be making for a patient.

### Profiled FHIR Resources ###

Please refer to the [AccessRecord HTML FHIR Resources](datalibraryaccessRecord.html) page for details of the FHIR profiles utilised for the Access Record HTML operation.

### SPINE Interactions ###

The Access Record HTML capability message set includes the following set of spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Get Care Record](accessrecord_use_case_retrieve_a_care_record_section.html) | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord` |
