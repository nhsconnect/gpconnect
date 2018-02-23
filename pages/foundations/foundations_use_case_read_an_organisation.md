---
title: Read an organisation
keywords: foundations, organisation, sdsuserid
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_read_an_organisation.html
summary: "Use case for reading an organisation resource."
---
## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- MAY have previously [resolved the logical ID of the organisation](https://nhsconnect.github.io/gpconnect/foundations_use_case_find_an_organisation.html) from the ODS Organisation Code.

## API Use Case ##

This specification describes a single use cases. For complete details and background please see the [Foundations Capability Bundle](foundations.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
GET /Organization/[id]
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Organization/[id]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:organization-1`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

For example the:

- Logical identifier of the resource is not valid/can't be found on the server.  

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return `Organization` resources that conform to the [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) profile.
- SHALL include the URI of the `CareConnect-GPC-Organization-1` profile StructureDefinition in the `Organization.meta.profile` element of the returned `Organization` resource.
- SHALL include the `versionId` of the current version of the `Organization` resource.
- SHALL include all relevant business `identifier` details (i.e. ODS Code) for the `Organization` resource.

```json
{
	"resourceType": "Organization",
	"id": "23",
	"meta": {
		"versionId": "636064088098730113",
		"lastUpdated": "2016-08-10T13:52:54.516+01:00",
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"]
	},
	"identifier": [{
		"system": "https://fhir.nhs.uk/Id/ods-organization-code",
		"value": "O001"
	}],
	"name": "Honley GP Practice"
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Read<Organization>("Organization/23");
FhirSerializer.SerializeResourceToXml(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = new FhirContext().forStu3();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
Organization organization = client.read().resource(Organization.class).withId("23").execute();
```