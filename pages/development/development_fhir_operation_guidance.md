---
title: Operation guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_operation_guidance.html
summary: "Details of which operations a FHIR&reg; server should expose to be a fully compliant GP Connect solution"
---

## Stage 1 and 2 FHIR&reg; operations ##

*Aim(s)*

- HTML Access Record views (with bundled Structured).
- Appointment and Task management.

*Mechanism*

- RESTful APIs in line with the FHIR&reg; standard (with limited/targeted usage of custom operations as/if required).

*Interactions*

All `InteractionIDs` are expected to follow the following format `urn:nhs:names:services:[program]:[standard]:[mechanism]:[operation]:[subject]`.

- Program = `gpconnect`
- Standard = `fhir`
- Mechanism = [ `rest`, `operation` ]
	- `rest` for RESTful API interactions
	- `operation` for custom Operation API interactions
- Operation
	- RESTful style API = [ `create`, `read`, `update`, `delete`, `search` ] + any more specific actions (for example, `cancel`)
	- Remote Procedure Call (RPC) style API = [ `gpc.getcarerecord`, `gpc.registerpatient` ]
- Subject = [ `resourceType`, `operationName` ]
	- Resource Type is the name of a FHIR resource, such as `Patient`, `Appointment`, `Organization`
	- Operation Name is the name of a custom FHIR operation, such as `gpc.getcarerecord`

### Foundations capability interactions ###

| Operation                 | InteractionID             | HTTP verb | Example URL pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Read metadata](foundations_use_case_get_the_fhir_capability_statement.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata-1` | `GET`  | `[base]/metadata` |
| [Read patient](foundations_use_case_read_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient` | `GET`  | `[base]/Patient/[id]` |
| [Patient search](foundations_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient` | `GET`  | <code>[base]/Patient?identifier=https://fhir.nhs.uk/Id/nhs-number&#124;[nhsNumber]</code> |
| [Read practitioner](foundations_use_case_read_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:practitioner` | `GET`  | `[base]/Practitioner/[id]` |
| [Practitioner search](foundations_use_case_find_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:practitioner` | `GET`  | <code>[base]/Practitioner?identifier=https://fhir.nhs.uk/Id/sds-user-id&#124;[sdsUserID]</code> |
| [Read organisation](foundations_use_case_read_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:organization` | `GET`  | `[base]/Organization/[id]` |
| [Organisation search](foundations_use_case_find_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization` | `GET`  | <code>[base]/Organization?identifier=https://fhir.nhs.uk/Id/ods-organization-code&#124;[odsCode]</code> |
| [Read location](foundations_use_case_read_a_location.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:location` | `GET`  | `[base]/Location/[id]` |
| [Register patient](foundations_use_case_register_a_patient.html)          | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient` | `POST`  | `[base]/Patient/$gpc.registerpatient` |


### Access Record HTML capability interactions ###

| Operation                 | InteractionID             | HTTP verb | Example URL pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Get care record](accessrecord_use_case_retrieve_a_care_record_section.html) | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord` | `POST` | `[base]/Patient/$gpc.getcarerecord` |


### Appointments capability interactions ###

| Operation                 | InteractionID             | HTTP verb | Example URL pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Search for free slots](appointments_use_case_search_for_free_slots.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot` | `POST` | `[base]/Slot` |
| [Read appointment](appointments_use_case_read_an_appointment.html)          | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment` | `GET`  | `[base]/Appointment/[id]` |
| [Create appointment](appointments_use_case_book_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment` | `POST` | `[base]/Appointment` |
| [Amend appointment](appointments_use_case_amend_an_appointment.html)         | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` | `PUT`  | `[base]/Appointment/[id]` |
| [Cancel appointment](appointments_use_case_cancel_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:cancel:appointment` | `PUT`  | `[base]/Appointment/[id]` |
| [Get patient appointments](appointments_use_case_retrieve_a_patients_appointments.html)  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments` | `GET`  | `[base]/Patient/[id]/Appointment` |


### Task capability interactions ###

| Operation                 | InteractionID             | HTTP verb | Example URL pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Create task](tasks_use_case_send_a_task.html) | `urn:nhs:names:services:gpconnect:fhir:rest:create:order` | `POST` | `[base]/Order/` |


## Stage 3. FHIR operations ##

*Aim*

- direct (unbundled) read-only access to care record resources for a patient

*Mechanism*

- RESTful APIs in line with the FHIR&reg; standard (with no custom operations)

```GET [base]/[ResourceType]?patient=[id]{&other parameters}```


{% include important.html content="Whilst several variations to the above URL syntax are possible, GP Connect provider systems are expected to support (as a minimum) the above format." %}

*Interactions*

All `InteractionIDs` are expected to follow the following format `urn:nhs:names:services:[program]:[standard]:[mechanism]:[claim]`.

{% include note.html content="`InteractionIDs` are to be considered case-insensitive." %}

- Program = `gpconnet`
- Standard = `fhir`
- Mechanism = [ `claim` ]
	- `claim` for logical access to a scoped resource.
- Claim
	- claim style API = [ `patient/AllergyIntolerance.read`, `patient/Condition.read`, and so on ]

{% include note.html content="The claims expressed below are in the format specified by the [SMART on FHIR](http://docs.smarthealthit.org/authorization/scopes-and-launch-context/) project." %}

| Operation                       | InteractionID             | Http verb | Example URL pattern |
|---------------------------------|---------------------------| ----------|---------------------|
| [Get patient allergy intolerances](accessrecord_rest_structured_data_allergyintolerance.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/AllergyIntolerance.read` | `GET`  | `[base]/AllergyIntolerance?patient=[id]` |
| [Get patient conditions](accessrecord_rest_structured_data_condition.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Condition.read` | `GET`  | `[base]/Condition?patient=[id]` |
| Get patient diagnostic orders | `urn:nhs:names:services:gpconnect:fhir:claim:patient/DiagnosticOrder.read` | `GET`  | `[base]/DiagnosticOrder?patient=[id]` |
| Get patient diagnostic reports | `urn:nhs:names:services:gpconnect:fhir:claim:patient/DiagnosticReport.read` | `GET`  | `[base]/DiagnosticReport?patient=[id]` |
| Get patient encounters | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Encounter.read` | `GET`  | `[base]/Encounter?patient=[id]` |
| Get patient flags | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Flag.read` | `GET`  | `[base]/Flag?patient=[id]` |
| [Get patient immunizations](accessrecord_rest_structured_data_immunization.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Immunization.read` | `GET`  | `[base]/Immunization?patient=[id]` |
| [Get patient medication orders](accessrecord_rest_structured_data_medicationorder.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationOrder.read` | `GET`  | `[base]/MedicationOrder?patient=[id]` |
| [Get patient medication statements](accessrecord_rest_structured_data_medicationstatement.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationStatement.read` | `GET`  | `[base]/MedicationStatement?patient=[id]` |
| Get patient medication dispenses | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationDispense.read` | `GET`  | `[base]/MedicationDispense?patient=[id]` |
| Get patient medication administrations | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationAdministration.read` | `GET`  | `[base]/MedicationAdministration?patient=[id]` |
| Get patient observations | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Observation.read` | `GET`  | `[base]/Observation?patient=[id]` |
| Get patient problems | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Problem.read` | `GET`  | `[base]/Problem?patient=[id]` |
| Get patient procedures | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Procedure.read` | `GET`  | `[base]/Procedure?patient=[id]` |
| Get patient referrals | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Referral.read` | `GET`  | `[base]/Referral?patient=[id]` |
| Get patient appointments | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Appointment.read` | `GET`  | `[base]/Appointment?patient=[id]` |

