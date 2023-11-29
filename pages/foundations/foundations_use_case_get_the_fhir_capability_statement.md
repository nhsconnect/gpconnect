---
title: Get the FHIR&reg; capability statement
keywords: foundations, fhir
tags: [foundations,use_case,fhir]
sidebar: foundations_sidebar
permalink: foundations_use_case_get_the_fhir_capability_statement.html
summary: "Use case for getting the GP Connect FHIR server's capability statement"
---

## Prerequisites ##

### Consumer ###

The consumer system:

- **SHALL** have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /metadata
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/metadata
```

#### Request headers ####

Consumers **SHALL** include the following additional HTTP request headers:

| Header              | Value                                                        |
| ------              | -----                                                        |
| `Ssp-TraceID`       | Consumer's TraceID (i.e. GUID/UUID)                          |
| `Ssp-From`          | Consumer's ASID                                              |
| `Ssp-To`            | Provider's ASID                                              |
| `Ssp-InteractionID` | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata-1` |

#### Payload request body ####

N/A

#### Error handling ####

Provider systems are expected to always be able to return a valid capability statement.

### Request response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful retrieval of the capability statement
- **SHALL** return a capability statement which conforms to the standard [FHIR CapabilityStatement](http://hl7.org/fhir/STU3/capabilitystatement.html)

An example GP Connect CapabilityStatement is shown below ready for customisation and embedding into GP Connect assured provider systems. Providers should use this CapabilityStatement as a base for their own CapabilityStatement, replacing the element in square brackets (`[` & `]`) with specific information of their implementation. The main version at the top of the CapabilityStatement should represent the GP Connect specification version which the FHIR server implements.

```json
{% include foundations/get_capability_statement_response_example.json %}
```

Consumer systems:

- **SHOULD** request the capability statement from the FHIR server endpoint in order to ascertain details of the implementation of GP Connect capabilities delivered by the FHIR server, this includes checking the version number specified in `CapabilityStatement.version`
- Consumers may also cache the capability statement information retrieved from an endpoint to reduce the number of future calls they make to the target organization's FHIR server.
