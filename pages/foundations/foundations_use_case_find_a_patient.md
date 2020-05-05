---
title: Find a patient
keywords: foundations, patient, nhsnumber, pid
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_a_patient.html
summary: "Use case for finding a patient resource by business identity"
---

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service

## API usage ##

Resolve (zero or more) `Patient` resources using a business identifier (that is, NHS number).

### Request operation ###

The consumer system:

- **SHALL** populate the `[system]` field with a valid patient identifier system URL (that is, `https://fhir.nhs.uk/Id/nhs-number`).

- **SHALL** apply percent encoding when constructing the request URL as indicated in [RFC 3986 Section 2.1](https://tools.ietf.org/html/rfc3986#section-2.1). This will ensure that downstream servers correctly handle the pipe `|` character, which must be used in the `identifier` parameter value below.

{% include important.html content="GP Connect can only guarantee a successful response for searches using the identifier type `https://fhir.nhs.uk/Id/nhs-number`. Other identifier types may result in an error response if the provider does not recognise or support the identifier." %}

#### FHIR relative request ####

```http
GET /Patient?identifier=[system]|[value]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient?identifier=[system]|[value]
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems:

- **SHALL** return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached

For example, the:

- business identifier `[system]` is not recognised/supported by the Provider system
- business identifier fails structural validation checks (that is, not enough digits to be a valid NHS number)

{% include important.html content="Failure to find a record with the supplied business identifier is not considered an error condition." %}

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return zero or more matching `Patient` resources in a `Bundle` of `type` searchset.
- SHALL only return `Patient` resources for [active patients](overview_glossary.html#active-patient). Where a patient is active but their NHS number has never been traced or verified, please see the [provider system unverified record requirements](#provider-system-unverified-record-requirements) below.
- SHALL return `Patient` resources that conform to the [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) profile.

- **SHALL** populate the following `Patient` fields:
  - `meta.profile` with the profile URI
  - `versionId` with the current version of each `Patient` resource.
  - `identifier` with relevant business identifiers, including a minimum of the patient's NHS number
  - `name`
    - The patient resource SHALL contain a single instance of the name element with the `use` of `official` and SHALL contain the name synchronised with PDS.
  - `birthDate`
  - `gender`
  - `address` where available
  - `telecom` where available
  - `contact` with the patient's contacts - see [Patient.contact population](development_fhir_resource_guidance.html#patientcontact) for further details
  - `registrationDetails.preferredBranchSurgery` with a reference to a `Location` resource representing the patient's preferred branch surgery (see [Branch surgeries](development_branch_surgeries.html) for more details)
  - `nhsCommunication` with the patient's language information, where available
  - `managingOrganization` Note: this is the current organisation, as addressed by ODS code in the base URL, and NOT the patient's registered practice which may be different

- **SHALL** meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields where data is available, excluding those listed below

- **SHALL NOT** populate the following fields:
  - `ethnicCategory`
  - `religiousAffiliation`
  - `patient-cadavericDonor`
  - `residentialStatus`
  - `treatmentCategory`
  - `birthPlace`
  - `maritalStatus`
  - `multipleBirthBoolean`

```json
{% include foundations/find_patient_response_example.json %}
```

#### Provider system unverified record requirements ####

Where an **[active](overview_glossary.html#active-patient) matching patient record** is found, but the **NHS number on this record has never been traced or verified** (either on PDS, or indirectly via NHAIS), the provider SHALL retrieve the patient's demographic record using a PDS Retrieval Query, and then:

- Verify the patient's NHS number according to the rules below:

  - The NHS number is considered verified if:
    - The NHS number is found on PDS and the date of birth on the local system exactly matches the date of birth held on PDS
    - OR should 2 out of 3 parts of the date of birth match (YYYY or MM or DD) AND the first 3 characters of the first family name match and the initial character of the given match that held for the record on PDS.
  - If both of the above checks fail to find a match then the NHS number is not considered as verified

- In addition, check that the patient is not recorded as deceased on PDS

- In addition, check that patient's PDS record does not have any of the following PDS flags:
  - Invalid
  - Sensitive
  - Superseded

If all three steps above succeed the patient's NHS number SHALL be marked as verified, and the patient SHALL be included in the response bundle. Otherwise the patient's NHS number SHALL NOT be marked as verified and SHALL NOT be included in the response bundle.