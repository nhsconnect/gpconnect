---
title: Operation guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_operation_guidance.html
summary: "Details of which operations a FHIR server should expose to be a fully compliant GP Connect solution"
---

## Stage 1 & 2 FHIR Operations ##

*Aim(s)*

- HTML Access Record Views (with Bundled Structured).
- Appointment and Task management.

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
| [Read Patient](foundations_use_case_read_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient` | `GET`  | `[base]/Patient/[id]` |
| [Patient Search](foundations_use_case_find_a_patient.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient` | `GET`  | <code>[base]/Patient?identifier=https://fhir.nhs.uk/Id/nhs-number&#124;[nhsNumber]</code> |
| [Read Practitioner](foundations_use_case_read_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:practitioner` | `GET`  | `[base]/Practitioner/[id]` |
| [Practitioner Search](foundations_use_case_find_a_practitioner.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:practitioner` | `GET`  | <code>[base]/Practitioner?identifier=https://fhir.nhs.uk/Id/sds-user-id&#124;[sdsUserID]</code> |
| [Read Organisation](foundations_use_case_read_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:organization` | `GET`  | `[base]/Organization/[id]` |
| [Organisation Search](foundations_use_case_find_an_organisation.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization` | `GET`  | <code>[base]/Organization?identifier=https://fhir.nhs.uk/Id/ods-organization-code&#124;[odsCode]</code> |
| [Read Location](foundations_use_case_read_a_location.html) | `urn:nhs:names:services:gpconnect:fhir:rest:read:location` | `GET`  | `[base]/Location/[id]` |
| [Register Patient](foundations_use_case_register_a_patient.html)          | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient` | `POST`  | `[base]/Patient/$gpc.registerpatient` |


### Access Record HTML capability interactions ###

| Operation                 | InteractionID             | Http Verb | Example URL Pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Get Care Record](accessrecord_use_case_retrieve_a_care_record_section.html) | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord` | `POST` | `[base]/Patient/$gpc.getcarerecord` |


### Appointments capability interactions ###

| Operation                 | InteractionID             | Http Verb | Example URL Pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Search for free slots](appointments_use_case_search_for_free_slots.html) | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot` | `POST` | `[base]/Slot` |
| [Read Appointment](appointments_use_case_read_an_appointment.html)          | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment` | `GET`  | `[base]/Appointment/[id]` |
| [Create Appointment](appointments_use_case_book_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment` | `POST` | `[base]/Appointment` |
| [Amend Appointment](appointments_use_case_amend_an_appointment.html)         | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` | `PUT`  | `[base]/Appointment/[id]` |
| [Cancel Appointment](appointments_use_case_cancel_an_appointment.html)        | `urn:nhs:names:services:gpconnect:fhir:rest:cancel:appointment` | `PUT`  | `[base]/Appointment/[id]` |
| [Get Patient Appointments](appointments_use_case_retrieve_a_patients_appointments.html)  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments` | `GET`  | `[base]/Patient/[id]/Appointment` |


### Task capability interactions ###

| Operation                 | InteractionID             | Http Verb | Example URL Pattern |
|---------------------------|---------------------------| ----------|---------------------|
| [Create Task](tasks_use_case_send_a_task.html) | `urn:nhs:names:services:gpconnect:fhir:rest:create:order` | `POST` | `[base]/Order/` |


## Stage 3. FHIR Operations ##

*Aim*

- Direct (unbundled) read-only access to care record resources for a patient.

*Mechanism*

- RESTful APIs in-line with the FHIR&reg; standard (with no custom operations).

```GET [base]/[ResourceType]?patient=[id]{&other parameters}```


{% include important.html content="Whilst several variations to the above URL syntax are possible GP Connect provider systems are expected to support (as a minimum) the above format." %}

*Interactions*

All `InteractionIDs` are expected to follow the following format `urn:nhs:names:services:[program]:[standard]:[mechanism]:[claim]`.

{% include note.html content="`InteractionIDs` are to be considered case-insensitive." %}

- Program = `gpconnet`
- Standard = `fhir`
- Mechanism = [ `claim` ]
	- `claim` for logical access to a scoped resource.
- Claim
	- Claim style API = [ `patient/AllergyIntolerance.read`, `patient/Condition.read` ... etc ]

{% include note.html content="The claims expressed below are in the format specified by the [SMART on FHIR](http://docs.smarthealthit.org/authorization/scopes-and-launch-context/) project." %}

| Operation                       | InteractionID             | Http Verb | Example URL Pattern |
|---------------------------------|---------------------------| ----------|---------------------|
| [Get Patient Allergy Intolerances](accessrecord_rest_structured_data_allergyintolerance.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/AllergyIntolerance.read` | `GET`  | `[base]/AllergyIntolerance?patient=[id]` |
| [Get Patient Conditions](accessrecord_rest_structured_data_condition.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Condition.read` | `GET`  | `[base]/Condition?patient=[id]` |
| Get Patient Diagnostic Orders | `urn:nhs:names:services:gpconnect:fhir:claim:patient/DiagnosticOrder.read` | `GET`  | `[base]/DiagnosticOrder?patient=[id]` |
| Get Patient Diagnostic Reports | `urn:nhs:names:services:gpconnect:fhir:claim:patient/DiagnosticReport.read` | `GET`  | `[base]/DiagnosticReport?patient=[id]` |
| Get Patient Encounters | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Encounter.read` | `GET`  | `[base]/Encounter?patient=[id]` |
| Get Patient Flags | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Flag.read` | `GET`  | `[base]/Flag?patient=[id]` |
| [Get Patient Immunizations](accessrecord_rest_structured_data_immunization.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Immunization.read` | `GET`  | `[base]/Immunization?patient=[id]` |
| [Get Patient Medication Orders](accessrecord_rest_structured_data_medicationorder.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationOrder.read` | `GET`  | `[base]/MedicationOrder?patient=[id]` |
| [Get Patient Medication Statements](accessrecord_rest_structured_data_medicationstatement.html) | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationStatement.read` | `GET`  | `[base]/MedicationStatement?patient=[id]` |
| Get Patient Medication Dispenses | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationDispense.read` | `GET`  | `[base]/MedicationDispense?patient=[id]` |
| Get Patient Medication Administrations | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationAdministration.read` | `GET`  | `[base]/MedicationAdministration?patient=[id]` |
| Get Patient Observations | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Observation.read` | `GET`  | `[base]/Observation?patient=[id]` |
| Get Patient Problems | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Problem.read` | `GET`  | `[base]/Problem?patient=[id]` |
| Get Patient Procedures | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Procedure.read` | `GET`  | `[base]/Procedure?patient=[id]` |
| Get Patient Referrals | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Referral.read` | `GET`  | `[base]/Referral?patient=[id]` |
| Get Patient Appointments | `urn:nhs:names:services:gpconnect:fhir:claim:patient/Appointment.read` | `GET`  | `[base]/Appointment?patient=[id]` |

