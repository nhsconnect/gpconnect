---
title: Read a patient
keywords: foundations, patient, nhsnumber, pid, read
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_read_a_patient.html
summary: "Use case for reading a patient resource."
---

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service.
- SHALL have previously [resolved the logical ID of the patient](https://nhsconnect.github.io/gpconnect/foundations_use_case_find_a_patient.html) on the server using the NHS Number

## API Use Case ##

This specification describes a single use cases. For complete details and background please see the [Foundations Capability Bundle](foundations.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
GET /Patient/[id]
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/[id]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:patient-1`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) ![STU3](images/stu3.png) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

For example the:

- Logical identifier of the resource is not valid/can't be found on the server.  

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return `Patient` resources that conform to the [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) ![STU3](images/stu3.png) profile.
- SHALL include the URI of the `CareConnect-GPC-Patient-1` profile StructureDefinition in the `Patient.meta.profile` element of the returned `Patient` resource.
- SHALL include the `versionId` of the current version of the `Patient` resource.
- SHALL include all relevant business `identifier` details (i.e. NHS Number) for the `Patient` resource.
- SHALL supply gender, name, birth date or deceased date where these are available (as indicated by the [Must-Support](https://www.hl7.org/fhir/STU3/conformance-rules.html#mustSupport) FHIR property)
- The patient resource SHALL contain at least a single name element. The patient resource SHALL contain a single instance of the name element with the `use` of `official`. This official name should contain the name registered on the spine which is returned by a PDS lookup for the patient.

```json
{
	"resourceType": "Patient",
	"id": "2",
	"meta": {
		"versionId": "636064088097580046",
		"lastUpdated": "2016-08-10T16:52:39.716+01:00",
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"]
	},
	"identifier": [{
		"extension": [{
			"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-NHSNumberVerificationStatus-1",
			"valueCodeableConcept": {
				"coding": [{
					"system": "https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-NHSNumberVerificationStatus-1",
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
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Read<Patient>("Patient/2");
FhirSerializer.SerializeResourceToXml(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = new FhirContext().forStu3();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
Patient patient = client.read().resource(Patient.class).withId("2").execute();
```