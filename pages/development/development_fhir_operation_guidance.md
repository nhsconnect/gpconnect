---
title: Operation guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_operation_guidance.html
summary: "Details of which operations a FHIR&reg; server should expose to be a fully compliant GP Connect solution"
---

## FHIR&reg; operations ##

*Mechanism*

- RESTful APIs in line with the FHIR&reg; standard (with limited/targeted usage of custom operations as/if required)

*Interactions*

All `InteractionIDs` are expected to follow the following format `urn:nhs:names:services:[program]:[standard]:[mechanism]:[operation]:[subject]`.

- program = `gpconnect`
- standard = `fhir`
- mechanism = [ `rest`, `operation` ]
	- `rest` for RESTful API interactions
	- `operation` for custom Operation API interactions
- operation
	- RESTful style API = [ `create`, `read`, `update`, `delete`, `search` ] + any more specific actions (for example, `cancel`)
	- Remote Procedure Call (RPC) style API = [ `gpc.getcarerecord`, `gpc.registerpatient` ]
- subject = [ `resourceType`, `operationName` ]
	- Resource Type is the name of a FHIR resource, such as `Patient`, `Appointment`, `Organization`
	- Operation Name is the name of a custom FHIR operation, such as `gpc.getcarerecord`

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

