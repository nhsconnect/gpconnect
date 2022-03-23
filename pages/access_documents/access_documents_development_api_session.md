---
title: Consumer session illustrated
keywords: getcarerecord, documents
tags: [getcarerecord, documents]
sidebar: access_documents_sidebar
permalink: access_documents_development_api_session.html
summary: "An illustration of consumer document API sessions"
---

A GP Connect Access Document consumer application would follow the typical API session described below to retrieve a patient's documents.

## Consumer session - querying and retrieving documents ##

The sequence diagram below illustrates which individual API calls are required by a consumer to both query for and retrieve a document from a GP practice in the simplest case. It describes interactions with the provider system at the GP practice, and does not include details of the prerequisite interactions with Spine services.

![Sequence diagram for querying and retrieving documents](images/access_documents/consumer-sessions-interaction.png)


| Step | Description |
|------|-------------|
| 1a   | **Consumer** makes a call to [find patient](access_documents_use_case_find_a_patient.html) providing the patient's NHS number|
| 1b   | **Provider** finds patient record and returns the logical identifier of the patient record at this practice in their system.|
| 2a   | **Consumer** [queries for a list of the patient's documents](access_documents_development_search_patient_documents.html)|
| 2b   | **Provider** responds with a list of document metadata for the patient's documents|
| 2a   | **Consumer** makes a request to [retrieve a document](access_documents_development_retrieve_patient_documents.html) using the location returned as part of the document metadata in step 2b|
| 2b   | **Provider** responds with the requested document|

## Consumer session - retrieving documents referenced from patient's structured record

The sequence diagram below illustrates how a consumer could retrieve the patient's structured record using Access Record Structured and then retrieve documents referenced from consultations or problems using the Access Document API.

![Sequence diagram for querying and retrieving documents](images/access_documents/consumer-sessions-interaction-structured.png)

| Step | Description |
|------|-------------|
| 1a   | **Consumer** makes a call to [retrieve the patient's structured record](accessrecord_structured_development_retrieve_patient_record.html) providing the patient's NHS number and parameters relating to the clinical information that should be returned|
| 1b   | **Provider** finds patient record and returns the patient's structured record including document metadata.|
| 2a   | **Consumer** makes a request to [retrieve a document](access_documents_development_retrieve_patient_documents.html) using the location returned as part of the document metadata in step 1b|
| 2b   | **Provider** responds with the requested document|
