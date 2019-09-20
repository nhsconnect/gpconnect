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
| `_include= DocumentReference:patient` | Include `Practitioner` resources referenced within the returned `Schedule` resources | `Schedule.actor:Practitioner` |
| `_include= DocumentReference:custodian:Organization` | Include `Location` resources referenced within the returned `Schedule` resources | `Schedule.actor:Location` |
| `_include= DocumentReference:author:Organization` | Include `Organization` resources references from matching `Location` resources | `Location.managingOrganization` |

Consumer systems SHALL send the following parameters in the request:

TODO: Add guidance on how parameters should be populated

Consumer systems SHOULD send the following parameters in the request:

- `searchFilter` parameters - see [Enhanced slot filtering](#enhanced-slot-filtering).




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
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/DocumentReference?[subject={PatientNHSNumber}]
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



#### Error handling ####

The provider system **MUST** return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shown common errors that may be encountered during this API call, and the returned Spine error code.  Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response, or to determine the response for errors encountered that are not shown below.

Errors returned due to parameter failure **MUST** include diagnostic information detailing the invalid parameter.

|-------------------------|-------------------|
| Error encountered        | Spine error code returned |
|-------------------------|-------------------|
| The `Parameters` resource passed does not conform to that specified in the [GPConnect-GetStructuredRecord-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1) `OperationDefinition` | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The provider could not parse the `Parameters` resource.  | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `patientNHSNumber` parameter is not provided | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `patientNHSNumber` parameter value is invalid, for example it fails format or check digit tests | [`INVALID_NHS_NUMBER`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The `medicationSearchFromDate` part parameter contains a partial date, or has a value containing a time or offset component | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `medicationSearchFromDate` part parameter is greater than the current date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeAllergies` parameter is passed without the corresponding `includeResolvedAllergies` part parameter | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeMedication` parameter is passed without the corresponding `includePrescriptionIssue` part parameter | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `consultationSearchPeriod` part parameter is greater than the current date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The end date of the `consultationSearchPeriod` part parameter is greater than the start date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `consultationSearchPeriod` and `includeNumberOfMostRecent` part parameters are both populated  | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `uncategorisedDataSearchPeriod` part parameter is greater than the current date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The end date of the `uncategorisedDataSearchPeriod` part parameter is greater than the start date | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeStatus` part parameter contains a value other than `active` or `inactive` | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `includeSignificance` part parameter contains a value other than `major` or `minor` | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
|The `filterResults` parameter is passed with a code from a code system other than SNOMED CT | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
|The `resultSearchPeriod` parameter value contains a partial date, or has a value containing a time or offset component | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The patient has dissented to sharing their clinical record | [`NO_PATIENT_CONSENT`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| A patient could not be found matching the `patientNHSNumber` provided | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for the record of an [inactive](overview_glossary.html#active-patient) or deceased patient | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for the record of a non-Regular/GMS patient (i.e. the patient’s registered practice is somewhere else) | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The patient's NHS number in the provider system is not associated with a NHS number status indicator code of 'Number present and verified' | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for a sensitive patient | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
|-------------------------|-------------------|


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

- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- return a `Bundle` conforming to the [`GPConnect-Searchset-Bundle-1`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1) profile definition
- return the following resources in the `Bundle`:
  - `Patient` matching the NHS Number sent in the body of the request
  - `Organization` matching the patient's registered GP practice, referenced from `Patient.generalPractitioner`
  - `Organization` matching the organisation serving the request, if different from above, referenced from `Patient.managingOrganization`
  - `Practitioner` matching the patient's usual GP, if they have one, referenced from `Patient.generalPractitioner`
  - `PractitionerRole` matching the usual GP's role
  - `OperationOutcome` containing warnings about any unsupported parameters
  - resources holding consultations, problems, immunisations, allergies, intolerance, medication and uncategorised data according to the rules below:

Provider systems **SHOULD**:




- `Organization`, `Practitioner` and `PractitionerRole` resources that are referenced by the resources above



#### Payload response examples ####

Examples of the payload requests and responses can be found here:

- [Allergies - FHIR&reg; examples](accessrecord_structured_development_fhir_examples_allergies.html)
