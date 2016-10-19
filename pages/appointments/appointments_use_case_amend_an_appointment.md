---
title: Amend an appointment for a patient at an organisation
keywords: appointments, use case, amend, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_amend_an_appointment.html
summary: "Use case for amending an appointment for a patient with a given organisation."
---

## Use Case ##

The typical flow to cancel an appointment is:

 1.	Search by `NHS Number` for, or otherwise obtain, a `Patient` resource.
 2. Search for `Appointment` resources for the `Patient` resource.
 3. Choose an `Appointment` resource and update it's `description` and/or `comment` details.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously traced the patient's NHS Number using PDS or an equivalent service.
- SHALL have previously found the appointment id using Retrieve a patient's appointments.

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
PUT /Appointment/[id]
```

#### FHIR Absolute Request ####

```http
PUT https://[proxy_server]/https://[provider_server]/[fhir_base]/Appointment/[id]
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `SSP-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `SSP-From`           | Consumer's ASID |
| `SSP-To`             | Provider's ASID |
| `SSP-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:update:appointment` |

#### Payload Request Body ####

The request payload is a profiled version of the standard FHIR [Appointment](https://www.hl7.org/fhir/DSTU2/appointment.html) resource.

Only the following data-elements can be modified when performing an appointment amendment.

- the appointment `reason` MUST be updated to include any updated appointment reason details.

{% include important.html content="If any content other than the appointment reason is updated the server SHALL reject the amendment and return an error." %}

On the wire a JSON serialised request would look something like the following:

```json
{
	"resourceType": "Appointment",
	"id": "1",
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
		"text": "Free text updated reason."
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

The Provider system SHALL return an error if:

- any appointment details other than the appointment `reason` field are attempted to be updated.

Provider systems SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return an `Appointment` resource that conform to the `gpconnect-appointment-1` profile.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned response.
- SHALL include the `versionId` of the current version of each `Appointment` resource.
- SHALL have updated the appointment `reason` inline with the details supplied in the request.

```json
{
	"resourceType": "Appointment",
	"id": "1",
	"meta": {
		"versionId": "636064088104680389",
		"lastUpdated": "2016-08-15T20:00:41.059+01:00",
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
		"text": "Free text updated reason."
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
var appointment = client.Read<Appointment>("Appointment/1");
// Update The Reason For The Appointment
appointment.Reason.Text = "Free text updated reason.";
var updatedAppointment = client.Update<Appointment>(appointment);
FhirSerializer.SerializeResourceToJson(updatedAppointment).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
TODO
```