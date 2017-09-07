---
title: Read an appointment
keywords: appointments, use case, read
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_read_an_appointment.html
summary: "Use case for reading an appointment resource."
---


## API Use Case ##

This specification describes a single use cases. For complete details and background please see the [Appointment Management Capability Bundle](appointments.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Consumer ##

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
GET /Appointment/[id]
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Appointment/[id]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

For example:

- Where a Logical identifier of the resource is not valid/can't be found on the server, a 404 HTTP Status code would be returned with the relevent OperationOutcome resource.
- Where insufficient data about an appointment is present in the provider system to populate an appointment resource which validates to the `GPConnect-Appointment-1` profile, an 500 HTTP Status code should be returned, together with the appropriate OperationOutcome resource providing diagnostic detail.   

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return `Appointment` resources that conform to the `gpconnect-appointment-1` profile.
- SHALL include the URI of the `gpconnect-appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the returned `Appointment` resource.
- SHALL include the `versionId` of the current version of the `Appointment` resource.
- SHALL include all relevant business `identifier` details (if any) for the `Appointment` resource.

```json
{
	"resourceType": "Appointment",
	"id": "9",
	"meta": {
		"versionId": "636068818095315079",
		"lastUpdated": "2016-08-15T19:16:49.971+01:00",
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-appointment-1"]
	},
	"status": "booked",
	"type": {
		"coding": [{
			"system": "http://hl7.org/fhir/ValueSet/c80-practice-codes",
			"code": "408443003"
		}],
		"text": "GP"
	},
	"reason": {
		"text": "Rash"
	},
	"description": "Free text description.",
	"start": "2016-05-30T10:00:00+01:00",
	"end": "2016-05-30T10:25:00+01:00",
	"slot": [{
		"reference": "Slot/1",
		"display": "Slot 1"
	}],
	"comment": "Free text comment.",
	"participant": [{
		"type": [{
			"coding": [{
				"system": "http://hl7.org/fhir/ValueSet/encounter-participant-type",
				"code": "SBJ"
			}],
			"text": "Subject"
		}],
		"actor": {
			"reference": "Patient/1",
			"display": "Mr. Mike Smith"
		},
		"required": "required",
		"status": "accepted"
	},
	{
		"type": [{
			"coding": [{
				"system": "http://hl7.org/fhir/ValueSet/encounter-participant-type",
				"code": "PPRF"
			}],
			"text": "Primary Performer"
		}],
		"actor": {
			"reference": "Practitioner/100",
			"display": "Dr. Bob Smith"
		},
		"required": "required",
		"status": "accepted"
	},
	{
		"actor": {
			"reference": "Location/32",
			"display": "Leeds GP Clinic"
		},
		"status": "accepted"
	}]
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Read<Appointment>("Appointment/1");
FhirSerializer.SerializeResourceToJson(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forDstu2();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1");
Appointment appointment = client.read().resource(Appointment.class).withId("1").execute();
System.out.println(fhirContext.newJsonParser().setPrettyPrint(true).encodeResourceToString(appointment));
```