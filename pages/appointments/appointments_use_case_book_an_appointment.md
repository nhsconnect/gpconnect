---
title: Book an appointment for a patient at an organisation
keywords: appointments, use case, book, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_book_an_appointment.html
summary: "Use case for booking an appointment for a patient with a given organisation."
---

## Use Case ##

The typical flow to book an appointment is:

 1. Search by `NHS Number` for, or otherwise obtain, a `Patient` resource.
 2. Search for available `Slot` resources by date range.
 3. Create an `Appointment` for the chosen `Slot` and `Patient` resources.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously traced the patient's NHS Number using PDS or an equivalent service.
- SHALL have previously obtained the details for one or more free slots that are to be booked.

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
POST /Appointment
```

#### FHIR Absolute Request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Appointment
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment` |

#### Payload Request Body ####

The request payload is a profiled version of the standard FHIR [Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html) resource.

The following data-elements are mandatory (i.e data MUST be present).

- the patient `participant` of the appointment.
- the primary practitioner `participant` of the appointment.
- the `start` and `end` of the appointment.
- the `status` identifying the appointment as "booked".
- the `slot` details of one or more free slots to be booked.

{% include important.html content="Multiple adjacent free slots can be booked using the same appointment (i.e. two 15 minute slots to obtain one 30 minute consultation)." %}

On the wire a JSON serialised request would look something like the following:

```json
{
	"resourceType": "Appointment",
	"status": "booked",
	"type": {
		"coding": [{
			"system": "http://hl7.org/fhir/ValueSet/c80-practice-codes",
			"code": "408443003"
		}],
		"text": "GP"
	},
	"reason": {
		"text": "Free text reason."
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
	}]
}
```

#### Error Handling ####

Provider systems:

- SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached.

For example the:

- submitted `start` and `end` date range does not match that of the requested `Slot`(s).
- one or more of the requested `Slot` resources does not exist or already has a `status` of busy.

Provider systems SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `201` **Created** HTTP status code on successful execution of the operation.
- SHALL return an `Appointment` resource that conform to the `gpconnect-appointment-1` profile.
- SHALL maintain resource state in accordance with their own internal integrity constraints, including the state of any associated resources, such as `Slots`, `Schedules`, etc.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned response.
- SHALL include the `versionId` of the current version of each `Appointment` resource.
- MAY generate a business identifier to allow an individual appointment (i.e. `Appointment` resource) to be uniquely identifiable.

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
	}]
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
TODO
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
TODO
```