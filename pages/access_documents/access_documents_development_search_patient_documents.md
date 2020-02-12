---
title: Search for a patient's documents
keywords: getstructuredrecord, view
tags: [design,structured]
sidebar: access_documents_sidebar
permalink: access_documents_development_search_patient_documents.html
summary: "Search for a patient's documents"
---

## Use case ##

Search for a patient's documents from a GP practice.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Search parameters ##

Provider systems **SHALL** support the following search parameters:

| Name | Type | Description | Paths |
|---|---|---|---|
| `subject` | `Patient` | Reference to the patient who is the subject of the document. | `DocumentReference.subject` |
| `created` | `date` or `dateTime` | Creation/Edit datetime of the document. | `DocumentReference.created` |
| `facility` | `token` | Additional details about where the content was created (for example, clinical specialty). | `DocumentReference.context.practiceSetting` |
| `author` | `Organization` | Who and/or what authored the document. | `DocumentReference.author` |
| `type` | `token` | Kind of document. | `DocumentReference.type` |
| `description` | `string` | Human-readable description (title). | `DocumentReference.title` |

{% include note.html content="The supported search parameters **MUST** be included in the Access Document [FHIR capability statement](access_documents_use_case_get_the_fhir_capability_statement.html)." %}

## _include parameters ##

Provider systems **SHALL** support the following include parameters:

| Name | Description | Paths |
|---|---|---|
| `_include= DocumentReference:patient` | Include `Patient` resources referenced within the returned `DocumentReference` resources | `DocumentReference.patient` |
| `_include= DocumentReference:custodian:Organization` | Details of organisations that are custodians for the documents that are returned in DocumentReference resources |
| `_include= DocumentReference:author:Organization` | Details of organisations that authored the documents that are returned in DocumentReference resources |
| `_include= DocumentReference:author:Practitioner` | Details of organisations that authored the documents that are returned in DocumentReference resources |
| `_revinclude:recurse= PractitionerRole:practitioner` | Include `PractitionerRole` resources referenced from matching `Practitioner` resources | `DocumentReference.author:Practitioner` |

Consumer systems **MUST** send the following parameters in the request:

- subject

Consumer systems **MUST** also send the following parameters to reduce the number of API calls:

- _include= DocumentReference:patient
- _include= DocumentReference:custodian:Organization
- _include= DocumentReference:author:Organization
- _include= DocumentReference:author:Practitioner
- _revinclude:recurse= PractitionerRole:practitioner

Consumer systems **MAY** send the following parameters in the request:

- created
- facility
- author
- type

When using the 'created' parameter, consumers **MUST** do the following
- to search for a lower boundary of a date:
  - a single `created` parameter with a date prefixed by `ge` should be supplied
- to search for a upper boundary of a date:
  - a single `created` parameter with a date prefixed by `le` should be supplied
- to search between two dates:
  - two created parameters should be supplied
    - a single `created` parameter with a date prefixed by `ge`
    - a single `created` parameter with a date prefixed by `le`

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's Access Document FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- **MUST** have previously traced the patient's NHS Number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service

## API usage ##

### Interaction diagram ###

<img style="height: 400px;" alt="Search for patient's documents interaction diagram" src="images/access_documents/search-patient-document-interaction-diagram.png"/>

### Request ###

#### FHIR&reg; relative request ####

```http
GET /DocumentReference?[subject={PatientLogicalId}]
                       (&created={search_prefix}creation_date)
                       (&facility={OrgTypeCodeSystem}|{OrgTypeCode})
                       (&author={OrgTypeCodeSystem}|{OrgTypeCode})
                       (&type={document_type})
                       (&custodian={OrgTypeCodeSystem}|{OrgTypeCode})
                       (&description={document_title})

```

#### FHIR&reg; absolute request ####

```http
GET https://[proxy_server]/https://[access_document_provider_server]/[access_document_fhir_base]/
                      DocumentReference?[subject={PatientLogicalId}]
                      [&created={search_prefix}creation_date]
                      [&facility={OrgTypeCodeSystem}|{OrgTypeCode}]
                      [&author={OrgTypeCodeSystem}|{OrgTypeCode}]
                      [&type={document_type}]
                      [&custodian={OrgTypeCodeSystem}|{OrgTypeCode}]
                      [&description={document_title}]
```

#### Request headers ####

Consumers **MUST** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's Trace ID (a GUID or UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:documents:fhir:rest:search:documentreference-1`|

Example HTTP request headers:

```http
Accept: application/fhir+json;charset=utf-8
Content-Type: application/fhir+json;charset=utf-8
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect:documents:fhir:rest:search:documentreference-1
```

#### Payload request body ####

n/a

#### Error handling ####

The provider system **SHALL** return an error if:

- facility contains an identifier other than an ODS code
- author contains an identifier other than an ODS code
- custodian contains an identifier other than an ODS code

**SHALL** return a [GPConnect-OperationOutcome-1](development_fhir_error_handling_guidance.html) resource that provides additional detail when one or more parameters are corrupt or a specific business rule/constraint is breached.

Refer to [Error handling guidance](development_fhir_error_handling_guidance.html) for details of error codes.


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

Provider systems **MUST**:

- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's documents
- return a [`Bundle`](access_documents_development_bundle.html)
- return the following resources in the `Bundle`:
  - `Patient` matching the NHS Number sent in the body of the request
  - `Organization` matching the patient's registered GP practice, referenced from `Patient.generalPractitioner`
  - `Organization` matching the organisation serving the request, if different from above, referenced from `Patient.managingOrganization`
  - `Practitioner` matching the patient's usual GP, if they have one, referenced from `Patient.generalPractitioner`
  - `PractitionerRole` matching the usual GP's role
  - `DocumentReference` resources conforming to the [CareConnect-GPC-DocumentReference-1](access_documents_development_documentreference.html) profile that match the supplied search criteria
    - where the `created` parameter has been supplied and `DocumentReference.created` doesn't exist, `DocumentReference.indexed` **MUST** be used instead
  - Only `Organization` resources SHALL be returned where they are associated with the `DocumentReference` resources matching the query

#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [Documents - FHIR&reg; examples](access_documents_development_fhir_examples_documents.html)
