---
title: Interaction IDs
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: integration_interaction_ids.html
summary: "A list of GP Connect API interaction IDs"
---

## GP Connect Interaction ID naming policy ##

All interaction IDs are expected to follow the following format `urn:nhs:names:services:[programme]:[capability]:[standard]:[mechanism]:[operation]:[subject]`

- Programme = `gpconnect`
- Capability = [ `documents` ]
- Standard = `fhir`
- Mechanism = [ `rest`, `operation` ]
	- `rest` for RESTful API interactions
	- `operation` for custom Operation API interactions
- Operation
	- RESTful style = [ `create`, `read`, `update`, `delete`, `search` ] + any more specific actions (for example, `cancel`)
	- Extended operation = [ `gpc.getcarerecord`, `gpc.registerpatient` ]
- Subject = [ `resourceType`, `operationName` ]
	- Resource Type is the name of a FHIR resource, such as `Patient`, `Appointment`, `Organization`
	- Operation Name is the name of a extended operation, such as `gpc.getcarerecord`

## List of Interaction IDs ##

| Operation                 | InteractionID             |
|---------------------------|---------------------------|
| [Read metadata](foundations_use_case_get_the_fhir_capability_statement.html) | `urn:nhs:names:services:gpconnect:documents:fhir:rest:read:metadata-1` |
| [Patient search](foundations_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect:documents:fhir:rest:search:patient-1` |
| [Search for documents](accessrecord_documents_development_retrieve_patient_documents.html) | `urn:nhs:names:services:gpconnect:documents:fhir:rest:search:documentreference-1` |
| [Retrieve documents](accessrecord_documents_development_search_patient_documents.html)          | `urn:nhs:names:services:gpconnect:documents:fhir:rest:read:binary-1` |
