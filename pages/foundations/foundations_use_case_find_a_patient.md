---
title: Find a patient
keywords: foundations, patient, nhsnumber, pid
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_a_patient.html
summary: "Use case for finding a patient resource by business identity."
---

## API Usage ##

Resolve (zero or more) `Patient` resources using a business identifier (i.e. NHS Number).

### Request Operation ###

The `[system]` field SHALL be populated with a valid patient identifier system URL (i.e. `http://fhir.nhs.net/Id/nhs-number`).

#### FHIR Relative Request ####

```http
GET /Patient?identifier=[system]|[value]
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient?identifier=[system]|[value]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `SSP-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `SSP-From`           | Consumer's ASID |
| `SSP-To`             | Provider's ASID |
| `SSP-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems:

- SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached.

For example the:

- Business identifier `[system]` is not recognised/supported by the Provider system.
- Business identifier fails structural validation checks (i.e. not enough digits to be a valid NHS Number).

{% include important.html content="Failure to find a record with the supplied business identifier is not considered an error condition." %}

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return zero or more matching `Patient` resources in a `Bundle` of `type` searchset.
- SHALL return `Patient` resources that conform to the `gpconnect-patient-1` profile.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned `Patient` resources.
- SHALL include the `versionId` and `fullUrl` of the current version of each `Patient` resource.
- SHALL include all relevant business `identifier` details (i.e. NHS Number) for each `Patient` resource.

```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "http://gpconnect.fhir.nhs.net/fhir/Patient/2/_history/636064088097580046",
		"resource": {
			"resourceType": "Patient",
			"id": "2",
			"meta": {
				"versionId": "636064088097580046",
				"lastUpdated": "2016-08-10T16:52:39.716+01:00",
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-patient-1"]
			},
			"identifier": [{
				"system": "http://fhir.nhs.net/Id/nhs-number",
				"value": "P002"
			}],
			"name": [{
				"use": "official",
				"family": ["Jackson"],
				"given": ["Jane"],
				"prefix": ["Miss"]
			}],
			"gender": "female",
			"birthDate": "22/02/1982"
		}
	}]
}
```

## Example Code ##

### C# ###

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
var query = new string[] { "identifier=http://fhir.nhs.net/Id/nhs-number|P002" };
var bundle = client.Search("Patient", query);
FhirSerializer.SerializeResourceToXml(bundle).Dump();
```

### Java ###

```java
FhirContext ctx = new FhirContext();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.fhir.nhs.net/fhir/");
Bundle bundle = client.search().forResource(Patient.class)
.where(new TokenClientParam("identifier").exactly().systemAndCode("http://fhir.nhs.net/Id/nhs-number", "P002"))
.encodedXml()
.execute();
```

### cURL ###

{% include embedcurl.html title="Find a patient" command="curl -X GET -H 'SSP-From: 0001' -H 'SSP-To: 0002' -H 'SSP-InteractionID: urn:nhs:names:services:gpconnect:fhir:rest:search:patient' -H 'Cache-Control: no-cache' -H 'SSP-TraceID: e623b4de-f6bb-be0c-956d-c4ded0d58fc0' 'http://gpconnect.fhir.nhs.net/fhir/Patient?identifier=http://fhir.nhs.net/Id/nhs-number%7CP002'" %}