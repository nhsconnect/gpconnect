---
title: Retrieve a patient's appointments
keywords: appointments, use case, retrieve
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_retrieve_a_patients_appointments.html
summary: "Use case for retrieval of a patient's appointments from an organisation."
---

## Use case ##

This specification describes a single use case enabling the consumer to retrieve a patient's future appointment bookings from a targeted Provider system. 

{% include important.html content="The Appointment Management capability pack is aimed at administration of a patient's appointments. As part of information governance (IG) requirements the view of a patient's appointments has been restricted to only viewing future appointments. Additional details are available on the [Design decisions](appointments_design.html#viewing-and-amending-booked-appointments) page." %}

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service
- SHALL have previously [resolved the logical ID of the patient](https://nhsconnect.github.io/gpconnect/foundations_use_case_find_a_patient.html) on the server using the NHS Number

## API usage ##

### Request operation ###

#### Search parameters ####

Provider systems SHALL implement the following search parameters:

| Name | Type | Description | Paths |
| --- | --- | --- | --- |
| `start` | `date` | Appointment start date/time. | `Appointment.start` |


The consumer:
- SHALL include two `start` search parameter with every request
  - One of the 'start' search parameter SHALL be supplied with the `ge` search prefix. For example, 'start=ge2017-09-22', which indicates that the consumer would like appointments where the appointment start date is on or after "2017-09-22".
  - One of the 'start' search parameter SHALL be supplied with the `le` search prefix. For example, 'start=le2017-09-25', which indicates that the consumer would like appointments where the appointment start date is on or before "2017-09-25"
- SHALL only include the date component of the search parameter and not a time component. The date SHALL include day, month and year elements.
- SHALL not request a date range where any part of the date range is in the past
- SHALL indicate to the end user that only appointments in the future will be returned from GP Connect and that the earliest that the user can request appointments is todays date

  ![Diagram - Date range parameters](images/appointments/RetrievePatientsApp.png)

The provider systems:
- SHALL support the search prefixes `ge` and `le`
- SHALL return an error if any part of the consumer requested search range is in the past.
  - If the consumer sends todays date the provider SHALL return all appointments for today, if the appointments are in the past because the current time is after the appointment time but the appointment start date is todays date, then the appointment SHALL still be returned in the response bundle.
  - The error returned SHALL include a meaningful error message to indicate that the search parameters can not request appointments in the past.
- SHALL return an error if either either of the date parameters contain a time element.
- SHALL return an error if either of the two start date parameters are not sent with the consumers request.

#### FHIR relative request ####


```http
GET /Patient/[id]/Appointment?start=ge{lower_date_range_boundary}&start=le{upper_date_range_boundary}

```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/[id]/Appointment?start=ge{lower_date_range_boundary}&start=le{upper_date_range_boundary}
```

#### Examples ####

```text
Retrieve all appointments for a patient which start on or between 2017-07-11 and 2017-09-14:

GET /Patient/[id]/Appointment?start=ge2017-07-11&start=le2017-09-14
```


#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments-1` |

#### Payload request body ####

N/A

### Error handling ###

Provider systems:

- SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached. Refer to [Development - FHIR API guidance - error handling](development_fhir_error_handling_guidance.html) for details of error codes.
- SHALL return an error if any part of the consumer supplied date range is in the past. The OperationOutcome returned SHALL include a meaningful error message to indicate that the search parameters can not request appointments in the past.
- Where the use of the `start` search parameter does not define a valid date range, `HTTP Status code 422` with error code `INVALID_PARAMETER` will be returned. Additional details SHALL be returned in the diagnostics element.


### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL only return appointments where the `start` element is in the future (greater than the the current date).
- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return zero or more matching [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) resources in a `Bundle` of `type` searchset.
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the returned `Appointment` resources.
- SHALL include the versionId and fullUrl of the current version of each `Appointment` resource returned.
- SHALL return all appointments for the patient within the requested period signified by the `start` search parameter(s). All appointments including cancelled appointments should be returned as part of the response, no additional filtering should be applied.

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

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library, which is the official .NET API for HL7&reg; FHIR&reg;." %}

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

