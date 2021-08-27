---
title: Find a healthcare service
keywords: foundations, service, DOS
tags: [foundations, use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_a_healthcareservice.html
summary: "Use case for finding a healthcare service resource by business identifier"
---

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API use case ##

Search for a healthcare service by business identifier.

{% include note.html content="This interaction is used to retrieve healthcare services that have been defined by the provider organisation to support [appointment service ID filtering](appointments_serviceid_filtering.html)." %}

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorisation
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details.

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /HealthcareService{?identifier=[system]|[value]}
```


#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/HealthcareService{?identifier=[system]|[value]}
```

#### Request headers ####

Consumers **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's trace ID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:healthcareservice-1`|

#### Payload request body ####

*(n/a)*

#### Error handling ####

The provider system **SHALL** return a `GPConnect-OperationOutcome-1` resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shown common errors that may be encountered during this API call, and the returned Spine error code. Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response or to determine the response for errors encountered that are not shown below.

Errors returned due to query parameter failure **SHALL** include diagnostic information detailing the invalid query parameter.

|-------------------------|-------------------|
| Error encountered        | Spine error code returned |
|-------------------------|-------------------|
| The identifier parameter token could not be parsed | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| GP Connect is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS_DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| The Foundations capability is not enabled at the practice (see [Enablement](development_api_non_functional_requirements.html#enablement)) | [`ACCESS_DENIED`](development_fhir_error_handling_guidance.html#security-validation-errors) |
|-------------------------|-------------------|

{% include important.html content="If no matching `HealthcareService` resources are found, this is not treated as an error and an empty `Bundle` is returned instead, which is the default behaviour for a [FHIR search](https://www.hl7.org/fhir/STU3/search.html) endpoint." %}

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond those described in the HTTP and FHIR standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful execution of the operation

- **SHALL** find matching services in the provider organisation's [service list](appointments_serviceid_configuration.html#service-list) in their service ID filtering configuration
  - except where the service ID filtering [organisation switch](appointments_serviceid_configuration.html#organisation-switch) is set to OFF

  {% include note.html content="If the [organisation switch](appointments_serviceid_configuration.html#organisation-switch) is set to OFF, the service list is treated as being empty for the purposes of this interaction." %}

- **SHALL** return zero or more matching `HealthcareService` resources in a `Bundle` of `type` searchset

- **SHALL** return `HealthcareService` resource that conform to the [CareConnect-GPC-HealthcareService-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-HealthcareService-1) profile

- **SHALL** populate the following `HealthcareService` fields:
  - `id` with a logical identifier in accordance with the [FHIR specification requirements](https://www.hl7.org/fhir/STU3/resource.html#id)
  - `meta` with:
    - `versionId` with the current version of the resource
    - `profile` with the profile URI
  - `identifier` with the DOS service ID (see [FHIR resources](datalibraryfoundation.html#common-identifier-systems) for population of the identifier.system field)
  - `providedBy` with a reference to the organisation providing the service
  - `name` with the service's name


### Examples ###

#### Search with identifier parameter ####

Searching with an identifier parameter returns all `HealthcareService` resources with matching the identifier value.

##### Request #####

```http
{% include foundations/find_healthcareservice_request_example_1.txt %}
```

##### Response when a matching resource is found #####

```json
{% include foundations/find_healthcareservice_response_example_1a.json %}
```

##### Response when a matching resource is not found #####

```json
{% include foundations/find_healthcareservice_response_example_1b.json %}
```


#### Search without parameters ####

Searching without parameters returns all `HealthcareService` resources.

##### Request #####

```http
{% include foundations/find_healthcareservice_request_example_2.txt %}
```

##### Response #####

```json
{% include foundations/find_healthcareservice_response_example_2.json %}
```
