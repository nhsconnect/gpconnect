---
title: Retrieve a patient's document
keywords: getstructuredrecord, view
tags: [design,structured]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_documents_development_retrieve_patient_documents.html
summary: "Retrieve a patient's document"
---

## Use case ##

Retrieve a patient's documents from a GP practice.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- **MUST** have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- **MUST** have previously traced the patient's NHS Number using the [Personal Demographics Service](https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service

## API usage ##

### Interaction diagram ###

<img style="height: 400px;" alt="Get patient's document interaction diagram" src="images/access_structured/get-patient-document-interaction-diagram.png"/>

### Request ###

#### FHIR&reg; relative request ####

```http
Get /Binary/[id]
```

#### FHIR&reg; absolute request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Binary/[id]
```

#### Request headers ####

Consumers **MUST** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's Trace ID (a GUID or UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect-documents:fhir:rest:read:binary-1`|

Example HTTP request headers:

```http
Accept: application/fhir+json;charset=utf-8
Content-Type: application/fhir+json;charset=utf-8
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect-documents:fhir:rest:read:binary-1
```

#### Payload request body ####
N/A

#### Error handling ####

Provider systems:

- SHALL return a [`GPConnect-OperationOutcome-1`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

Examples of other scenarios which may result in error being returned:

- Where a logical identifier of the resource is not valid/can’t be found on the server, a 404 HTTP Status code would be returned with the relevant OperationOutcome resource.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####
Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR® standards.

#### Payload response body ####

Provider systems **MUST**:

- return a `200` **OK** HTTP status code to indicate successful execution of the operation.
- return a `Binary` resource conforming to the [`Binary`](accessrecord_documents_development_binary.html) resource definition
- include the `versionId` of the current version of the `Binary` resource.

#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [Documents - FHIR&reg; examples](accessrecord_documents_development_fhir_examples_documents.html)
