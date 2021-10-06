---
title: Register a patient
keywords: foundations, patient, nhsnumber, pid, register
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_register_a_patient.html
summary: "Use case for registering a patient with an organisation"
---

## API use case ##

The "Register a patient" use case creates a new temporary patient registration, or re-activates an existing "inactive" patient registration as a temporary patient registration within the GP practice system ([Definition of a GP Connect active patient](/overview_glossary.html#active-patient)).

This specification describes a single use case. For complete details and background please see the [Foundations capability bundle](foundations.html).

{% include note.html content="This API use case is designed only to support the need to  register a **temporary** patient at a federated organisation as an enabler for federated appointment bookings. It does not change a patient's registered practice information as held on the Personal Demographics Service (PDS)." %}

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorisation
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details 

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service


## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
POST /Patient/$gpc.registerpatient
```

#### FHIR absolute request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/$gpc.registerpatient
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient-1`|

Example HTTP request headers:

```http
{% include foundations/register-patient-request-headers-1.txt %}
```

#### Payload request body ####

The request payload is a [Parameters](https://www.hl7.org/fhir/STU3/parameters.html) resource conforming to the [GPConnect-RegisterPatient-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-RegisterPatient-Operation-1/) profile, with a single parameter of `registerPatient` containing a `Patient` resource profiled to the [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) profile.  This is the patient to be registered.

Within the `Patient` resource: 

- The following fields SHALL be populated as a minimum to allow the provider system to perform a PDS trace:
  - `identifier` with the patient's NHS number
  - `name` including `family` and `given`, with the `use` element set to `official`.
    - No more than one instance of `name` where `use` is set to `official` SHALL be provided.
  - `birthDate`

- The following fields SHOULD be populated, to create the patient's record in the provider system:
  - `gender`
  - `address` with the patient's home address, with the `use` of `home`. No more than one instance of this `use` SHALL be populated.
  - `telecom` with the patient's telephone number(s), with `use` of `home`, `work` or `mobile`, and `system` of `phone`. No more than one instance of each `use` SHALL be populated.
  - `telecom` with the patient's email address if available, with `system` of `email`. No more than one instance of this SHALL be populated.
  - a single instance of `nhsCommunication` if available, specifically the `language` and `interpreterRequired` sub-elements
  
    {% include important.html content="If the above *\"SHOULD\"* fields are not provided, the provider system will use demographics retrieved from PDS in order to create the patient's record." %}

- The following fields MAY be populated in order to record temporary details known to the consuming system:
  - `address` with temporary address details, with the `use` of `temp`.  No more than one instance of this `use` SHALL be populated.
  - `telecom` with temporary telephone details, with the `use` of `temp` and `system` of `phone`.  No more than one instance of this SHALL be populated.

- **All other fields MUST NOT be populated.**

On the wire a JSON serialised `$gpc.registerpatient` request would look something like the following:

```json
{% include foundations/register-patient-request-payload-1.json %}
```

### Provider system registration requirements ###

{% include important.html content="The following registration requirements MUST be implemented by providers, however due to provider system variances the implemented flow MAY deviate where required to accommodate these and shall be agreed and documented accordingly." %}

#### PDS requirements ####

Before registering the patient record on the local system, the provider SHALL retrieve the patient's demographic record using a PDS Retrieval Query, and then:

- **Verify the patient's NHS number according to the rules below**:

  - The NHS number within the request is considered verified if:
    - The NHS number is found on PDS and the date of birth in the request exactly matches the date of birth held on PDS
    - OR should 2 out of 3 parts of the date of birth match (YYYY or MM or DD) AND the first 3 characters of the first family name match and the initial character of the given match that held for the record on PDS.
  - If both of the above checks fail to find a match then the NHS number is treated as not verified

    {% include note.html content="The provider **MAY** use a [PDS Cross Check Trace](https://data.developer.nhs.uk/dms/mim/6.3.01/Domains/PDS/Document%20files/PDS%20IM.htm#_Toc_Section_2.10) to perform this step, instead of using a [PDS Retrieval](https://data.developer.nhs.uk/dms/mim/6.3.01/Domains/PDS/Document%20files/PDS%20IM.htm#_Toc_Section_2.4) and implementing the rules local locally.
    <br/>
    If using the Cross Check Trace, the provider **MUST** then perform a subsequent Retrieval Query in order to return the patient's full PDS record to supplement the patient's demographics when creating or updating the patient's record (in [Local registration requirements](foundations_use_case_register_a_patient.html#local-registration-requirements))." %}

- **Check that the patient is not recorded as deceased on PDS**

- **Check that patient's PDS record does not have any of the following PDS flags**:
  - Invalid
  - Sensitive
  - Superseded


#### Duplicate record prevention

Before registering the patient record on the local system, the provider SHALL check the practice patient index for matching patients using the patient's NHS number, and then:

- **If a matching patient record IS found**:

  - and the matching patient record's NHS number has not previously been traced or verified, it SHALL be verified using the [rules shown above](foundations_use_case_register_a_patient.html#pds-requirements)

    - If the verification fails the registration SHALL be halted and an error returned to the consuming system

  - Then, if the matching patient record:

    - is **active** (i.e. a currently registered patient, of any registration type):

      - The registration SHALL be halted and error is returned to the consumer

    - is **inactive** (i.e. a patient whose registration has lapsed of any registration type):

      - The patient record SHALL be re-activated as a **temporary** patient 
      - Follow the [Local registration requirements](foundations_use_case_register_a_patient.html#local-registration-requirements) when updating the patient's demographics

    - is recorded as **deceased**:

      - The registration SHALL be halted and an error returned to the consuming system

- **If a matching patient record IS NOT found**:

  - A new **temporary** patient record SHALL be created
  - Follow the [Local registration requirements](foundations_use_case_register_a_patient.html#local-registration-requirements) when creating the patient record

{% include warning.html content="Provider systems MUST NOT create or re-activate a patient as a GMS (regular) patient.  Doing so would adversely affect national systems and interfere with the practice's caseload." %}

#### Local registration requirements

- **The patient record SHOULD be created or updated using**:

  - demographic details sent by the consumer
  - supplemented by demographics returned from a PDS Retrieval Query where elements were omitted by the consumer or not part of the payload request message
  - temporary address or temporary telecom details sent by the consumer SHOULD be marked with an end date aligned with the expiry date of the temporary record.

- **If the provider system synchronises temporary patient records with PDS**:
  - an update SHALL NOT automatically be sent to PDS
  - PDS synchronisation SHALL occur where a user is present during the next routine synchronisation event (for example, a receptionist opening the patient's record)
  - temporary address or temporary telecom details SHOULD be marked with an end date.

- **a populated `Patient` resource representing the record created, or reactivated and updated, SHALL be returned to the consuming system shown in [Payload response body](foundations_use_case_register_a_patient.html#payload-response-body) below**.

#### Error Handling ####

The provider system **MUST** return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shown common errors that may be encountered during this API call, and the returned Spine error code.  Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response, or to determine the response for errors encountered that are not shown below.

Errors returned due to parameter failure **MUST** include diagnostic information detailing the invalid parameter.

|-------------------------|-------------------|
| Error encountered        | Spine error code returned |
|-------------------------|-------------------|
| The `Parameters` resource passed by the consuming system including the embedded `Patient` resource is invalid, or does not include the minimum mandatory details | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The NHS number could not be found on PDS, or verified against a PDS record | [`INVALID_PATIENT_DEMOGRAPHICS`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The patient is marked as deceased on PDS, or on the provider system | [`INVALID_PATIENT_DEMOGRAPHICS`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The registration request is for a sensitive patient | [`INVALID_PATIENT_DEMOGRAPHICS`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The PDS record contains an invalid or superseded flag | [`INVALID_NHS_NUMBER`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| PDS is unavailable, or could not be contacted | [`INTERNAL_SERVER_ERROR`](development_fhir_error_handling_guidance.html#internal-server-errors) |
| The patient is already registered | [`DUPLICATE_REJECTED`](development_fhir_error_handling_guidance.html#duplicate-errors) |
|-------------------------|-------------------|

### Request response ###

#### Response headers ####

```http
HTTP/1.1 200 OK
Cache-Control: no-store
Content-Type: application/fhir+json; charset=utf-8
Date: Sun, 07 Aug 2016 11:13:05 GMT
Content-Length: 1464
```

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful registration of the patient into the provider system.
- SHALL include the URI of the relevant GP Connect `StructureDefinition` profile in the `Patient.meta.profile` element of the returned resources.
- SHALL return a searchset `Bundle` profiled to [GPConnect-Searchset-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1) with a `Patient` profiled to [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) 
- SHALL populate the `Patient` resource with details of the newly registered or re-activated patient

- SHALL populate the following fields:
  - `meta.profile` with the profile URI
  - `versionId` with the current version of the `Patient` resource.
  - `identifier` with relevant business identifiers, including a minimum of the patient's NHS number
  - `name`
  - `birthDate`
  - `gender`
  - `address` where available
  - `telecom` where available
  - `contact` with the patient's contacts - see [Patient.contact population](development_fhir_resource_guidance.html#patientcontact) for further details
  - `registrationDetails.preferredBranchSurgery` with a reference to a `Location` resource representing the patient's preferred branch surgery (see [Branch surgeries](development_branch_surgeries.html) for more details), for a re-activated patient where available
  - `registrationDetails.registrationType` with the registration type used within the provider system. If an appropriate registration type is not available within the valueset then the `Other` type SHALL be use and the name of the registration type SHOULD be added using the `text` element of the CodeableConcept
  - `nhsCommunication` with the patient's language information, where available
  - `managingOrganization` Note: this is the current organisation, as addressed by ODS code in the base URL, and NOT the patient's registered practice which may be different

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all  fields where data is available, excluding those listed below

- SHALL NOT populate the following fields:
  - `ethnicCategory`
  - `religiousAffiliation`
  - `patient-cadavericDonor`
  - `residentialStatus`
  - `treatmentCategory`
  - `birthPlace`
  - `maritalStatus`
  - `multipleBirthBoolean`

```json
{% include foundations/register-patient-response-payload-1.json %}
```
