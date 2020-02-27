---
title: Access Document introduction
keywords: structured design
tags: [design,structured]
sidebar: access_documents_sidebar
permalink: access_documents.html
summary: "Introduction to the Access Document capability"
---

## Introduction ##

The Access Document capability provides the ability to retrieve unstructured documents from a patient's registered GP practice.

## FHIR&reg; resources ##

The [FHIR resources](access_documents_development_resources_overview.html) pages provide a detailed reference on population and consumption of the FHIR profiled resources used in this capability.

## API definition

The following API definitions are included in this capability:

- [Search for a patient's documents](access_documents_development_search_patient_documents)
- [Retrieve a document](access_documents_development_retrieve_patient_documents.html)

## Spine interactions ##

The Access Document capability message set includes the following set of Spine interactions:

| Operation                 | InteractionID             |
|---------------------------|---------------------------|
| [Read metadata (Access Document)](access_documents_use_case_get_the_fhir_capability_statement.html) | `urn:nhs:names:services:gpconnect:documents:fhir:rest:read:metadata-1` |
| [Patient search (Access Document)](access_documents_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect:documents:fhir:rest:search:patient-1` |
| [Search for documents](access_documents_development_retrieve_patient_documents.html) | `urn:nhs:names:services:gpconnect:documents:fhir:rest:search:documentreference-1` |
| [Retrieve document](access_documents_development_search_patient_documents.html)          | `urn:nhs:names:services:gpconnect:documents:fhir:rest:read:binary-1` |
