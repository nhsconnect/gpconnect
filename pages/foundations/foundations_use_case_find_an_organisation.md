---
title: Find an organisation
keywords: foundations, organisation, ods, odscode
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_an_organisation.html
summary: "Use case for finding an organisation resource by business identity."
---

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)

## API Usage ##

Resolve (zero or more) `Organization` resources using a business identifier (i.e. ODS organization code).

### Request Operation ###

The `[system]` field SHALL be populated with a valid organization identifier system URL (i.e. `https://fhir.nhs.uk/Id/ods-organization-code`).

The consumer systerm SHALL apply percent encoding when constructing the request URL as indicated in [RFC 3986 Section 2.1](https://tools.ietf.org/html/rfc3986#section-2.1). The will ensure that downstream servers correctly handle the pipe `|` character which must be used in the `identifier` parameter value below.

{% include important.html content="GP Connect can only guarantee a successful response for searches using the identifier type 'https://fhir.nhs.uk/Id/ods-organization-code', other identifier types may result in an error response if the provider does not recognise or support the identifier." %}

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
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:organization-1`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems:

- SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached.

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
- SHALL return `Organization` resources that conform to the [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) profile.
- SHALL include the URI of the `CareConnect-GPC-Organization-1` profile StructureDefinition in the `Organization.meta.profile` element of the returned `Organization` resources.
- SHALL include the `versionId` and `fullUrl` of the current version of each `Organization` resource.
- SHALL include all relevant business `identifier` details (i.e. ODS Code) for each `Organization` resource.

```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "http://gpconnect.aprovider.nhs.net/GP001/STU3/1/Organization/23",
		"resource": {
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
	}]
}
```

## Example Code ##

### C# ###

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var query = new string[] { "identifier=https://fhir.nhs.uk/Id/ods-organization-code|O001" };
var bundle = client.Search("Organization", query);
FhirSerializer.SerializeResourceToJson(bundle).Dump();
```

### Java ###

```java
FhirContext ctx = new FhirContext();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
Bundle bundle = client.search().forResource(Organization.class)
.where(new TokenClientParam("identifier").exactly().systemAndCode("https://fhir.nhs.uk/Id/ods-organization-code", "O001"))
.encodedJson()
.execute();
```
