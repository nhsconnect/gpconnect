---
title: Consumer session illustrated
keywords: getcarerecord, documents
tags: [getcarerecord, documents]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_documents_development_api_session.html
summary: "An illustration of consumer document API session"
---

A GP Connect Document API consumer application would follow the API session below to retrieve a patient's documents.

## Consumer session - querying and retrieving documents ##

The sequence diagram below illustrates which individual API calls are required by a consumer to both query for and retrieve a document from a GP practice in the simplest case. It describes interactions with the provider system at the GP practice, and does not include details of the prerequisite interactions with Spine services.

![Sequence diagram for querying and retrieving documents](images/access_structured/consumer-sessions-interaction.png)


| Step | Description |
|------|-------------|
| 1a   | **Consumer** makes a call to [find patient](foundations_use_case_find_a_patient.html) providing the patient's NHS number|
| 1b   | **Provider** finds patient record and returns the logical identifier of the patient record at this practice in their system.|
| 2a   | **Consumer** [queries for a list of the patient's documents](accessrecord_documents_development_search_patient_documents.html)|
| 2b   | **Provider** responds with a list of document metadata for the patient's documents|
| 2a   | **Consumer** makes a request to [retrieve a patient's document](accessrecord_documents_development_retrieve_patient_documents.html) using the location returned as part of the document metadata in step 2b|
| 2b   | **Provider** responds with the requested document|
