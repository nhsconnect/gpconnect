---
title: Migrate a document
keywords: getstructuredrecord, view
tags: [design,structured]
sidebar: access_documents_sidebar
permalink: access_documents_development_migrate_patient_documents.html
summary: "Migrate a document"
---

## Use case ##

Retrieve a document for the purpose of migrating it to a patient's new registered practice.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's Access Document FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- **MUST** have previously traced the patient's NHS Number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service
- **MUST** have used the [Migrate a patient's structured record](accessrecord_structured_development_migrate_patient_record.html) to retrieve a list of the patient's documents

## API usage ##

### Interaction diagram ###

<img style="height: 400px;" alt="Retrieve a document interaction diagram" src="images/access_documents/documents-get-patient-document-interaction-diagram.png"/>

### Request ###

#### FHIR&reg; relative request ####

```http
GET /Binary/[id]
```

#### FHIR&reg; absolute request ####

```http
GET https://[proxy_server]/https://[documents_provider_server]/[documents_fhir_base]/Binary/[id]
```

#### Availability of data ####

The record migration use case requires that information is always available regardless of whether the [documents capability has been enabled](development_api_non_functional_requirements.html#enablement), or whether clinical areas have been turned off using [configuration for clinical areas](accessrecord_structured_development_clinical_area_config.html).

#### Confidential and sensitive documents ####

This interaction allows confidential and sensitive documents to be retrieved. This interaction can only be used if an appropriate `requested_scope` value is provided in the JWT, more guidance is available in the  <a href="integration_cross_organisation_audit_and_provenance.html#requested_scope-claim">Cross-organisation audit and provenance page</a>

#### File size limit ####

Documents up to 100MB can be retrieved using this interaction.

#### Request headers ####

Consumers **MUST** include the following additional HTTP request headers:

| Header               | Value                                                                   |
| ------               | -----                                                                   |
| `Ssp-TraceID`        | Consumer's Trace ID (a GUID or UUID)                                    |
| `Ssp-From`           | Consumer's ASID                                                         |
| `Ssp-To`             | Provider's ASID                                                         |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:documents:fhir:rest:migrate:binary-1` |

Example HTTP request headers:

```http
Accept: application/fhir+json;charset=utf-8
Content-Type: application/fhir+json;charset=utf-8
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect:documents:fhir:rest:migrate:binary-1
```

#### Payload request body ####

N/A

#### Error handling ####

The provider system **MUST** return a `GPConnect-OperationOutcome-1` resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shown common errors that may be encountered during this API call, and the returned Spine error code. Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response or to determine the response for errors encountered that are not shown below.

Errors returned due to query parameter failure **MUST** include diagnostic information detailing the invalid query parameter.

| Error encountered                                                                                                                             | Spine error code returned                                                                     |
| -----------------                                                                                                                             | -------------------------                                                                     |
| A document could not be found with the document id provided                                                                                   | [`NO_RECORD_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The document could not be retrieved due to it exceeding the file size limit                                                                   | [`NO_RECORD_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| GP Connect is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement))                     | [`ACCESS DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors)   |
| The Access Document capability is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors)   |
| An unauthorised request has been made for sensitive information                                                                               | [`NOT_AUTHORISED`](development_fhir_error_handling_guidance.html#security-validation-errors)  |
| The ODS code in the JWT doesn't match the ODS code for the patient's registered practice on PDS                                               | [`NOT_AUTHORISED`](development_fhir_error_handling_guidance.html#security-validation-errors)  |
| The JWT `requested_scope` is set to `conf/N` when a request has been made for sensitive information                                           | [`NOT_AUTHORISED`](development_fhir_error_handling_guidance.html#security-validation-errors)  |

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR® standards.

#### Payload response body ####

Provider systems **MUST**:

- return a `200` **OK** HTTP status code to indicate successful execution of the operation
- return a `Binary` resource conforming to the [`Binary`](access_documents_development_binary.html) resource definition
- include the `versionId` of the current version of the `Binary` resource

#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [Documents - FHIR&reg; examples](access_documents_development_fhir_examples_documents.html)
