---
title: Read a location
keywords: foundations, location, nhsnumber, pid, read
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_read_a_location.html
summary: "Use case for reading a location resource."
---

## API Use Case ##

This specification describes a single use cases. For complete details and background please see the [Foundations Capability Bundle](foundations.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
GET /Location/[id]
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Location/[id]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `SSP-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `SSP-From`           | Consumer's ASID |
| `SSP-To`             | Provider's ASID |
| `SSP-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:location`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

For example the:

- Logical identifier of the resource is not valid/can't be found on the server.  

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return `Location` resources that conform to the `gpconnect-location-1` profile.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned `Location` resource.
- SHALL include the `versionId` of the current version of the `Location` resource.
- SHALL include all relevant business `identifier` details (i.e. ODS Site Code) for the `Location` resource.

```json
{
	"resourceType": "Location",
	"id": "1",
	"meta": {
		"versionId": "636064088100870233",
		"lastUpdated": "2016-08-10T14:27:49.778+01:00",
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-location-1"]
	},
	"identifier": [{
		"system": "http://fhir.nhs.net/Id/ods-site-code",
		"value": "L001"
	}],
	"name": "Honley Highstreet"
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Read<Location>("Location/1");
FhirSerializer.SerializeResourceToXml(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
Hello World
```