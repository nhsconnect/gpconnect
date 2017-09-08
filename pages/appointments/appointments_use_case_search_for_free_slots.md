---
title: Search for free slots at an organisation
keywords: appointments, use case, search, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_search_for_free_slots.html
summary: "Use case for searching for free slots within a date range at an organisation."
---

## Use Case ##

This specification describes a single use case. For complete details and background please see the [Appointment Management Capability Bundle](appointments.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously [resolved the organisation's FHIR Base URL](integration_spine_directory_services.html) using an ODS Code, ODS Site Code or other organisational business identifier.
- SHALL request a maximum date range covering a two week period.

{% include tip.html content="Multiple separate API calls can be made if a larger date range is required however consideration should be given to the load this placed on the Provider system." %}

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
POST /Organization/[id]/$gpc.getschedule
```

#### FHIR Absolute Request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Organization/[id]/$gpc.getschedule
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getschedule` |

#### Payload Request Body ####

The following data-elements are mandatory (i.e. data MUST be present):

- the `timePeriod` is the time period over which the requested information is to be returned.

The request payload is a set of [Parameters](https://www.hl7.org/fhir/DSTU2/parameters.html) conforming to the `gpconnect-schedule-operation-1` profiled `OperationDefinition`, see below:

{% include tip.html content="This is an instance level operation (i.e. is associated with a given resource instance)." %} 

```xml
<OperationDefinition xmlns="http://hl7.org/fhir">
	<id value="getschedule" />
	<version value="1.0.0-beta.1" />
	<name value="Get Schedule &amp; Slots" />
	<status value="draft" />
	<kind value="operation" />
	<experimental value="true" />
	<publisher value="NHS Digital" />
	<date value="2016-08-01" />
	<description value="Get The Free Schedule &amp; Slots For A Given Organization." />
	<idempotent value="true" />
	<code value="gpc.getschedule" />
	<system value="false" />
	<type value="Organization" />
	<instance value="true" />
	<parameter>
		<name value="timePeriod" />
		<use value="in" />
		<min value="1" />
		<max value="1" />
		<documentation value="The time period for the requested information." />
		<type value="Period" />
	</parameter>
	<parameter>
		<name value="response" />
		<use value="out" />
		<min value="1" />
		<max value="1" />
		<documentation value="A searchset bundle containing the free slots with associated schedule and organisational details for the queried organisation and site." />
		<type value="Bundle" />
	</parameter>
</OperationDefinition>
```

{% include important.html content="Provider systems SHALL only expose `Schedule`, `Slot` and associated resources for organisations whose appointment book they're responsible for maintaining." %}

On the wire a JSON serialised `$gpc.getschedule` request would look something like the following:

```http
POST /Organization/1/$gpc.getschedule
```

```json
{
	"resourceType": "Parameters",
	"parameter": [{
		"name": "timePeriod",
		"valuePeriod": {
			"start": "2016-08-08",
			"end": "2016-08-22"
		}
	}]
}
```

#### Error Handling ####

The Provider system SHALL return an error if:

- the `timePeriod` is for more than a two week period.
- the Provider system isn't responsible for maintaining the organisation's appointment book.

Provider systems SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful retrieval of a "free" schedule and slot details.
- SHALL include the free `Slot` details for the organisation which have a `freeBusyType` status of "free" and fall within the requested date range.
- SHALL include the URI of the relevant GP Connect `StructureDefinition` profile in the `{Resource}.meta.profile` element of the returned resources.
- SHALL include the `Schedule`, `Slot`, `Organization` and `Location` details for the retrieved schedule(s) in a searchset `Bundle`. `Practitioner` is required in the searchset `Bundle` only if available.
 
  The response `Bundle` SHALL only contain `Schedule`, `Organization`, `Practitioner` and `Location` Resources related to the returned free `Slot` Resources. If no free slots are returned for the requested time period then no Resources should be returned within the response `Bundle`.


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
			"modifierExtension": [{
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

var parameters = new Parameters();
parameters.Add("timePeriod", new Period()
{
	Start = new FhirDateTime("2017-09-07").ToString(),
	End = new FhirDateTime("2017-09-15").ToString()
});

var resource = client.InstanceOperation(new Uri("Organization/1",UriKind.Relative),"getschedule",parameters);

FhirSerializer.SerializeResourceToJson(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forDstu2();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1");

PeriodDt timePeriod = new PeriodDt();
timePeriod.setStart(new DateTimeDt("2017-09-07"));
timePeriod.setEnd(new DateTimeDt("2017-09-15"));

Parameters params = new Parameters();
params.addParameter().setName("timePeriod").setValue(timePeriod);

Bundle responseBundle = client
		.operation()
		.onInstance(new IdDt("Organization", "1"))
		.named("$gpc.getschedule")
		.withParameters(params)
		.returnResourceType(Bundle.class)
		.execute();

System.out.println(ctx.newJsonParser().setPrettyPrint(true).encodeResourceToString(responseBundle));
```