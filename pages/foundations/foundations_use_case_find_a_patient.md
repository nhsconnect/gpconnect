---
title: Find a patient
keywords: foundations, patient, nhsnumber, pid
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_a_patient.html
summary: "Use case for finding a patient resource by business identity."
---

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service.

## API Usage ##

Resolve (zero or more) `Patient` resources using a business identifier (i.e. NHS Number).

### Request Operation ###

The `[system]` field SHALL be populated with a valid patient identifier system URL (i.e. `https://fhir.nhs.uk/Id/nhs-number`).

The consumer systerm SHALL apply percent encoding when constructing the request URL as indicated in [RFC 3986 Section 2.1](https://tools.ietf.org/html/rfc3986#section-2.1). The will ensure that downstream servers correctly handle the pipe `|` character which must be used in the `identifier` parameter value below.

{% include important.html content="GP Connect can only guarantee a successful response for searches using the identifier type 'https://fhir.nhs.uk/Id/nhs-number', other identifier types may result in an error response if the provider does not recognise or support the identifier." %}

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
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient`|

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
- SHALL only return `Patient` resources for `Active` patients ([Definition of a GP Connect Active Patient](overview_glossary.html#active-patient)).
- SHALL return `Patient` resources that conform to the `CareConnect-GPC-Patient-1` profile.
- SHALL include the URI of the `CareConnect-GPC-Patient-1` profile StructureDefinition in the `Patient.meta.profile` element of the returned `Patient` resources.
- SHALL include the `versionId` and `fullUrl` of the current version of each `Patient` resource.
- SHALL include all relevant business `identifier` details (i.e. NHS Number) for each `Patient` resource.
- SHALL supply gender, name, birth date or deceased date where these are available (as indicated by the [Must-Support](https://www.hl7.org/fhir/DSTU2/conformance-rules.html#mustSupport) FHIR property)


```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/Patient/2",
		"resource": {
			"resourceType": "Patient",
			"id": "2",
			"meta": {
				"versionId": "636064088097580046",
				"lastUpdated": "2016-08-10T16:52:39.716+01:00",
				"profile": ["https://fhir.nhs.uk/StructureDefinition/CareConnect-GPC-Patient-1"]
			},
			"identifier": [{
				"extension": [{
					"url": "https://fhir.nhs.uk/StructureDefinition/Extension-CareConnect-GPC-NHSNumberVerificationStatus-1",
					"valueCodeableConcept": {
						"coding": [{
							"system": "https://fhir.nhs.uk/CareConnect-NHSNumberVerificationStatus-1",
							"code": "01"
						}]
					}
				}],
				"system": "https://fhir.nhs.uk/Id/nhs-number",
				"value": "9476719931"
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
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/");
client.PreferredFormat = ResourceFormat.Json;
var query = new string[] { "identifier=https://fhir.nhs.uk/Id/nhs-number|9476719931" };
var bundle = client.Search("Patient", query);
FhirSerializer.SerializeResourceToXml(bundle).Dump();
```

### Java ###

```java
FhirContext ctx = new FhirContext();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/");
Bundle bundle = client.search().forResource(Patient.class)
.where(new TokenClientParam("identifier").exactly().systemAndCode("https://fhir.nhs.uk/Id/nhs-number", "9476719931"))
.encodedXml()
.execute();
```

### cURL ###

{% include embedcurl.html title="Find a patient" command="curl -X GET -H 'Ssp-From: 0001' -H 'Ssp-To: 0002' -H 'Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:rest:search:patient' -H 'Cache-Control: no-cache' -H 'Ssp-TraceID: e623b4de-f6bb-be0c-956d-c4ded0d58fc0' 'http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/Patient?identifier=https://fhir.nhs.uk/Id/nhs-number%7CP002'" %}