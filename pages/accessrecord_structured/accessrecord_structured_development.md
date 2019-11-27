---
title: Development introduction
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development.html
summary: "Development overview to the Access Record Structured capability"
---

## Introduction ##

The Access Record Structured capability provides the ability to retrieve data from a patient's GP record in a structured and coded format. In order to do this safely and effectively, we need to consider how GP systems store data about patients, how it is categorised/structured and how the context in which the data is entered by or displayed to the user may influence its meaning.

## Record structure in GP clinical systems

There are several GP clinical systems in use in England and, although there are many differences in functionality, there are many categorisations that are common across most/all of the different systems. In GP Connect we have called these categorisations 'clinical areas' and have treated each one as a separate group of data that can be retrieved by the API.

For each of these clinical areas in GP systems, there is usually a separate screen or module for entering and viewing data. However, it is normal that there are a number of different ways for a user to view data that has been entered. It is common, for instance, to view an allergy in a separate allergy screen, in a view of a consultation, in a date-ordered screen containing all clinical items often called a journal or care history screen or in a screen that is a one-page summary of the patient record.

Defining all the clinical data areas within a patient record has enabled GP Connect Access Record Structured to more clearly define the scope of the project. It will also help providers and consumers to understand how we intend to make available the whole record and how far we are through that journey in any given release.

## Representing the different clinical areas

We have defined a data model for the whole GP record that we are working through a clinical area at a time. This is illustrated in the diagram below:

<a href="images/access_structured/GP_Record_Clinical_Areas_Overview_v2.png"><img src="images/access_structured/GP_Record_Clinical_Areas_Overview_v2.png" alt="Logical Model" style="max-width:100%;max-height:100%;"></a>

In the diagram each of the boxes with a blue outline represents a clinical area. These each contain 1 or more boxes representing FHIR&reg; resources. The FHIR resource boxes are colour coded:

* Green - are resources that were defined for use in GP Connect in a previous version of the specification
* Orange - are resources that are defined for the first time for use in GP Connect in this version
* Blue - are resources that have yet to have their GP Connect usage defined

The clinical areas that are contained in the larger box on the right-hand side, labelled 'Clinical Item', are the clinical areas in which pieces of clinical information are held. The clinical areas on the left of the diagram will be used to model the way the clinical items are viewed, organised and managed in GP systems. The aim being that data can be reproduced in consumer interfaces in a way that maintains the context of the data and most accurately communicates the meaning that was intended by the clinician who created it.

## Linkages

It is also apparent in the diagram that many of the resources are linked together. Details of how these linkages exist and will be managed can be found on the linkages page.

- [Linkages](accessrecord_structured_development_linkages.html)

## Clinical areas

The following pages describe each of the clinical areas in more detail and are followed by pages explaining how to populate the related resources and giving worked examples in FHIR.

- [Allergies guidance](accessrecord_structured_development_allergies_guidance.html)
- [Medication resource relationships](accessrecord_structured_development_medication_resource_relationships.html)
- [Medication guidance](accessrecord_structured_development_medication_guidance.html)
- [Immunization guidance](accessrecord_structured_development_immunization_guidance.html)
- [Uncategorised data guidance](accessrecord_structured_development_uncategorisedData_guidance.html)
- [Consultation guidance](accessrecord_structured_development_consultation_guidance.html)
- [Problem guidance](accessrecord_structured_development_problems_guidance.html)
- [Investigations guidance](accessrecord_structured_development_pathology_guidance.html)
- [Referrals guidance](accessrecord_structured_development_referralrequest_guidance.html)
- [Diary Entries guidance](accessrecord_structured_development_diaryentry_guidance.html)

{% include note.html content="The Access Document capability is available in its own GP Connect specification version. 
Access Document complements Access Record Structure by retrieval of a documents list or individual documents.
Please consult the [specification versions page](https://developer.nhs.uk/gp-connect-specification-versions/) for more details." %}
