---
title: Retrieve a care record section
keywords: getcarerecord, section, html, view
tags: [use_case,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_use_case_retrieve_a_care_record_section.html
summary: "Use case for retrieving a care record section for a patient from a given organisation."
---

## Use Case ##

This specification describes a single use cases. For complete details and background please see the [Access Record Capability Bundle](accessrecord.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously traced the patient's NHS Number using PDS or an equivalent service.
- SHALL render HTML content in-line with the [Access Record - Development - HTML Implementation Guide](accessrecord_development_html_implementation_guide.html).

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
POST /Patient/$gpc.getcarerecord
```

#### FHIR Absolute Request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/$gpc.getcarerecord
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord`|

Example HTTP request headers:

```http
POST http://gpconnect.fhir.nhs.net/fhir/Patient/$gpc.getcarerecord HTTP/1.1
User-Agent: .NET FhirClient for FHIR 1.2.0
Accept: application/json+fhir;charset=utf-8
Prefer: return=representation
Host: michaelm-pc
Content-Type: application/json+fhir;charset=utf-8
Content-Length: 289
Expect: 100-continue
Connection: Keep-Alive
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord
```

#### Payload Request Body ####

The following data-elements are mandatory (i.e. data MUST be present):

- the `patientNHSNumber` is the NHS Number of the patient who's GP care record you want to access.
- the `recordSection` is the GP care record section you wish to retrieve.

The following data-elements are optional (i.e. can be supplied for certain care record sections):

- the `timePeriod` is the time period over which the requested information is to be returned.

The request payload is a set of [Parameters](https://www.hl7.org/fhir/DSTU2/parameters.html) conforming to the `gpconnect-carerecord-operation-1` profiled `OperationDefinition`, see below:

{% include tip.html content="This is a type level operation (i.e. is not associated with a given resource instance)." %} 

```xml
<OperationDefinition xmlns="http://hl7.org/fhir">
	<id value="getcarerecord" />
	<version value="1.0.0-rc.1" />
	<name value="Get Care Record" />
	<status value="draft" />
	<kind value="operation" />
	<experimental value="true" />
	<publisher value="NHS Digital" />
	<date value="2016-08-01" />
	<description value="Get The GP Care Record Section For A Given Patient." />
	<idempotent value="true" />
	<code value="gpc.getcarerecord" />
	<system value="false" />
	<type value="Patient" />
	<instance value="false" />
	<parameter>
		<name value="patientNHSNumber" />
		<use value="in" />
		<min value="1" />
		<max value="1" />
		<documentation value="Patient that matches the NHS Number." />
		<type value="Identifier" />
	</parameter>
	<parameter>
		<name value="recordSection" />
		<use value="in" />
		<min value="1" />
		<max value="1" />
		<documentation value="Section of the care record defined by the parameter." />
		<type value="CodeableConcept" />
	</parameter>
	<parameter>
		<name value="timePeriod" />
		<use value="in" />
		<min value="0" />
		<max value="1" />
		<documentation value="The time period for the requested information." />
		<type value="Period" />
	</parameter>
	<parameter>
		<name value="response" />
		<use value="out" />
		<min value="1" />
		<max value="1" />
		<documentation value="View of the patient's care record which can be a summary view or specified section of the care record." />
		<type value="Bundle" />
	</parameter>
</OperationDefinition>
```

{% include important.html content="Provider systems SHALL only expose `Patient` resources for patient's who have a valid PDS trace status." %}

On the wire a JSON serialised `$gpc.getcarerecord` request would look something like the following:

```json
{
	"resourceType": "Parameters",
	"parameter": [{
		"name": "patientNHSNumber",
		"valueIdentifier": {
			"system": "http://fhir.nhs.net/Id/nhs-number",
			"value": "P003"
		}
	},
	{
		"name": "recordSection",
		"valueCodeableConcept": {
			"coding": [{
				"system": "http://fhir.nhs.net/ValueSet/gpconnect-record-section-1",
				"code": "ALL"
			}]
		}
	}]
}
```

The Provider system SHALL:

- use a default time period if no `timePeriod` parameter is specified for a section that can accept a time period.

<br/>
Refer to [Access Record - Development - HTML Implementation Guide - Per Section Default Time Frames](accessrecord_development_html_implementation_guide.html#per-section-default-time-frames) for details of the default time periods that SHALL be applied per care record section.

#### Error Handling ####

The Provider system SHALL return an error if:

- the `patientNHSNumber` is invalid (i.e. fails NHS Number format and check digit tests).
- the `patientNHSNumber` is not associated with a `NHS Number Status Indicator Code` of `Number present and verified`.
- the GP organisation is not the patient's nominated primary care provider.
- the `recordSection` is invalid (i.e. isn't from the correct value set).
- an invalid `timePeriod` is requested (i.e. end date > start date).
- a `timePeriod` is specified for a `recordSection` that is time period agnostic (e.g. Patient Summary, Allergies, Medications etc.)

Provider systems SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

```http
HTTP/1.1 200 OK
Cache-Control: no-cache
Pragma: no-cache
Content-Type: application/json+fhir; charset=utf-8
Date: Sun, 07 Aug 2016 11:13:05 GMT
Content-Length: 1464
```

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful retrieval of a care record section.
- SHALL return the care record section as valid XHTML inline with the [FHIR Narrative](https://www.hl7.org/fhir/DSTU2/narrative.html) guidance.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned response.
- SHALL include the `Patient`, `Practitioner` and `Organization` details for the retrieved care record in a searchset `Bundle`.

```json
{
	"resourceType": "Bundle",
	"meta": {
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-searchset-bundle-1"]
	},
	"type": "searchset",
	"entry": [{
		"resource": {
			"resourceType": "Patient",
			"id": "3",
			"meta": {
				"versionId": "636038251035486239",
				"lastUpdated": "2016-08-07T21:01:07.317+09:30",
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-patient-1"]
			},
			"identifier": [{
				"system": "http://fhir.nhs.net/Id/nhs-number",
				"value": "P003"
			}],
			"name": [{
				"use": "official",
				"family": ["Downs"],
				"given": ["Clare"],
				"prefix": ["Mrs"]
			}],
			"gender": "female",
			"birthDate": "19/01/1978"
		}
	},
	{
		"resource": {
			"resourceType": "Composition",
			"meta": {
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-carerecord-composition-1"]
			},
			"text": {
				"status": "generated"
			},
			"section": [{
				"code": {
					"coding": [{
						"system": "http://fhir.nhs.net/ValueSet/gpconnect-record-section-1",
						"code": "ALL"
					}]
				},
				"text": {
					"status": "generated",
					"div": "<div xmlns=\"http://www.w3.org/1999/xhtml\">\r\n    <h2>Current Allergies and Sensitivities</h2>\r\n    <table>\r\n        <thead>\r\n            <tr>\r\n                <td>\r\n                    <b>Start</b>\r\n                </td>\r\n                <td>\r\n                    <b>Details</b>\r\n                </td>\r\n            </tr>\r\n        </thead>\r\n        <tbody>\r\n            <tr>\r\n                <td>10 Mar 2014</td>\r\n                <td>Allergy to penicillin (disorder)</td>\r\n            </tr>\r\n        </tbody>\r\n    </table>\r\n</div>"
				}
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
var parameters = new Parameters();
parameters.Add("nhsNumber", new Identifier("http://fhir.nhs.net/Id/nhs-number","P003"));
parameters.Add("recordSection", new CodeableConcept("http://fhir.nhs.net/ValueSet/gpconnect-record-section-1","ALL"));
var resource = client.TypeOperation<Patient>("gpc.getcarerecord",parameters);
FhirSerializer.SerializeResourceToJson(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forDstu2();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.fhir.nhs.net/fhir/");
client.registerInterceptor(new LoggingInterceptor(true));

// Create the input parameters to pass to the server
Parameters inParams = new Parameters();
inParams.addParameter().setName("patientNHSNumber").setValue(new Identifier().setValue("P003").setSystem("http://fhir.nhs.net/Id/nhs-number"));
inParams.addParameter().setName("recordSection").setValue(new CodeableConcept().addCoding(new Coding().setCode("ALL").setSystem("http://fhir.nhs.net/ValueSet/gpconnect-record-section-1")));

Parameters outParams = client
		.operation()
		.onType(Patient.class)
		.named("gpc.getcarerecord")
		.withParameters(inParams)
		.execute();

Bundle responseBundle = (Bundle) outParams.getParameter().get(0).getResource();
System.out.println(ctx.newXmlParser().setPrettyPrint(true).encodeResourceToString(responseBundle));
```
