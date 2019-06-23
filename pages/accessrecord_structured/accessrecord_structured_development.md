---
title: Development introduction
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development.html
summary: "Development overview to the Access Record Structured capability"
---

## Introduction ##

The access record structured capability provides the ability to retrieve data from a patient's GP record in a structured and coded format. In order to do this safely and effectively we need to consider how GP systems store data about patients, how it is categorised/structured and how the context in which the data is entered by or displayed to the user may influence it's meaning.

## Record structure in GP clinical systems

There are several GP clinical systems in use in England and although there are many differences in functionality there are many categorisations that are common across most/all of the different systems. In GP Connect we have called these categorisations 'clinical areas' and have treated each one as a separate group of data that can be retrieved by the API. 

For each of these clinical areas in GP systems there is usually a separate screen or module for entering and viewing data. However it is normal that there are a number of different ways for a user to view data that has been entered. It is common for instance to view an allergy in a separate allergy screen, in a view of a consultation, in a date ordered screen containing all clinical items often called a journal or care history screen or in a screen that is a one page summary of the patient record.

Defining all the clinical data areas within a patient record has enabled GP Connect access structured record to more clearly define the scope of the project. It will also help providers and consumers to understand how we intend to make available the whole record and how far we are through that journey in any given release.

## Representing the different clinical areas

We have defined a data model for the whole GP record that we are working through a clinical area at a time. This is iluustrated in the diagram below,

![Logical model ](images/access_structured/GP Record - clinical areas overview.png)

In the diagram each of the boxes with a blue outline represents a clinical area, these each contain 1 or more boxes representing FHIR resources. The FHIR resource boxes are colour coded,

* Green - are resources that were definied for use in GP COnnect in a previous version of the specification
* Yellow - are resources that are defined for the first time for use in GP Connect
* Blue - are resources that have yet to have their GP Connect usage defined

The clinical areas that are contained in the larger box on the right hand side, labeled clinical item, are the clinical areas in which pieces of clinical information are held. The clinical areas on the left of the diagram will be used to model the way the clincal items are viewed, organised and managed in GP systems. The aim being that data can be reproduced in consumer interfaces in a way that maintains the context of the data and most acurately communicates the meaning that was intended by the clinician that created it.

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
- [Consultation guidance](accessrecord_structured_development_consultation_guidance.html
- [Problem guidance](accessrecord_structured_development_problems_guidance.html

## Get whole record - dealing with placeholders

Currently as it has not been specified how to represent all areas of the record it is necessary to use placeholders to represent items that are present in the record but there is no mechanism to transport.

Need to finish this section...speak to Matt.



# Below here is old stuff to remove....

The capability consists of a single API operation for retrieving a patient's structured record which is listed below in [API definition](accessrecord_structured_development.html#api-definition).


## FHIR&reg; resources ##

The [FHIR resources](accessrecord_structured_development_resources_overview.html) pages provide a detailed reference on population and consumption of the FHIR profiled resources used in this capability.

## FHIR&reg; examples ##

The following pages provide example request and response messages:

- [Allergies](accessrecord_structured_development_fhir_examples_allergies.html)
- [Medication](accessrecord_structured_development_fhir_examples_medication.html)

## API definition

The following API definitions are included in this capability:

- [Retrieve a patient’s structured record](accessrecord_structured_development_retrieve_patient_record.html)

## Spine interactions ##

The Access Record Structured capability message set includes the following set of Spine interactions:

| Operation                 | Interaction ID            |
|---------------------------|---------------------------|
| [Get Structured Record](accessrecord_structured_development_retrieve_patient_record.html) | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getstructuredrecord-1` |
