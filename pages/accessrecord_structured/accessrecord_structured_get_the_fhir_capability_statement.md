---
title: Get the FHIR&reg; capability statement
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_get_the_fhir_capability_statement.html
summary: "Get the FHIR capability statement from the Access Record Structured FHIR server"
---

{% include warning.html content="Consumer systems **MUST NOT** use this API interaction unless instructed to do so as it is not yet present in all live systems. Please use the [combined FHIR&reg; capability statement](foundations_use_case_get_the_fhir_capability_statement.html) instead." %}

{% include important.html content="This capability statement is specific to the Access Record Structured capability and is identified as such by an Access Record Structured specific [interaction ID](#request-headers) and [service root URL](#fhir-absolute-request) path. Please see other capabilities for their respective capability statements." %}

## Use case ##

Get the Access Record Structured FHIR capability statement.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's Access Record Structured FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API usage ##

### Interaction diagram ###

<img style="height: 400px;" alt="Get the FHIR&reg; capability statement interaction diagram" src="images/access_structured/get-structured-capability-statement-interaction-diagram.png"/>

### Request operation ###

#### FHIR relative request ####

```http
GET /metadata
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[structured_provider_server]/[structured_fhir_base]/metadata
```

#### Request headers ####

Consumers **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:structured:fhir:rest:read:metadata-1`|

#### Payload request body ####

N/A

#### Error handling ####

The provider system **MUST** return a `GPConnect-OperationOutcome-1` resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shown common errors that may be encountered during this API call, and the returned Spine error code. Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response or to determine the response for errors encountered that are not shown below.

Errors returned due to query parameter failure **MUST** include diagnostic information detailing the invalid query parameter.

|-------------------------|-------------------|
| Error encountered        | Spine error code returned |
|-------------------------|-------------------|
| GP Connect is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| The Access Record Structured capability is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors) |
|-------------------------|-------------------|


### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful retrieval of the capability statement
- **SHALL** return a capability statement which conforms to the standard [FHIR CapabilityStatement](http://hl7.org/fhir/STU3/capabilitystatement.html)

An example Access Record Structured capability statement is shown below ready for customisation and embedding into assured provider systems. Providers should use this capability statement as a base for their own Access Record Structured capability statement, replacing the element in square brackets (`[` & `]`) with specific information of their implementation. The main version at the top of the CapabilityStatement should represent the GP Connect API specification version that the Access Record Structured FHIR server implements.

```json
{
  "resourceType": "CapabilityStatement",
  "version": "1.5.1",
  "name": "GP Connect API - Access Record Structured",
  "status": "active",
  "date": "2020-02-10",
  "publisher": "[Provider Software Vendor Name]",
  "contact": [
    {
      "name": "[Provider Software Vendor Contact Name]"
    }
  ],
  "description": "This server implements the GP Connect API - Access Record Structured version 1.5.1",
  "copyright": "Copyright NHS Digital 2016-21",
  "kind": "capability",
  "software": {
    "name": "[Provider Software Name]",
    "version": "[Provider Software Version]",
    "releaseDate": "[Provider Software Release Date]"
  },
  "fhirVersion": "3.0.1",
  "acceptUnknown": "both",
  "format": [
    "application/fhir+json",
    "application/fhir+xml"
  ],
  "profile": [
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1/_history/1.8" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1/_history/1.4" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1/_history/1.2" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-PractitionerRole-1/_history/1.2" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1/_history/1.7" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1/_history/1.2" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1/_history/1.7" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1/_history/1.6" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1/_history/1.7" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1/_history/1.3" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1/_history/1.2" }
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Immunization-1/_history/1.5" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Condition-ProblemHeader-1/_history/1.6" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Encounter-1/_history/1.5" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1/_history/1.6" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DiagnosticReport-1/_history/1.3" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Specimen-1/_history/1.3" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ProcedureRequest-1/_history/1.3" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1/_history/1.2" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1/_history/1.3"}
      { "reference": "https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-HealthcareService-1/_history/1.0"}
  ],
  "rest": [
    {
      "mode": "server",
      "security": {
        "cors": true
      },
      "operation": [
        {
          "name": "gpc.getstructuredrecord",
          "definition": {
            "reference": "https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1/_history/1.16"
          }
        },
        {
          "name": "gpc.migratestructuredrecord",
          "definition": {
            "reference": "https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-MigrateStructuredRecord-Operation-1/_history/1.1"
          }
        },
      ]
    }
  ]
}
```

Consumer systems:
- **SHOULD** request the capability statement from the Access Record Structured FHIR server endpoint in order to ascertain details of the implementation delivered by the FHIR server, this includes checking the version number specified in `CapabilityStatement.version`
- **MAY** also cache the Access Record Structured capability statement information retrieved from an endpoint to reduce the number of future calls they make to the target organization's Access Record Structured FHIR server.
