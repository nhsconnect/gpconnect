---
title: Read a healthcare service
keywords: foundations, service, DOS
tags: [foundations, use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_read_a_healthcareservice.html
summary: "Use case for reading a healthcare service resource"
---

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API use case ##

Retrieve a healthcare service by logical id.

{% include note.html content="This interaction is currently used to retrieve healthcare services operated by the provider organisation that have been configured in order to allow searching for appointment slots by DOS service.  For more information see [service ID filtering](appointments_serviceid_filtering.html) in the Appointment Management capability.
It may be generalised in future to allow healthcare services to be retreived for other purposes." %}

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details.

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /HealthcareService/[id]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/HealthcareService/[id]
```

#### Request headers ####

Consumers **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's Trace ID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:healthcareservice-1`|

#### Payload request body ####

*(n/a)*

#### Error handling ####

The provider system **SHALL** return a `GPConnect-OperationOutcome-1` resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shown common errors that may be encountered during this API call, and the returned Spine error code. Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response or to determine the response for errors encountered that are not shown below.

Errors returned due to query parameter failure **SHALL** include diagnostic information detailing the invalid query parameter.

|-------------------------|-------------------|
| Error encountered        | Spine error code returned |
|-------------------------|-------------------|
| A healthcare service could not be found using the id provided | [`NO_RECORD_FOUND`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| Service ID filtering [organisation switch](appointments_serviceid_configuration.html#organisation-switch) is set to OFF  | [`NO_RECORD_FOUND`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| GP Connect is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS_DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| The Foundations capability is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS_DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors) |
|-------------------------|-------------------|

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond those described in the HTTP and FHIR standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful execution of the operation
- **SHALL** return a matching service from the provider organisation's [service list](appointments_serviceid_configuration.html#service-list) in their service ID filtering configuration

- **SHALL** return a `HealthcareService` resource that conforms to the [CareConnect-GPC-HealthcareService-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-HealthcareService-1) profile

- **SHALL** populate the following `HealthcareService` fields:
  - `id` with a logical identifier in accordance with the [FHIR specification requirements](https://www.hl7.org/fhir/STU3/resource.html#id)
  - `meta` with:
    - `versionId` with the current version of the resource
    - `profile` with the profile URI
  - `identifier` with the DOS service ID (see [FHIR resources](datalibraryfoundation.html#common-identifier-systems) for population of the identifier.system field)
  - `providedBy` with a reference to the organisation providing the service
  - `location` with reference to the location at which the service operates
  - `name` with the service's name

```json
{% include foundations/read_healthcareservice_response_example.json %}
```
