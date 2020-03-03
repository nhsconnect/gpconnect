---
title: Read a patient
keywords: foundations, patient, nhsnumber, pid, read
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_read_a_patient.html
summary: "Use case for reading a patient resource"
---

## Prerequisites ##

### Consumer ###

The consumer application:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( integration_personal_demographic_service.html) or an equivalent service
- SHALL have previously [resolved the logical ID of the patient](foundations_use_case_find_a_patient.html) on the server using the NHS Number

## API use case ##

This page describes a single use case. For complete details and background, please see the [Foundations Capability Bundle](foundations.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /Patient/[id]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/[id]
```

#### Request headers ####

Consumer applications **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems **SHALL** return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

For example, the:

- logical identifier of the resource is not valid/can't be found on the server 

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful execution of the operation.
- **SHALL** return `Patient` resources that conform to the [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) profile.

- **SHALL** populate the following fields:
  - `meta.profile` with the profile URI
  - `versionId` with the current version of the `Patient` resource.
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
{
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
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Read<Patient>("Patient/2");
FhirSerializer.SerializeResourceToXml(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = new FhirContext().forStu3();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
Patient patient = client.read().resource(Patient.class).withId("2").execute();
```
