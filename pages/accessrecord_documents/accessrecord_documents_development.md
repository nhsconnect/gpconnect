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
| [Read metadata](foundations_use_case_get_the_fhir_capability_statement.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:read:metadata-1` |
| [Read patient](foundations_use_case_read_a_patient.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:read:patient-1` |
| [Patient search](foundations_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:search:patient-1` |
| [Read practitioner](foundations_use_case_read_a_practitioner.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:read:practitioner-1` |
| [Practitioner search](foundations_use_case_find_a_practitioner.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:search:practitioner-1` |
| [Read organisation](foundations_use_case_read_an_organisation.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:read:organization-1` |
| [Organisation search](foundations_use_case_find_an_organisation.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:search:organization-1` |
| [Read location](foundations_use_case_read_a_location.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:read:location-1` |
| [Search for documents](accessrecord_documents_development_retrieve_patient_documents.html) | `urn:nhs:names:services:gpconnect-documents:fhir:rest:search:documentreference-1` |
| [Retrieve documents](accessrecord_documents_development_search_patient_documents.html)          | `urn:nhs:names:services:gpconnect-documents:fhir:rest:read:binary-1` |
