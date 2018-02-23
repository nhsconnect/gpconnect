---
title: Retrieve a patient's appointments
keywords: appointments, use case, retrieve
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_retrieve_a_patients_appointments.html
summary: "Use case for retrieval of a patient's appointments from an organisation."
---

## Use Case ##

This specification describes a single use case. For complete details and background please see the [Appointment Management Capability Bundle](appointments.html).

{% include important.html content="The Appointment Management capability pack is aimed at administration of a patients appointments. As part of IG requirements the view of a patients appointments has been restricted to only viewing future appointments, additional details are available on the [Design Decisions](appointments_design.html#viewing-and-amending-booked-appointments) page." %}

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


#### Search Parameters ####

Provider systems SHALL implement the following search parameters:

| Name | Type | Description | Paths |
| --- | --- | --- | --- |
| `start` | `date` | Appointment start date/time. | `Appointment.start` |

The Provider systems:
- SHALL support the search prefixes `eq`, `gt`, `lt`, `ge` and `le`.

#### FHIR Relative Request ####

```http
GET /Patient/[id]/Appointment
```

```http
GET /Patient/[id]/Appointment?start=[{search_prefix}start_date]{&start=[{search_prefix}end_date]}
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/[id]/Appointment
```

#### Examples ####

```text
Retrieve all appointments for a patient:

GET /Patient/[id]/Appointment
```

```text
Retrieve all appointments for a patient which start on or between 2017-07-11 and 2017-09-14:

GET /Patient/[id]/Appointment?start=ge2017-07-11&start=le2017-09-14
```

```text
Retrieve all appointments for a patient which start after 2017-07-11:

GET /Patient/[id]/Appointment?start=gt2017-07-11
```

```text
Retrieve all appointments for a patient which start before 2017-09-14:

GET /Patient/[id]/Appointment?start=start=le2017-09-14
```

```text
Retrieve all appointments for a patient on 2017-08-22:

GET /Patient/[id]/Appointment?start=2017-08-22
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments-1` |

#### Payload Request Body ####

N/A

### Error Handling ###

Provider systems:

- SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached. Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

For example:

- Where the use of the `start` search parameter does not define a valid date range, `HTTP Status code 422` with error code `INVALID_PARAMETER` will be returned. Additional details can be returned in the diagnostics element.


### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL only return appointments where the `start` dateTime is in the future (greater than the the current date and time).
- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return zero or more matching [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) resources in a `Bundle` of `type` searchset.
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the returned `Appointment` resources.
- SHALL include the versionId and fullUrl of the current version of each `Appointment` resource returned.
- SHALL return all appointments for the patient within the requested period signified by the `start` search parameter(s). All appointments including cancelled appointments should be returned as part of the response, no additional filtering should be applied.
  - Where no `start` search parameter is specified the provider systems SHALL return all present and future appointments.
  - Where only a lower boundary `start` search parameter (with prefix 'gt' or 'ge') is included in the request, provider SHALL return all data items from this date on, inclusive or exlusive as per the search prefix.
  - Where only an upper boundary `start` search parameter (with prefix 'le' or 'lt') is included in the request, provider SHALL return all data items up to this date, inclusive or exlusive as per the search prefix.
  - Where no search prefix, or only an equals (eq) search prefix, is sent with a single `start` search parameter, provider SHALL return all data items for that specified date.
  - Where two search parameters are included there should be a lower boundary search prefix on one of the `start` parameter and an upper boundary search prefiex with the other `start` search parameter.

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
				"lastUpdated": "2017-11-08T10:20:20.000+00:00",
				"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1"]
			},
			"contained": [{
				"resourceType": "Organization",
				"id": "1",
				"meta": {
					"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"]
				},
				"name": "Test Organization Name",
				"telecom": [{
					"system": "phone",
					"value": "0300 303 5678"
				}]
			}],
			"extension": [{
				"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-GPConnect-BookingOrganisation-1",
				"valueReference": {
					"reference": "#1"
				}
			}],
			"status": "booked",
			"reason": {
				"coding": [{
					"system": "http://snomed.info/sct",
					"code": "00001",
					"display": "Default Appointment Type"
				}],
				"text": "Default Appointment Type"
			},
			"description" : "GP Connect Appointment description 148",
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
			"created": "2017-10-09T13:48:41+01:00",
			"comment": "Test Appointment Comment 148",
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
				"versionId": "1503440820000",
				"lastUpdated": "2016-08-17T10:20:20.000+00:00",
				"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1"]
			},
			"contained": [{
				"resourceType": "Organization",
				"id": "1",
				"meta": {
					"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"]
				},
				"name": "Test Organization Name 2",
				"telecom": [{
					"system": "phone",
					"value": "0300 303 5679"
				}]
			}],
			"extension": [{
				"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-GPConnect-BookingOrganisation-1",
				"valueReference": {
					"reference": "#1"
				}
			}],
			"status": "booked",
			"description" : "GP Connect Appointment description 148",
			"start": "2016-08-16T11:20:00.000+00:00",
			"end": "2016-08-16T11:30:00.000+00:00",
			"slot": [{
				"reference": "Slot/303"
			}],
			"created": "2016-08-14T13:48:41+01:00",
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
	}]
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient(string.Format("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/"));
client.PreferredFormat = ResourceFormat.Json;
Bundle bundle = (Bundle)client.Get("Patient/2/Appointment");
FhirSerializer.SerializeResourceToJson(bundle).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forStu3();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");

Bundle responseBundle = client.search()
	.forResource(Patient.class)
	.withIdAndCompartment("2", "Appointment")
	.returnBundle(ca.uhn.fhir.model.dstu2.resource.Bundle.class)
	.execute();
	
System.out.println(ctx.newJsonParser().setPrettyPrint(true).encodeResourceToString(responseBundle));
```

