---
title: Medication Statement
keywords: getcarerecord, structured, section, medication, statement
tags: [structured,getcarerecord]
sidebar: accessrecord_rest_sidebar
permalink: accessrecord_rest_structured_data_medicationstatement.html
summary: "Medication Statement"
---

## Medication Statement ##

Search for all medication statement resources for a patient. Fetches a bundle of all `MedicationStatement` resources for the specified patient.

This specification describes a single use cases. For complete details and background please see the [Access Record REST Capability Bundle](accessrecord_rest.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Search Parameters ##

Provider systems SHOULD implement all [search parameters for the `MedicationStatement` resource](https://www.hl7.org/fhir/DSTU2/medicationstatement.html#search){:target="_blank"}

Provider systems SHALL implement the following search parameters:

| Name | Type | Description | Paths |
| `code` | `token` | Return administrations of this medication code | `MedicationStatement.medicationCodeableConcept` |
| `effectivedate` | `date` | Date when patient was taking (or not taking) the medication | `MedicationStatement.effective[x]` |
| `medication` | `reference` | Return administrations of this medication reference | `MedicationStatement.medicationReference (Medication)` |
| `patient` | `reference` | The identity of a patient to list statements for | `MedicationStatement.patient (Patient)` |
| `status` | `token` | Return statements that match the given status | `MedicationStatement.status` |

In order to manage the number of search results returned, the server may choose to return the results in a series of pages. The search result set contains the URLs that the client uses to request additional pages from the search set. For a simple RESTful search, the page links are contained in the returned bundle as links. Please refer to [Paged Search](https://www.hl7.org/fhir/DSTU2/search.html#count){:target="_blank"} for further details.

Provider systems SHALL return an error for any unknown or unsupported parameter inline with the `Prefer: handling=strict` search behavior.

{% include note.html content="Provider systems SHALL NOT represent the medication with an external reference to a `Medication` resource but SHALL represents the medication using either an inline code or a contained `Medication` resource." %}

### List Search Mechanism ###

Provider systems SHALL implement [_list](https://www.hl7.org/fhir/DSTU2/search.html#list) search mechanism.

Provider systems SHALL implement the standard [current resource list](https://www.hl7.org/fhir/lifecycle.html#current) for the `MedicationStatement` resource:

- `$current-medications` A list of all medications that the patient is taking.

On the RESTful API, this is done using the [list search mechanism](https://www.hl7.org/fhir/DSTU2/search.html#list) as follows:

```http
GET [base]/MedicationStatement?patient=[id]&_list=$current-medications
```

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service.
- SHALL have resolved the patient's logical id on the server using the patient's NHS Number.

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
GET /MedicationStatement?patient=[id]{&other search parameters}
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/MedicationStatement?patient=[id]{&other search parameters}
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:claim:patient/MedicationStatement.read-1`|

Example HTTP request headers:

```http
```

#### Payload Request Body ####

N/A

#### Error Handling ####

The Provider system SHALL return an error if:

- the `id` is invalid (i.e. no `Patient` resource with that logical id exists on the server).

Provider systems SHALL return an [OperationOutcome](http://www.hl7.org/fhir/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

Refer to [Development - FHIR Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

```http
TODO
```

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned response.

```json
TODO
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

#### Example 1. Retrieve all medication statements for a patient ####

```csharp
var client = new FhirClient("https://fhirtest.uhn.ca/baseDstu2");
client.PreferredFormat = ResourceFormat.Json;
var query = new string[] { "patient=42" };
var bundle = client.Search<MedicationStatement>(query);
bundle.Entry.Count().Dump();
FhirSerializer.SerializeResourceToJson(bundle).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
TODO
```





