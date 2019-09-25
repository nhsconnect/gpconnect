---
title: Development introduction
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_documents_development.html
summary: "Development overview to the Access Record Documents capability"
---

## Introduction ##

The Access Record Documents capability provides the ability to retrieve unstructured documents from a patient's GP.

## FHIR&reg; resources ##

The [FHIR resources](accessrecord_documents_development_resources_overview.html) pages provide a detailed reference on population and consumption of the FHIR profiled resources used in this capability.

## FHIR&reg; examples ##

The following pages provide example request and response messages:

- [Query documents](accessrecord_documents_development_fhir_examples_documents.html)
- [Retrieve documents](accessrecord_documents_development_fhir_examples_documents.html)

## API definition

The following API definitions are included in this capability:

- [Query documents](accessrecord_documents_development_search_patient_documents)
- [Retrieve documents](accessrecord_documents_development_retrieve_patient_documents.html)

## Spine interactions ##

The Access Record Structured capability message set includes the following set of Spine interactions:

| Operation                 | InteractionID             |
|---------------------------|---------------------------|
| [Search for documents](accessrecord_documents_development_retrieve_patient_documents.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:search:documentreference-1` |
| [Retrieve documents](accessrecord_documents_development_search_patient_documents.html)          | `urn:nhs:names:services:gpconnect-documents:fhir:rest:read:binary-1` |
