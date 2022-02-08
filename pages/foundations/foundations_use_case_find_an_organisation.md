---
title: Find an organisation
keywords: foundations, organisation, ods, odscode
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_an_organisation.html
summary: "Use case for finding an organisation resource by business identity"
---

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API usage ##

Resolve (zero or more) `Organization` resources using a business identifier (for example, ODS organization code).

### Request operation ###

The consumer system:

- SHALL populate the `[system]` field with a valid organization identifier system URL (for example, `https://fhir.nhs.uk/Id/ods-organization-code`).

- apply percent encoding when constructing the request URL as indicated in [RFC 3986 Section 2.1](https://tools.ietf.org/html/rfc3986#section-2.1). This will ensure that downstream servers correctly handle the pipe `|` character which must be used in the `identifier` parameter value below.

{% include important.html content="GP Connect can only guarantee a successful response for searches using the identifier type `https://fhir.nhs.uk/Id/ods-organization-code`. Other identifier types may result in an error response if the provider does not recognise or support the identifier." %}

#### FHIR relative request ####

```http
GET /Organization?identifier=[system]|[value]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Organization?identifier=[system]|[value]
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (for example, GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization-1`|

#### Payload request body ####

N/A

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation
- SHALL return zero or more matching `Organization` resources in a `Bundle` of `type` searchset
- SHALL return `Organization` resources that conform to the [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) profile

- SHALL populate the following `Organization` fields:
  - `meta.profile` with the profile URI
  - `versionId` with the current version of each `Organization` resource.
  - `identifier` with relevant business identifiers (for example, ODS code) for each `Organization` resource.
  - `name`
  - `address` where available
  - `telecom` where available

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields where data is available, excluding those listed below

- SHALL NOT populate the following fields:
  - `contact`
  - `endpoint`

#### Error handling ####

Provider systems:

- SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached

For example, the:

- Business identifier `[system]` is not recognised/supported by the provider system
- Business identifier fails any structural validation checks (for example, length and check digits)

{% include important.html content="Failure to find a record with the supplied business identifier is not considered an error condition." %}


### Examples ###

#### Find an organisation by ODS organisation code ####

##### Request #####

```http
{% include foundations/find-organization-request-header-1.txt %}
```

##### Response #####

```json
{% include foundations/find-organization-response-payload-1a.json %}
```

##### Response when no organisation is found #####

```json
{% include foundations/find-organization-response-payload-1b.json %}
```
