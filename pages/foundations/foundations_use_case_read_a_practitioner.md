---
title: Read a practitioner
keywords: foundations, practitioner, sdsuserid
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_read_a_practitioner.html
summary: "Use case for reading a practitioner resource"
---

## API use case ##

This page describes a single use case. For complete details and background please see the [Foundations Capability Bundle](foundations.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /Practitioner/[id]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Practitioner/[id]
```

#### Request headers ####

Consumer applications **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:practitioner-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems **SHALL** return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

For example, the:

- Logical identifier of the resource is not valid/can't be found on the server.  

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful execution of the operation.
- **SHALL** return `Practitioner` resources that conform to the [CareConnect-GPC-Practitioner-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1) profile.

- **SHALL** populate the following `Practitioner` fields:
  - `meta.profile` with the profile URI
  - `versionId` with the current version of the `Practitioner` resource.
  - `identifier` with relevant business identifiers (for example, SDS User Id) for each `Practitioner` resource.
  - `name`
  - `gender` where available
  - `nhsCommunication` with the practitioner's language information, where available

- **SHALL** meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields where data is available, excluding those listed below

- **SHALL NOT** populate the following fields:
  - `telecom`
  - `address`
  - `birthDate`
  - `photo`
  - `qualification`

```json
{
  "resourceType": "Practitioner",
  "id": "15",
  "meta": {
    "versionId": "636064088099800115",
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1"
    ]
  },
  "identifier": [
    {
      "system": "https://fhir.nhs.uk/Id/sds-user-id",
      "value": "S001"
    }
  ],
  "name": [
    {
      "family": "Black",
      "given": [
        "Sarah"
      ],
      "prefix": [
        "Mrs"
      ]
    }
  ],
  "gender": "female"
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Read<Practitioner>("Practitioner/15");
FhirSerializer.SerializeResourceToXml(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = new FhirContext().forStu3();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
Practitioner practitioner = client.read().resource(Practitioner.class).withId("15").execute();
```
