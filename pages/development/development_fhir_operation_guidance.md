---
title: Operation guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_operation_guidance.html
summary: "Details of which operations a FHIR server should expose to be a fully compliant GP Connect solution."
---

## FHIR operations ##

*Aim(s)*

- Access Record views

*Mechanism*

- RESTful APIs in-line with the FHIR&reg; standard (with limited/targeted usage of custom operations as/if required).

*Interactions*

All `InteractionIDs` are expected to follow the following format `urn:nhs:names:services:[program]:[standard]:[mechanism]:[operation]:[subject]`.

- Program = `gpconnect`
- Standard = `fhir`
- Mechanism = [ `rest`, `operation` ]
	- `rest` for RESTful API Interactions.
	- `operation` for custom Operation API Interactions.
- Operation
	- RESTful syle API = [ `create`, `read`, `update`, `delete`, `search` ] + any more specific actions (i.e. `cancel`).
	- RPC style API = [ `gpc.getcarerecord`, `gpc.registerpatient` ]
- Subject = [ `resourceType`, `operationName` ]
	- Resource Type is the name of a FHIR resource (i.e. `Patient`, `Appointment`, `Organization` etc).
	- Operation Name is the name of a custom FHIR operation (i.e. `gpc.getcarerecord`)

### Foundations capability interactions ###

| Operation                 | InteractionID             | Http Verb | Example URL Pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Read Metadata](foundations_use_case_get_the_fhir_conformance_profile.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata` | `GET`  | `[base]/metadata` |

The remaining interactions of the Foundations capability pack are not available at this specification version.

### Access Record HTML capability interactions ###

| Operation                 | InteractionID             | Http Verb | Example URL Pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Get Care Record](accessrecord_use_case_retrieve_a_care_record_section.html) | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord` | `POST` | `[base]/Patient/$gpc.getcarerecord` |

### Access Record Structured capability interactions ###

Access Record Structured interactions are not available at this specification version.

### Appointments capability interactions ###

Appointments interactions are not available at this specification version.

### Task capability interactions ###

Task interactions are not available at this specification version.

