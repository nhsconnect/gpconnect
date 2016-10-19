---
title: Find a practitioner
keywords: foundations, practitioner, sds, sdsuserid
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_a_practitioner.html
summary: "Use case for finding a practitioner resource by business identity."
---

## API Usage ##

Resolve (zero or more) `Practitioner` resources using a business identifier (i.e. SDS User Id).

### Request Operation ###

The `[system]` field SHALL be populated with a valid practitioner identifier system URL (i.e. `http://fhir.nhs.net/Id/sds-user-id`).

#### FHIR Relative Request ####

```http
GET /Practitioner?identifier=[system]|[value]
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Practitioner?identifier=[system]|[value]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `SSP-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `SSP-From`           | Consumer's ASID |
| `SSP-To`             | Provider's ASID |
| `SSP-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:practitioner`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems:

- SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached.

For example the:

- Business identifier `[system]` is not recognised/supported by the Provider system.
- Business identifier fails any structural validation checks (i.e. length and check digits).

{% include important.html content="Failure to find a record with the supplied business identifier is not considered an error condition." %}

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return zero or more matching `Practitioner` resources in a `Bundle` of `type` searchset.
- SHALL return `Practitioner` resources that conform to the `gpconnect-practitioner-1` profile.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned `Practitioner` resources.
- SHALL include the `versionId` and `fullUrl` of the current version of each `Practitioner` resource.
- SHALL include all relevant business `identifier` details (i.e. SDS User Id) for each `Practitioner` resource.

```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "http://gpconnect.fhir.nhs.net/fhir/fhir/Practitioner/1/_history/636064088099800115",
		"resource": {
			"resourceType": "Practitioner",
			"id": "1",
			"meta": {
				"versionId": "636064088099800115",
				"lastUpdated": "2016-08-10T13:47:09.966+01:00",
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-practitioner-1"]
			},
			"identifier": [{
				"system": "http://fhir.nhs.net/Id/sds-user-id",
				"value": "S001"
			}],
			"name": {
				"family": ["Black"],
				"given": ["Sarah"],
				"prefix": ["Mrs"]
			},
			"gender": "female"
		}
	}]
}
```

## Example Code ##

### C# ###

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
var query = new string[] { "identifier=http://fhir.nhs.net/Id/sds-user-id|S001" };
var bundle = client.Search("Practitioner", query);
FhirSerializer.SerializeResourceToJson(bundle).Dump();
```

### Java ###

```java
FhirContext ctx = new FhirContext();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.fhir.nhs.net/fhir/");
Bundle bundle = client.search().forResource(Practitioner.class)
.where(new TokenClientParam("identifier").exactly().systemAndCode("http://fhir.nhs.net/Id/sds-user-id", "S001"))
.encodedJson()
.execute();
```
