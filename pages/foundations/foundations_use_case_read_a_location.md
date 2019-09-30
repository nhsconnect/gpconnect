---
title: Read a location
keywords: foundations, location, nhsnumber, pid, read
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_read_a_location.html
summary: "Use case for reading a location resource"
---

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API use case ##

This page describes a single use case. For complete details and background please see the [Foundations Capability Bundle](foundations.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /Location/[id]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Location/[id]
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:location-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

For example, the:

- Logical identifier of the resource is not valid/can't be found on the server.  

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful execution of the operation.
- **SHALL** return `Location` resources that conform to the [CareConnect-GPC-Location-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1) profile.

- **SHALL** populate the following `Location` fields:
  - `meta.profile` with the profile URI
  - `versionId` with the current version of each `Location` resource.
  - `name`
  - `address` where available
  - `telecom` where available
  - `managingOrganization` with a reference to the 'managing' organisation. For Locations that are managed by GP practices, see [Branch surgeries](development_branch_surgeries.html) for more details.

- **SHALL** meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields where data is available, excluding those listed below

- **SHALL NOT** populate the following fields:
  - `endpoint`

```json
{
  "resourceType": "Location",
  "id": "17",
  "meta": {
    "versionId": "636064088100870233",
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1"
    ]
  },
  "name": "Trevelyan Surgery",
  "address": [
    {
      "line": [
        "Trevelyan Square",
        "Boar Ln"
      ],
      "city": "Leeds",
      "district": "West Yorkshire",
      "postalCode": "LS1 6AE"
    }
  ],
  "telecom": [
    {
      "system": "phone",
      "value": "03003035678",
      "use": "work"
    }
  ],
  "managingOrganization": {
    "reference": "Organization/14"
  }
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Read<Location>("Location/17");
FhirSerializer.SerializeResourceToXml(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = new FhirContext().forStu3();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
Location location = client.read().resource(Location.class).withId("17").execute();
```
