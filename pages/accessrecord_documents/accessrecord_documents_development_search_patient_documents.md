---
title: Search for a patient's documents
keywords: getstructuredrecord, view
tags: [design,structured]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_documents_development_search_patient_documents.html
summary: "Search for a patient's documents"
---

## Use case ##

Search for a patient's documents from a GP practice.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Search parameters ##

Provider systems SHALL support the following search parameters:

| Name | Type | Description | Paths |
|---|---|---|---|
| `subject` | `Patient` | the patient who is the subject of the document. | `DocumentReference.subject` |
| `created` | `date` or `dateTime` | Creation/Edit datetime of the document. | `DocumentReference.created` |
| `facility` | `token` | Additional details about where the content was created (e.g. clinical specialty). | `DocumentReference.clinicalSetting` |
| `author` | `Organization` | Who and/or what authored the document. | `DocumentReference.author` |
| `type` | `token` | Kind of document. | `DocumentReference.type` |
| `custodian` | `Organization` | Organisation which maintains this document. | `DocumentReference.custodian` |
| `description` | `string` | Human-readable description (title). | `DocumentReference.title` |

{% include note.html content="The supported search parameters MUST be included in the [FHIR Capability Statement](foundations_use_case_get_the_fhir_capability_statement.html)." %}

## _include parameters ##

Provider systems SHALL support the following include parameters:

| Name | Description | Paths |
|---|---|---|
| `_include= DocumentReference:patient` | Include `Patient` resources referenced within the returned `DocumentReference` resources | `DocumentReference.patient` |
| `_include= DocumentReference:custodian:Organization` | Include `Organization` resources referenced within the returned `DocumentReference` resources | `DocumentReference.custodian:Organization` |
| `_include= DocumentReference:author:Organization` | Include `Organization` resources references from matching `DocumentReference` resources | `DocumentReference.author` |

Consumer systems MUST send the following parameters in the request:

TODO: Add guidance on how parameters should be populated
- subject **MUST** be included

Consumer systems **SHOULD** send the following parameters in the request:

-  created
- facility
- author
- type

Consumer systems **MAY** send the following parameters in the request:

-  description

## Prerequisites ##

### Consumer ###

The consumer system:

- **MUST** have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- **MUST** have previously traced the patient's NHS Number using the [Personal Demographics Service](https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service

## API usage ##

### Interaction diagram ###

<img style="height: 400px;" alt="Search for patient's documents interaction diagram" src="images/access_structured/search-patient-document-interaction-diagram.png"/>

### Request ###

#### FHIR&reg; relative request ####

```http
GET /DocumentReference?[subject={PatientNHSNumber}]
                       [&created={search_prefix}creation_date]
                       [&facility={OrgTypeCodeSystem}|{OrgTypeCode}]
                       [&author={OrgTypeCodeSystem}|{OrgTypeCode}]
                       [&type={document_type}]
                       [&custodian={OrgTypeCodeSystem}|{OrgTypeCode}]
                       [&description={document_title}]

```

#### FHIR&reg; absolute request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/
                      DocumentReference?[subject={PatientNHSNumber}]
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
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect-documents:fhir:rest:search:documentreference-1`|

Example HTTP request headers:

```http
Accept: application/fhir+json;charset=utf-8
Content-Type: application/fhir+json;charset=utf-8
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect-documents:fhir:rest:search:documentreference-1
```

#### Payload request body ####

n/a

#### Error handling ####

The provider system SHALL return an error if:

- facility contains an identifier other than an ODS code
- author contains an identifier other than an ODS code
- custodian contains an identifier other than an ODS code

SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more parameters are corrupt or a specific business rule/constraint is breached.

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
- return a [`Bundle`](http://hl7.org/fhir/STU3/bundle.html)
- return the following resources in the `Bundle`:
  - `Patient` matching the NHS Number sent in the body of the request
  - `Organization` matching the patient's registered GP practice, referenced from `Patient.generalPractitioner`
  - `Organization` matching the organisation serving the request, if different from above, referenced from `Patient.managingOrganization`
  - `Practitioner` matching the patient's usual GP, if they have one, referenced from `Patient.generalPractitioner`
  - `PractitionerRole` matching the usual GP's role
  - `DocumentReference` resources conforming to the [CareConnect-GPC-DocumentReference-1](accessrecord_structured_development_documents.html) profile that match the supplied search criteria
  - Only `Organization` resources SHALL be returned where they are associated with the `DocumentReference` resources matching the query



#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [Allergies - FHIR&reg; examples](accessrecord_structured_development_fhir_examples_allergies.html)
