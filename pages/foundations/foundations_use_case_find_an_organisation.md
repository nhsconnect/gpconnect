---
title: Find an organisation
keywords: foundations, organisation, ods, odscode
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_an_organisation.html
summary: "Use case for finding an organisation resource by business identity."
---

## API Usage ##

Resolve (zero or more) `Organization` resources using a business identifier (i.e. SDS User Id).

### Request Operation ###

The `[system]` field SHALL be populated with a valid organization identifier system URL (i.e. `http://fhir.nhs.net/Id/ods-organization-code` or `http://fhir.nhs.net/Id/ods-site-code`).

#### FHIR Relative Request ####

```http
GET /Organization?identifier=[system]|[value]
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Organization?identifier=[system]|[value]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization`|

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
- SHALL return zero or more matching `Organization` resources in a `Bundle` of `type` searchset.
- SHALL return `Organization` resources that conform to the `gpconnect-organization-1` profile.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned `Organization` resources.
- SHALL include the `versionId` and `fullUrl` of the current version of each `Organization` resource.
- SHALL include all relevant business `identifier` details (i.e. ODS Code, ODS Site Code etc.) for each `Organization` resource.

```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "http://gpconnect.fhir.nhs.net/fhir/Organization/1/_history/636064088098730113",
		"resource": {
			"resourceType": "Organization",
			"id": "1",
			"meta": {
				"versionId": "636064088098730113",
				"lastUpdated": "2016-08-10T13:52:54.516+01:00",
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-organization-1"]
			},
			"identifier": [{
				"system": "http://fhir.nhs.net/Id/ods-organization-code",
				"value": "O001"
			}],
			"name": "Honley GP Practice"
		}
	}]
}
```

## Example Code ##

### C# ###

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
var query = new string[] { "identifier=http://fhir.nhs.net/Id/ods-organization-code|O001" };
var bundle = client.Search("Organization", query);
FhirSerializer.SerializeResourceToJson(bundle).Dump();
```

### Java ###

```java
FhirContext ctx = new FhirContext();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.fhir.nhs.net/fhir/");
Bundle bundle = client.search().forResource(Organization.class)
.where(new TokenClientParam("identifier").exactly().systemAndCode("http://fhir.nhs.net/Id/ods-organization-code", "O001"))
.encodedJson()
.execute();
```
