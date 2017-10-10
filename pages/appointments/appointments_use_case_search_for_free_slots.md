---
title: Search for free slots
keywords: appointments, use case, search, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_search_for_free_slots.html
summary: "Use case for searching for free slots within a date range."
---

## Use Case ##

This specification describes a single use case. For complete details and background please see the [Appointment Management Capability Bundle](appointments.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 


## Search Parameters ##

Provider systems SHALL implement the following search parameters:

| Name | Type | Description | Paths |
| `fb-type` | `token` | The free/busy status of the appointment | `Slot.freeBusyType` |
| `start` | `date` | Slot start date/time. | `Slot.start` |
| `end` | `date` | Slot end date/time. | `Slot.end` |

{% include note.html content="The supported search parameters should be included in the [conformance profile](foundations_use_case_get_the_fhir_conformance_profile.html)." %}

## _include Parameters ##

Provider systems SHALL implement the following include parameters:

| `_include=Slot:schedule` |   | Include Schedule Resources referenced within the returned Slot Resources | `Slot.schedule` |
| `_include:recurse= Schedule:Practitioner` |  | Include Practitioner Resources referenced within the returned Schedule Resources | `Schedule.extension("practitioner")` |
| `_include:recurse= Schedule:actor:Location` |  | Include Location Resources referenced within the returned Schedule Resources | `Schedule.actor:Location` |


The following parameters SHALL be included in the request:

- The `start` parameter SHALL only be included once in the request.
- The `start` parameter SHALL be supplied with the `ge` search prefix. For example 'start=ge22-09-2017' which indicates that the consumer would like slots where the slot start date is on or after "22-09-2017".
- The `end` parameter SHALL only be included once in the request.
- The `end` parameter SHALL be supplied with the `le` search prefix. For example 'end=le26-09-2017' which indicates that the consumer would like slots where the slot end date is on or before "26-09-2017".
  
  ![Diagram - Date range parameters](images/appointments/SearchForFreeSlots.png)

- `fb-type=free` specifies that only free slots will be returned. Note: the SlotStatus value of `free` SHALL be specified, other SlotStatus values are not permitted.

- `_include=Slot:schedule` specifies that associated Schedule resources are returned.


The following parameters MAY be included to minimise the number of API calls required to prepare an appointment booking:

- _include:recurse=Schedule:actor:Practitioner
- _include:recurse=Schedule:actor:Location


On the wire a `Search for free slots` request would look something like the following:

```http
GET /Slot?start=ge22-09-2017&end=le26-09-2017&Slot.fh-type=free&_include=Slot:schedule&_include:recurse=Schedule:actor:Practitioner&_include:recurse=Schedule:actor:Location
```




## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL request a maximum date range covering a two week period.

{% include tip.html content="Multiple separate API calls can be made if a larger date range is required however consideration should be given to the load this placed on the Provider system." %}

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
GET /Slot?[start={search_prefix}start_date]
          [&end=[{search_prefix}end_date]
          [&fb-type=free]
          [&_include=Slot:schedule]
          {&_include:recurse=Schedule:actor:Practitioner}
          {&_include:recurse=Schedule:actor:Location}
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]
          /Slot?[start={search_prefix}start_date]
          [&end=[{search_prefix}end_date]
          [&fb-type=free]
          [&_include=Slot:schedule]
          {&_include:recurse=Schedule:actor:Practitioner}
          {&_include:recurse=Schedule:actor:Location}
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot` |

#### Payload Request Body ####


#### Error Handling ####

The Provider system SHALL return an error if:

- the time period defined by `start` and `end` parameters is greater than a two week period.
- the `fb-type` parameter is absent or is present with a value other than `free`
- the `_include=Slot:schedule` is absent

Provider systems SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more parameters are corrupt or a specific business rule/constraint is breached.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful retrieval of a "free" slot details.
- SHALL include the free `Slot` details for the organisation which have a `freeBusyType` status of "free" and fall fully within the requested date range. I.e. free slots which start before the `start` parameter and free slots which end after `end` search parameter SHALL NOT be returned. 
- SHALL include the `Schedule` and `Slot` details associated with the returned slots as defined by the search parameter which have been specified. `Practitioner` is required in the searchset `Bundle` only if available.
 
  The response `Bundle` SHALL only contain `Schedule`, `Organization`, `Practitioner` and `Location` Resources related to the returned free `Slot` Resources. If no free slots are returned for the requested time period then no Resources should be returned within the response `Bundle`.

- SHALL include `Practitioner` and `Location` resources associated with Schedule resources in the response Bundle ONLY where requested to do so by the consumer using the `_include:recurse=Schedule:actor:Practitioner` and/or `_include:recurse=Schedule:actor:Location` parameters.

- SHALL manage slot `start` and `end` times to indicate which slots can be considered `adjacent` and therefore be booked against a single appointment as part of a `multi slot appointment booking`. Providers are responsible for the implementation of business rules that forbid the booking of non-adjacent slots according to their own practices.

  To allow consumers to implement multi slot appointment booking, the consumer needs to be able to identify which slots can be considered adjacent. A provider SHALL indicate which slots are adjacent or not adjacent using the following rules:

  * To indicate two slots (Slot A & Slot B) are adjacent, the two slots SHALL reference the same schedule resource and the ```start``` time of ```Slot B``` SHALL equals ```end``` time of ```Slot A```.
  * If the slots do not conform to the rule above, either the slots do not link to the same schedule or the start time of one slot is not the same as the end time of the previous slot then these slots SHALL not be considered adjacent.

```json
{
	"resourceType": "Bundle",
	"type": "searchset",
	"entry": [{
		"fullUrl": "Organisation/1",
		"resource": {
			"resourceType": "Organization",
			"id": "1",
			"meta": {
				"versionId": "1469444400000",
				"lastUpdated": "2016-07-25T12:00:00.000+01:00",
				"profile": ["https://fhir.nhs.uk/StructureDefinition/CareConnect-GPC-Organization-1"]
			},
			"identifier": [{
				"system": "https://fhir.nhs.uk/Id/ods-organization-code",
				"value": "R1A15"
			}],
			"name": "The Hepworth Surgery"
		}
	},
	{
		"fullUrl": "Location/1",
		"resource": {
			"resourceType": "Location",
			"id": "1",
			"meta": {
				"versionId": "1469444400000",
				"lastUpdated": "2016-07-25T12:00:00.000+01:00",
				"profile": ["https://fhir.nhs.uk/StructureDefinition/CareConnect-GPC-Location-1"]
			},
			"identifier": [{
				"system": "https://fhir.nhs.uk/Id/local-location-identifier",
				"value": "BUILDING-A127"
			}],
			"name": "Building A"
		}
	},
	{
		"fullUrl": "Schedule/1",
		"resource": {
			"resourceType": "Schedule",
			"id": "1",
			"meta": {
				"versionId": "1469444400000",
				"lastUpdated": "2016-07-25T12:00:00.000+01:00",
				"profile": ["https://fhir.nhs.uk/StructureDefinition/gpconnect-schedule-1"]
			},
			"extension": [{
				"url": "http://fhir.nhs.net/StructureDefinition/extension-gpconnect-practitioner-1",
				"valueReference": {
					"reference": "Practitioner/2"
				}
			}],
			"identifier": [{
				"system": "http://fhir.nhs.net/Id/gpconnect-schedule-identifier",
				"value": "Schedule001"
			}],
			"type": [{
				"coding": [{
					"system": "http://hl7.org/fhir/ValueSet/c80-practice-codes",
					"code": "394802001",
					"display": "General medicine"
				}],
				"text": "General medicine"
			}],
			"actor": {
				"reference": "Location/1"
			},
			"planningHorizon": {
				"start": "2016-03-22T10:00:00+00:00",
				"end": "2030-12-22T17:59:59+00:00"
			},
			"comment": "Schedule 1 for general appointments"
		}
	},
	{
		"fullUrl": "Practitioner/2",
		"resource": {
			"resourceType": "Practitioner",
			"id": "2",
			"meta": {
				"versionId": "1469444400000",
				"lastUpdated": "2016-07-25T12:00:00.000+01:00",
				"profile": ["http://fhir.nhs.net/StructureDefinition/CareConnect-GPC-Practitioner-1"]
			},
			"identifier": [{
				"system": "https://fhir.nhs.uk/Id/sds-user-id",
				"value": "G22345655"
			},
			{
				"system": "http://fhir.nhs.net/Id/sds-role-profile-id",
				"value": "PT1122"
			}],
			"name": {
				"use": "usual",
				"family": ["Slater"],
				"given": ["Kibo"],
				"prefix": ["Mr"]
			},
			"gender": "male",
			"practitionerRole": [{
				"managingOrganization": {
					"reference": "Organization/1"
				},
				"role": {
					"coding": [{
						"system": "http://fhir.nhs.net/ValueSet/sds-job-role-name-1",
						"code": "R0050",
						"display": "Consultant"
					}]
				}
			}],
			"communication": [{
				"coding": [{
					"system": "http://fhir.nhs.net/ValueSet/human-language-1",
					"code": "en",
					"display": "English"
				}]
			}]
		}
	},
	{
		"fullUrl": "Slot/1584",
		"resource": {
			"resourceType": "Slot",
			"id": "1584",
			"meta": {
				"versionId": "1471219260000",
				"lastUpdated": "2016-08-15T01:01:00.000+01:00",
				"profile": ["https://fhir.nhs.uk/StructureDefinition/gpconnect-slot-1"]
			},
			"type": {
				"coding": [{
					"system": "http://hl7.org/fhir/ValueSet/c80-practice-codes",
					"code": "394592004",
					"display": "Clinical oncology"
				}],
				"text": "Clinical oncology"
			},
			"schedule": {
				"reference": "Schedule/1"
			},
			"freeBusyType": "free",
			"start": "2016-08-15T11:30:01.000+01:00",
			"end": "2016-08-15T12:00:01.000+01:00"
		}
		// Note, remainder of response has been truncated.
	}]	
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/");
client.PreferredFormat = ResourceFormat.Json;

[ to add ]

FhirSerializer.SerializeResourceToJson(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forDstu2();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1");

[ to add ]

System.out.println(ctx.newJsonParser().setPrettyPrint(true).encodeResourceToString(responseBundle));
```
