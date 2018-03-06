---
title: Find a patient
keywords: foundations, patient, nhsnumber, pid
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_find_a_patient.html
summary: "Use case for finding a patient resource by business identity"
---

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service

## API usage ##

Resolve (zero or more) `Patient` resources using a business identifier (that is, NHS number).

### Request Operation ###

The `[system]` field SHALL be populated with a valid patient identifier system URL (that is, `https://fhir.nhs.uk/Id/nhs-number`).

The consumer system SHALL apply percent encoding when constructing the request URL as indicated in [RFC 3986 Section 2.1](https://tools.ietf.org/html/rfc3986#section-2.1). This will ensure that downstream servers correctly handle the pipe `|` character, which must be used in the `identifier` parameter value below.

{% include important.html content="GP Connect can only guarantee a successful response for searches using the identifier type 'https://fhir.nhs.uk/Id/nhs-number'. Other identifier types may result in an error response if the provider does not recognise or support the identifier." %}

#### FHIR relative request ####

```http
GET /Patient?identifier=[system]|[value]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient?identifier=[system]|[value]
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems:

- SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached

For example the:

- business identifier `[system]` is not recognised/supported by the Provider system
- business identifier fails structural validation checks (that is, not enough digits to be a valid NHS number)

{% include important.html content="Failure to find a record with the supplied business identifier is not considered an error condition." %}

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return zero or more matching `Patient` resources in a `Bundle` of `type` searchset.
- SHALL only return `Patient` resources for `Active` patients ([Definition of a GP Connect Active Patient](overview_glossary.html#active-patient)).
- SHALL return `Patient` resources that conform to the [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) profile.
- SHALL include the URI of the `CareConnect-GPC-Patient-1` profile StructureDefinition in the `Patient.meta.profile` element of the returned `Patient` resources.
- SHALL include the `versionId` and `fullUrl` of the current version of each `Patient` resource.
- SHALL include all relevant business `identifier` details (that is, NHS number) for each `Patient` resource.
- SHALL supply gender, name and birth date where these are available (as indicated by the [Must-Support](https://www.hl7.org/fhir/STU3/conformance-rules.html#mustSupport) FHIR property)
- SHOULD populate the preferred branch surgery within the registration details extension of the patient resource with a reference to a location resource which represents the patients preferred branch surgery including ODS Site Code where available OR the GP Practice where they are registered if there is no preferred branch surgery.
- The patient resource SHALL contain at least a single name element. The patient resource SHALL contain a single instance of the name element with the `use` of `official`. This official name should contain the name registered on the spine which is returned by a PDS lookup for the patient.


```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "http://gpconnect.aprovider.nhs.net/GP001/STU3/1/Patient/2",
		"resource": {
			"resourceType": "Patient",
			"id": "2",
			"meta": {
				"versionId": "1469448000000",
				"lastUpdated": "2016-07-25T12:00:00.000+00:00",
				"profile": [
					"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"
				]
			},
			"extension": [{
							"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-RegistrationDetails-1",
							"extension": [
								{
									"url": "preferredBranchSurgery",
									"valueReference": {
										"reference": "Location/785b4ff5-aced-4bdf-b7ed-34f92131ce97"
									}
								}
							]
						}],
			"identifier": [
				{
					"extension": [
						{
							"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-NHSNumberVerificationStatus-1",
							"valueCodeableConcept": {
								"coding": [
									{
										"system": "https://fhir.nhs.uk/CareConnect-NHSNumberVerificationStatus-1",
										"code": "01",
										"display": "Number present and verified"
									}
								]
							}
						}
					],
					"system": "https://fhir.nhs.uk/Id/nhs-number",
					"value": "9476719931"
				}
			],
			"active": true,
			"name": [
				{
					"use": "official",
					"text": "Minnie DAWES",
					"family": "Jackson",
					"given": ["Jane"],
					"prefix": ["Miss"]
				}
			],
			"telecom": [
				{
					"system": "phone",
					"value": "01454587554",
					"use": "home"
				}
			],
			"gender": "female",
			"birthDate": "1952-05-31",
			"address": [
				{
					"use": "home",
					"type": "physical",
					"text": "Trevelyan Square, Boar Ln, Leeds, LS1 6AE"
					"address": {
						"line": [
							"Trevelyan Square",
							"Boar Ln",
							"Leeds"
						],
						"postalCode": "LS1 6AE"
					}
				}
			]
		}
	}]
}
```

## Example Code ##

### C# ###

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var query = new string[] { "identifier=https://fhir.nhs.uk/Id/nhs-number|9476719931" };
var bundle = client.Search("Patient", query);
FhirSerializer.SerializeResourceToXml(bundle).Dump();
```

### Java ###

```java
FhirContext ctx = new FhirContext();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
Bundle bundle = client.search().forResource(Patient.class)
.where(new TokenClientParam("identifier").exactly().systemAndCode("https://fhir.nhs.uk/Id/nhs-number", "9476719931"))
.encodedXml()
.execute();
```

### cURL ###

{% include embedcurl.html title="Find a patient" command="curl -X GET -H 'Ssp-From: 0001' -H 'Ssp-To: 0002' -H 'Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:rest:search:patient-1' -H 'Cache-Control: no-cache' -H 'Ssp-TraceID: e623b4de-f6bb-be0c-956d-c4ded0d58fc0' 'http://gpconnect.aprovider.nhs.net/GP001/STU3/1/Patient?identifier=https://fhir.nhs.uk/Id/nhs-number%7CP002'" %}
