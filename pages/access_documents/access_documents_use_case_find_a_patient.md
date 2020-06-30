---
title: Find a patient
keywords: foundations, patient, nhsnumber, pid
tags: [foundations,use_case]
sidebar: access_documents_sidebar
permalink: access_documents_use_case_find_a_patient.html
summary: "Find a patient by NHS number on the Access Document FHIR server"
---

{% include important.html content="This Find a Patient interaction is specific to the Access Document capability and is identified as such by an Access Document specific [interaction ID](#request-headers) and [service root URL](#fhir-absolute-request) path. Consumer systems **SHALL** only use this Find a Patient interaction in conjunction with other Access Document interactions." %}

## Use case ##

Find a patient using NHS number.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's Access Document FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- **SHALL** have previously traced the patient's NHS Number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service

## API usage ##

Resolve (zero or more) `Patient` resources using a business identifier (that is, NHS Number).

### Interaction diagram ###

<img style="height: 400px;" alt="Find patient interaction diagram" src="images/access_documents/documents-find-patient-interaction-diagram.png"/>

### Request operation ###

The consumer system:

- **SHALL** populate the `[system]` field with a valid patient identifier system URL (that is, `https://fhir.nhs.uk/Id/nhs-number`)

- **SHALL** apply percent encoding when constructing the request URL as indicated in [RFC 3986 Section 2.1](https://tools.ietf.org/html/rfc3986#section-2.1). This will ensure that downstream servers correctly handle the pipe `|` character, which must be used in the `identifier` parameter value below.

- **SHALL** only use this Find a Patient interaction in conjunction with other Access Document interactions, and **SHALL NOT** use it with interactions in other capabilities.

{% include important.html content="GP Connect can only guarantee a successful response for searches using the identifier type `https://fhir.nhs.uk/Id/nhs-number`. Other identifier types may result in an error response if the provider does not recognise or support the identifier." %}

#### FHIR relative request ####

```http
GET /Patient?identifier=[system]|[value]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[documents_provider_server]/[documents_fhir_base]/Patient?identifier=[system]|[value]
```

#### Request headers ####

Consumers **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:documents:fhir:rest:search:patient-1`|

#### Payload request body ####

N/A

#### Error handling ####

The provider system **MUST** return a `GPConnect-OperationOutcome-1` resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shown common errors that may be encountered during this API call, and the returned Spine error code. Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response or to determine the response for errors encountered that are not shown below.

Errors returned due to query parameter failure **MUST** include diagnostic information detailing the invalid query parameter.

|-------------------------|-------------------|
| Error encountered        | Spine error code returned |
|-------------------------|-------------------|
| The `identifier` parameter is not provided | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `identifier` parameter contains a missing or unrecognised system | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The NHS number provided is invalid, for example it fails format or check digit tests | [`INVALID_NHS_NUMBER`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| GP Connect is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| The Access Document capability is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors) |
|-------------------------|-------------------|

{% include important.html content="Failure to find a record with the supplied business identifier is not considered an error condition." %}

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful execution of the operation
- **SHALL** return zero or more matching `Patient` resources in a `Bundle` of `type` searchset
- **SHALL** only return `Patient` resources for [active patients](overview_glossary.html#active-patient) with a Regular/GMS registration type (i.e. where this is their registered GP practice)

  {% include note.html content="Please note the restriction on returning patient records with a Regular/GMS registration type is a difference in behaviour between this Find a patient and [Find a patient](foundations_use_case_find_a_patient.html) in the Foundations capability." %}

- **SHALL** return `Patient` resources that conform to the [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1/_history/1.8) profile

- **SHALL** populate the following `Patient` fields:
  - `meta.profile` with the profile URI
  - `versionId` with the current version of each `Patient` resource
  - `identifier` with relevant business identifiers, including a minimum of the patient's NHS Number
  - `name`
    - The patient resource **SHALL** contain a single instance of the name element with the `use` of `official` and SHALL contain the name synchronised with PDS
  - `birthDate`
  - `gender`
  - `address` where available
  - `telecom` where available
  - `contact` with the patient's contacts - see [Patient.contact population](development_fhir_resource_guidance.html#patientcontact) for further details
  - `registrationDetails.preferredBranchSurgery` with a reference to a `Location` resource representing the patient's preferred branch surgery (see [Branch surgeries](development_branch_surgeries.html) for more details)
  - `nhsCommunication` with the patient's language information, where available
  - `managingOrganization` Note: this is the current organisation, as addressed by ODS code in the base URL, and NOT the patient's registered practice, which may be different

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
{
  "resourceType": "Bundle",
  "type": "searchset",
  "entry": [
    {
      "resource": {
        "resourceType": "Patient",
        "id": "2",
        "meta": {
          "versionId": "1469448000000",
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"
          ]
        },
        "extension": [
          {
            "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-RegistrationDetails-1",
            "extension": [
              {
                "url": "preferredBranchSurgery",
                "valueReference": {
                  "reference": "Location/785b4ff5-aced-4bdf-b7ed-34f92131ce97"
                }
              }
            ]
          },
          {
            "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-NHSCommunication-1",
            "extension": [
              {
                "url": "language",
                "valueCodeableConcept": {
                  "coding": [
                    {
                      "system": "https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-HumanLanguage-1",
                      "code": "bn",
                      "display": "Bengali"
                    }
                  ]
                }
              },
              {
                "url": "interpreterRequired",
                "valueBoolean": false
              }
            ]
          }
        ],
        "identifier": [
          {
            "extension": [
              {
                "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-NHSNumberVerificationStatus-1",
                "valueCodeableConcept": {
                  "coding": [
                    {
                      "system": "https://fhir.nhs.uk/CareConnect-NHSNumberVerificationStatus-1",
                      "code": "01",
                      "display": "Number present and verified"
                    }
                  ]
                }
              }
            ],
            "system": "https://fhir.nhs.uk/Id/nhs-number",
            "value": "9476719931"
          }
        ],
        "active": true,
        "name": [
          {
            "use": "official",
            "text": "JACKSON Jane (Miss)",
            "family": "Jackson",
            "given": [
              "Jane"
            ],
            "prefix": [
              "Miss"
            ]
          }
        ],
        "telecom": [
          {
            "system": "phone",
            "value": "01454587554",
            "use": "home"
          }
        ],
        "gender": "female",
        "birthDate": "1952-05-31",
        "address": [
          {
            "use": "home",
            "type": "physical",
            "line": [
              "Trevelyan Square",
              "Boar Ln"
            ],
            "city": "Leeds",
            "district": "West Yorkshire",
            "postalCode": "LS1 6AE"
          }
        ],
        "managingOrganization": {
          "reference": "Organization/14"
        }
      }
    }
  ]
}
```
