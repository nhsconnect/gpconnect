---
title: Operation guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_operation_guidance.html
summary: "Details of which operations a FHIR server should expose to be a fully compliant GP Connect solution"
---

## FHIR Operations ##

*Aim(s)*

- Appointment Management

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
| [Read Metadata](foundations_use_case_get_the_fhir_capability_statement.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata-1` | `GET`  | `[base]/metadata` |
| [Read Patient](foundations_use_case_read_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient-1` | `GET`  | `[base]/Patient/[id]` |
| [Patient Search](foundations_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient-1` | `GET`  | <code>[base]/Patient?identifier=https://fhir.nhs.uk/Id/nhs-number&#124;[nhsNumber]</code> |
| [Read Practitioner](foundations_use_case_read_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:practitioner-1` | `GET`  | `[base]/Practitioner/[id]` |
| [Practitioner Search](foundations_use_case_find_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:practitioner-1` | `GET`  | <code>[base]/Practitioner?identifier=https://fhir.nhs.uk/Id/sds-user-id&#124;[sdsUserID]</code> |
| [Read Organisation](foundations_use_case_read_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:organization-1` | `GET`  | `[base]/Organization/[id]` |
| [Organisation Search](foundations_use_case_find_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization-1` | `GET`  | <code>[base]/Organization?identifier=https://fhir.nhs.uk/Id/ods-organization-code&#124;[odsCode]</code> |
| [Read Location](foundations_use_case_read_a_location.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:location-1` | `GET`  | `[base]/Location/[id]` |
| [Register Patient](foundations_use_case_register_a_patient.html)          | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient-1` | `POST`  | `[base]/Patient/$gpc.registerpatient` |


### Appointments capability interactions ###

| Operation                 | InteractionID             | Http Verb | Example URL Pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Search for free slots](appointments_use_case_search_for_free_slots.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot-1` | `POST` | `[base]/Slot` |
| [Read Appointment](appointments_use_case_read_an_appointment.html)          | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment-1` | `GET`  | `[base]/Appointment/[id]` |
| [Create Appointment](appointments_use_case_book_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment-1` | `POST` | `[base]/Appointment` |
| [Amend Appointment](appointments_use_case_amend_an_appointment.html)         | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment-1` | `PUT`  | `[base]/Appointment/[id]` |
| [Cancel Appointment](appointments_use_case_cancel_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:cancel:appointment-1` | `PUT`  | `[base]/Appointment/[id]` |
| [Get Patient Appointments](appointments_use_case_retrieve_a_patients_appointments.html)  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments-1` | `GET`  | `[base]/Patient/[id]/Appointment` |

### Access Record HTML capability interactions ###

Access Record HTML interactions are not available at this specification version.

### Access Record Structured capability interactions ###

Access Record Structured interactions are not available at this specification version.

### Task capability interactions ###

Task interactions are not available at this specification version.

