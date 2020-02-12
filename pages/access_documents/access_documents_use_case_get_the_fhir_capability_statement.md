---
title: Get the FHIR&reg; capability statement
keywords: foundations, fhir
tags: [foundations,use_case,fhir]
sidebar: access_documents_sidebar
permalink: access_documents_use_case_get_the_fhir_capability_statement.html
summary: "Get the Access Document FHIR capability statement"
---

{% include important.html content="This capability statement is specific to the Access Document capability and is identified as such by a Access Document specific [interaction ID](#request-headers) and [service root URL](#fhir-absolute-request) path. Please see other capabilities for their respective capability statements." %}

## Use case ##

Get the Access Document FHIR capability statement.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's Access Document FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /metadata
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[access_document_provider_server]/[access_document_fhir_base]/metadata
```

#### Request headers ####

Consumers **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:documents:fhir:rest:read:metadata-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems are expected to always be able to return a valid capability statement.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful retrieval of the capability statement
- **SHALL** return a capability statement which conforms to the standard [FHIR CapabilityStatement](http://hl7.org/fhir/STU3/capabilitystatement.html)

An example GP Connect capability statement is shown below ready for customisation and embedding into GP Connect Access Document assured provider systems. Providers should use this capability statement as a base for their own capability statement, replacing the element in square brackets (`[` & `]`) with specific information of their implementation. The main version at the top of the CapabilityStatement should represent the GP Connect API specification version that the Access Document FHIR server implements.

```json
{
  "resourceType": "CapabilityStatement",
  "version": "1.5.0",
  "name": "GP Connect API - Access Document",
  "status": "active",
  "date": "2020-02-10",
  "publisher": "[Provider Software Vendor Name]",
  "contact": [
    {
      "name": "[Provider Software Vendor Contact Name]"
    }
  ],
  "description": "This server implements the GP Connect API - Access Document version 1.5.0",
  "copyright": "Copyright NHS Digital 2016-20",
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
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1/_history/1.2" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1/_history/1.2" },
      { "reference": "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1/_history/1.3" },
  ],
  "rest": [
    {
      "mode": "server",
      "security": {
        "cors": true
      },
      "resource": [
        {
          "type": "Patient",
          "interaction": [
            {
              "code": "read"
            },
            {
              "code": "search-type"
            }
          ],
          "searchParam": [
            {
              "name": "identifier",
              "type": "token",
              "documentation": "NHS Number (i.e. https://fhir.nhs.uk/Id/nhs-number|123456789)"
            }
          ]
        },
        {
          "type": "Binary",
          "interaction": [
            {
              "code": "read"
            }
          ]
        },
        {
          "type": "DocumentReference",
          "interaction": [
            {
              "code": "search-type"
            }
          ],
          "searchInclude": [
            "DocumentReference:patient"
            "DocumentReference:custodian:Organization"
            "DocumentReference:author:Organization"            
          ],
          "searchParam": [
            {
              "name": "subject",
              "type": "Patient"
            },
            {
              "name": "created",
              "type": "date"
            },
            {
              "name": "facility",
              "type": "token"
            },
            {
              "name": "author",
              "type": "Organization"
            },
            {
              "name": "type",
              "type": "token"
            },
            {
              "name": "custodian",
              "type": "Organization"
            },
            {
              "name": "description",
              "type": "string"
            }
          ]
        }
      ]
    }
  ]
}
```

Consumer systems:
- **SHOULD** request the capability statement from the Access Document FHIR server endpoint in order to ascertain details of the implementation delivered by the FHIR server, this includes checking the version number specified in `CapabilityStatement.version`
- **MAY** also cache the Access Document capability statement information retrieved from an endpoint to reduce the number of future calls they make to the target organization's Access Document FHIR server.
