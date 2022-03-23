---
title: Access Record HTML
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord.html
summary: "Introduction to the GP Connect Access Record HTML capability"
toc: false
---

<a href="#" class="back-to-top">Back to Top</a>

## HTML view ##

{% include custominfocallout.html content="<strong>Information:</strong> For Direct Patient Care purposes only, the Primary Care record contains a wealth of useful information which can improve patient safety and efficiency if it is made interoperable across health care settings (subject to [IG](designprinciples_ig_principles.html) and [Clinical Safety](designprinciples_clinical_safety_principles.html) requirements which consumers **MUST** meet and confirm compliance with during assurance). <br/><br/>Access Record HTML is delivering the capability to view a patient record and **MUST** be used in real time for read only. <br/><br/> Please refer to [NHS Digital - FAQ on legal access to personal confidential data - Definitions questions - How is Direct Patient Care defined?](http://content.digital.nhs.uk/article/3638/Personal-data-access-FAQs){:target='_blank'} for details of what constitutes direct patient care. " type="danger" %} 


### Purpose ###

In an unstructured and pre-rendered format (HTML), this capability will provide health professionals with access to a patient's primary care record by requesting sections or headings. Where appropriate, a date range can be defined to filter the retrieval of larger sections. These views can be incorporated directly into Electronic Patient Record systems.

The content displayed in the HTML views has then been used as a common baseline of available data to guide the structured and coded 'Access Record' approach.

Significant effort has already been made to unify the HTML section views from all four principal suppliers but it is expected that this will be an iterative process during development, UAT and FoT.


### Scope ###

The information sections in scope for care record access are:

1. [Summary](accessrecord_view_summary.html)
2. [Encounters](accessrecord_view_encounters.html)
3. [Clinical items](accessrecord_view_clinical_items.html)
4. [Problems and issues](accessrecord_view_problems.html)
5. [Allergies and adverse reactions](accessrecord_view_allergies.html)
6. [Medications](accessrecord_view_medications.html)
7. [Referrals](accessrecord_view_referrals.html)
8. [Observations](accessrecord_view_observations.html)
9. [Immunisations](accessrecord_view_immunisations.html)
10. *[Administrative items](accessrecord_view_administrative_items.html)*<sup>*</sup>

{% include customcallout.html content="**Note:** sections of the patient care record (marked above with a <sup>*</sup>) may not initially be available from all primary care record Principal systems. " type="info" %}

### Use cases ###

- extended access GP practices can view all of the patient's primary care views even when the record is held on a different GP system
- other care settings (e.g. 111, Physio, Community, Emergency, Acute/Secondary, Social) can view the patient's GP record (those held by the patient's recorded GP practice) to better inform care decisions they may be making for a patient

### Profiled FHIR resources ###

Please refer to the [AccessRecord HTML FHIR Resources](datalibraryaccessRecord.html) page for details of the FHIR profiles utilised for the Access Record HTML operation.

### Spine Interactions ###

The Access Record HTML capability message set includes the following set of Spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
| [Get Care Record](accessrecord_use_case_retrieve_a_care_record_section.html) | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord` |
