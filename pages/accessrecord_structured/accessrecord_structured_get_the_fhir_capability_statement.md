---
title: Get the structured FHIR&reg; capability statement
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_get_the_fhir_capability_statement.html
summary: "Get the FHIR capability statement for the Access Record Structured capability"
---

{% include warning.html content="Consumer systems MUST NOT use this API interaction unless instructed to do so as it is not yet present in all live systems. Please use the [combined FHIR&reg; capability statement](foundations_use_case_get_the_fhir_capability_statement.html) instead." %}

## Use case ##

Retrieve the FHIR&reg; capability statement describing the Access Record Structured capability at a GP practice.

{% include important.html content="Please note this capability statement describes the Access Record Structured capability only.  For the combined capability statement that describes Appointment Management, Foundations and Access Record Structured please see [Get the FHIR&reg; capability statement](foundations_use_case_get_the_fhir_capability_statement.html) " %}

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- **MUST** have previously resolved the organisation's Access Record Structured FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /metadata
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[structured_fhir_base]/metadata
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:structured_metadata-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems are expected to always be able to return a valid capability statement.

### Request response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful retrieval of the capability statement
- SHALL return a capability statement which conforms to the standard [FHIR CapabilityStatement](http://hl7.org/fhir/STU3/capabilitystatement.html)

An example GP Connect API Access Record Structured `CapabilityStatement` is shown below ready for customisation and embedding into GP Connect assured provider systems. Providers should use this CapabilityStatement as a base for their own CapabilityStatement, replacing the element in square brackets (`[` & `]`) with specific information of their implementation. The main version at the top of the `CapabilityStatement` should represent the GP Connect specification version which the FHIR server implements.

```json
{
  "resourceType": "CapabilityStatement",
  "version": "1.2.6",
  "name": "GP Connect Access Record Structured API",
  "status": "active",
  "date": "2019-11-05",
  "publisher": "[Provider Software Vendor Name]",
  "contact": [
    {
      "name": "[Provider Software Vendor Contact Name]"
    }
  ],
  "description": "This server implements the GP Connect Access Record Structured API version 1.2.6",
  "copyright": "Copyright NHS Digital 2016-9",
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
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-PractitionerRole-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-List-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1" }
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
            "reference": "https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1/_history/1.8"
          }
        }
      ]
    }
  ]
}
```

Consumer systems:
- **SHOULD** request the capability statement from the Access Record Structured FHIR server endpoint in order to ascertain details of the implementation of GP Connect Access Record Structured capabilities delivered by the FHIR server
- Consumers **MAY** also cache the capability statement information retrieved from an endpoint to reduce the number of future calls they make to the target organization's FHIR server.
