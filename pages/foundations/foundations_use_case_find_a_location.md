---
title: Find a location
keywords: foundations, location, ods, odssitecode, find
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_a_location.html
summary: "Use case for finding a location resource by business identity."
---

## API Usage ##

Resolve (zero or more) `Location` resources using a business identifier (i.e. ODS Site Code).

### Request Operation ###

The `[system]` field SHALL be populated with a valid location identifier system URL (i.e. `http://fhir.nhs.net/Id/ods-site-code`).

#### FHIR Relative Request ####

```http
GET /Location?identifier=[system]|[value]
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Location?identifier=[system]|[value]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `SSP-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `SSP-From`           | Consumer's ASID |
| `SSP-To`             | Provider's ASID |
| `SSP-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:location`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems:

- SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached.

For example the:

- Business identifier `[system]` is not recognised/supported by the Provider system.
- Business identifier fails structural validation checks (i.e. not enough digits to be a valid ODS Site Code).

{% include important.html content="Failure to find a record with the supplied business identifier is not considered an error condition." %}

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return zero or more matching `Location` resources in a `Bundle` of `type` searchset.
- SHALL return `Location` resources that conform to the `gpconnect-location-1` profile.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned `Location` resources.
- SHALL include the `versionId` and `fullUrl` of the current version of each `Location` resource.
- SHALL include all relevant business `identifier` details (i.e. ODS Site Code) for each `Location` resource.

```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "http://gpconnect.fhir.nhs.net/fhir/Location/1/_history/636064088100870233",
		"resource": {
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
	}]
}
```

## Example Code ##

### C# ###

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
var query = new string[] { "identifier=http://fhir.nhs.net/Id/ods-site-code|L001" };
var bundle = client.Search("Location", query);
FhirSerializer.SerializeResourceToXml(bundle).Dump();
```

### Java ###

```java
FhirContext ctx = new FhirContext();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.fhir.nhs.net/fhir/");
Bundle bundle = client.search().forResource(Location.class)
.where(new TokenClientParam("identifier").exactly().systemAndCode("http://fhir.nhs.net/Id/ods-site-code", "L001"))
.encodedXml()
.execute();
```