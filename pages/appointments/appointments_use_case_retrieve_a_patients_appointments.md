---
title: Retrieve a patient's appointments
keywords: appointments, use case, retrieve
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_retrieve_a_patients_appointments.html
summary: "Use case for retrieval of a patient's appointments from an organisation."
---

## Use Case ##

This specification describes a single use cases. For complete details and background please see the [Appointment Management Capability Bundle](appointments.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service.
- SHALL have previously [resolved the logical ID of the patient](https://nhsconnect.github.io/gpconnect/foundations_use_case_find_a_patient.html) on the server using the NHS Number

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
GET /Patient/[id]/Appointment
```

Providers SHALL support searching within this compartment by `start` date/time, for example:

```http
GET /Patient/[id]/Appointment?start=[{search_prefix}start_date]{&start=[{search_prefix}end_date]}
```

The Provider systems:

- SHALL support the following search prefixes (eq,gt,lt,ge,le) as outlined in the [Development Guidance - FHIR API Guidance - Common API Guidance](development_fhir_api_guidance.html#search-resources) section.  

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/[id]/Appointment
```

Providers SHALL support searching within this compartment by `start` date/time, for example:

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/[id]/Appointment?start=[{search_prefix}start_date]{&start=[{search_prefix}end_date]}
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments` |

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems:

- SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

For example:

- Where the use of the `start` search parameter does not define a valid date range, HTTP Status code 422 with error code 'INVALID_PARAMETER' will be returned.


### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return zero or more matching `Appointment` resources in a `Bundle` of `type` searchset.
- SHALL include the URI of the `gpconnect-appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the returned `Appointment` resources.
- SHALL include the versionId and fullUrl of the current version of each `Appointment` resource returned.
- SHALL return all appointments for the patient within the requested period. No additional filtering should be applied by the provider, all appointments including cancelled appointments should be returned as part of the response.

```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "Appointment/148",
		"resource": {
			"resourceType": "Appointment",
			"id": "148",
			"meta": {
				"versionId": "1503310820000",
				"lastUpdated": "2017-08-21T10:20:20.000+00:00",
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-appointment-1"]
			},
			"status": "booked",
			"type": {
				"coding": [{
					"system": "http://hl7.org/fhir/ValueSet/c80-practice-codes",
					"code": "null",
					"display": "Clinical oncology"
				}],
				"text": "Clinical oncology"
			},
			"reason": {
				"coding": [{
					"system": "http://snomed.info/sct",
					"code": "00001",
					"display": "Default Appointment Type"
				}],
				"text": "Default Appointment Type"
			},
			"start": "2017-08-21T10:20:00.000+00:00",
			"end": "2017-08-21T10:50:00.000+00:00",
			"slot": [{
				"reference": "Slot/544"
			},
			{
				"reference": "Slot/545"
			},
			{
				"reference": "Slot/546"
			}],
			"comment": "Test Appointment 1",
			"participant": [{
				"actor": {
					"reference": "Patient/2"
				},
				"status": "accepted"
			},
			{
				"actor": {
					"reference": "Location/1"
				},
				"status": "accepted"
			},
			{
				"actor": {
					"reference": "Practitioner/2"
				},
				"status": "accepted"
			}]
		}
	},
	{
		"fullUrl": "Appointment/149",
		"resource": {
			"resourceType": "Appointment",
			"id": "149",
			"meta": {
				"versionId": "1503310844000",
				"lastUpdated": "2017-08-21T10:20:44.000+00:00",
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-appointment-1"]
			},
			"status": "booked",
			"type": {
				"coding": [{
					"system": "http://hl7.org/fhir/ValueSet/c80-practice-codes",
					"code": "null",
					"display": "Clinical oncology"
				}],
				"text": "Clinical oncology"
			},
			"reason": {
				"coding": [{
					"system": "http://snomed.info/sct",
					"code": "00001",
					"display": "Default Appointment Type"
				}],
				"text": "Default Appointment Type"
			},
			"start": "2017-08-21T12:40:00.000+00:00",
			"end": "2017-08-21T12:50:00.000+00:00",
			"slot": [{
				"reference": "Slot/558"
			}],
			"comment": "Test Appointment 2",
			"participant": [{
				"actor": {
					"reference": "Patient/2"
				},
				"status": "accepted"
			},
			{
				"actor": {
					"reference": "Location/1"
				},
				"status": "accepted"
			}]
		}
	},
	{
		"fullUrl": "Appointment/150",
		"resource": {
			"resourceType": "Appointment",
			"id": "150",
			"meta": {
				"versionId": "1503310866000",
				"lastUpdated": "2017-08-21T10:21:06.000+00:00",
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-appointment-1"]
			},
			"status": "booked",
			"type": {
				"coding": [{
					"system": "http://hl7.org/fhir/ValueSet/c80-practice-codes",
					"code": "null",
					"display": "Clinical oncology"
				}],
				"text": "Clinical oncology"
			},
			"reason": {
				"coding": [{
					"system": "http://snomed.info/sct",
					"code": "00001",
					"display": "Default Appointment Type"
				}],
				"text": "Default Appointment Type"
			},
			"start": "2017-08-24T09:10:00.000+00:00",
			"end": "2017-08-24T09:20:00.000+00:00",
			"slot": [{
				"reference": "Slot/681"
			}],
			"comment": "Test Appointment 3",
			"participant": [{
				"actor": {
					"reference": "Patient/2"
				},
				"status": "accepted"
			},
			{
				"actor": {
					"reference": "Location/1"
				},
				"status": "accepted"
			},
			{
				"actor": {
					"reference": "Practitioner/2"
				},
				"status": "accepted"
			}]
		}
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

