---
title: Retrieve a care record section
keywords: getcarerecord, section, html, view
tags: [use_case,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_use_case_retrieve_a_care_record_section.html
summary: "Use case for retrieving a care record section for a patient from a given organisation"
---

<a href="#" class="back-to-top">Back to Top</a>

## Use case ##

This specification describes a single use case. For complete details and background please see the [Access Record Capability Bundle](accessrecord.html).

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- **MUST** have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- **MUST** have previously traced the patient's NHS Number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service
- **MUST** render HTML content in-line with the [HTML Implementation Guidance](accessrecord_development_html_implementation_guide.html)

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
POST /Patient/$gpc.getcarerecord
```

#### FHIR absolute request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/$gpc.getcarerecord
```

#### Request headers ####

Consumers **MUST** include the following additional HTTP request headers:

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
Accept: application/json+fhir
Prefer: return=representation
Host: michaelm-pc
Content-Type: application/json+fhir
Content-Length: 289
Expect: 100-continue
Connection: Keep-Alive
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:operation:gpc.getcarerecord
```

#### Payload request body ####

The following data-elements are mandatory (meaning, data **MUST** be present):

- the `patientNHSNumber` is the NHS Number of the patient whose GP care record you want to access
- the `recordSection` is the GP care record section you wish to retrieve

The following data-elements are optional (meaning, **MAY** be supplied for certain care record sections):

- the `timePeriod` is the time period over which the requested information is to be returned

The request payload is a set of [Parameters](https://www.hl7.org/fhir/stu3/parameters.html) conforming to the `gpconnect-carerecord-operation-1` profiled `OperationDefinition`, see below:

{% include tip.html content="This is a type level operation (meaning, is not associated with a given resource instance)." %}

```xml
<OperationDefinition xmlns="http://hl7.org/fhir">
	<id value="getcarerecord" />
	<version value="0.7.2" />
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

{% include custominfocallout.html content="**Important:** Provider systems **MUST** only expose `Patient` resources for patients who have a valid PDS trace status." type="warning" %}

On the wire a JSON serialised `$gpc.getcarerecord` request would look something like the following:

```json
{
	"resourceType": "Parameters",
	"parameter": [{
		"name": "patientNHSNumber",
		"valueIdentifier": {
			"system": "http://fhir.nhs.net/Id/nhs-number",
			"value": "9480489457"
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

The provider system **MUST**:

- use a default time period if no `timePeriod` parameter is specified for a section that can accept a time period

<br/>
Refer to [HTML Implementation Guidance - Per Section Default Time Frames](accessrecord_development_html_layout_guide.html#per-section-default-time-frames) for details of the default time periods that **MUST** be applied per care record section.


#### Error handling ####

The provider system **MUST** return an error if:

- the `patientNHSNumber` is invalid (meaning, fails NHS Number format and check digit tests)
- the `patientNHSNumber` is not associated with a `NHS Number Status Indicator Code` of `Number present and verified`
- the GP organisation is not the patient's nominated primary care provider
- the `recordSection` is invalid (meaning, isn't from the correct value set)
- an invalid `timePeriod` is requested (i.e. end date > start date)
- a `timePeriod` is specified for a `recordSection` that is time period agnostic (for example, Patient Summary, Allergies etc.)
- the patient is recorded as deceased and the request is received after the allowed access period post patient's death. In this case, the error code "PATIENT_NOT_FOUND" should be returned.

Provider systems **MUST** return an [OperationOutcome](https://www.hl7.org/fhir/stu3/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

Refer to [Development Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####

```http
HTTP/1.1 200 OK
Cache-Control: no-store
Content-Type: application/json+fhir
Date: Sun, 07 Aug 2016 11:13:05 GMT
Content-Length: 1464
```

#### Payload response body ####

Provider systems:

- **MUST** return a `200` **OK** HTTP status code on successful retrieval of a care record section
- **MUST** return the care record section as valid XHTML in line with the [FHIR Narrative](https://www.hl7.org/fhir/stu3/narrative.html) guidance
- **MUST** include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned response
- **MUST** include the `Patient`, `Practitioner` and `Organization` details for the retrieved care record in a searchset `Bundle`
- **MUST** include patient's date of death in Patient.deceased\[x\](deceasedDateTime) where it is recorded in the provider system

```json
{
   "resourceType": "Bundle",
   "id": "48b4dc58-9c04-470d-a819-16fbb433daf9",
   "type": "searchset",
   "entry": [
      {
         "resource": {
            "resourceType": "Composition",
            "id": "77bf75df-3853-4b47-ab53-5edce53f8ee6",
            "meta": {
               "profile": [
                  "http://fhir.nhs.net/StructureDefinition/gpconnect-carerecord-composition-1"
               ]
            },
            "date": "2017-02-24T13:51:00+00:00",
            "title": "Patient Care Record",
            "status": "final",
            "subject": {
               "reference": "Patient/7302348e-e090-4c5d-99e9-14147c266ebe"
            },
            "author": [
               {
                  "reference": "Device/f4d020c6-eaff-4528-83ba-e81a1cfd30dc"
               }
            ],
            "custodian": {
               "reference": "Hl7.Fhir.Model.Organization",
               "display": "BRIDGE STREET SURGERY"
            },
            "section": [
               {
                  "title": "Allergies and Sensitivities",
                  "code": {
                     "coding": [
                        {
                           "system": "http://fhir.nhs.net/ValueSet/gpconnect-record-section-1",
                           "code": "ALL"
                        }
                     ],
                     "text": "Allergies and Sensitivities"
                  },
                  "text": {
                     "status": "generated",
                     "div": "<div><h1>Allergies and Adverse Reactions<\/h1><div><p><table><tr><td><p>All Data Items<\/p><\/td><\/tr><\/table><\/p><\/div><table><tr><td>Sensitive data has been excluded<\/td><\/tr><\/table><h2>Current Allergies and Adverse Reactions<\/h2><table><th>Start date<\/th><th>Details<\/th><tr><td>31 Oct 2016<\/td><td>Latex allergy<\/td><\/tr><\/table><h2>Historical Allergies and Adverse Reactions<\/h2><table><tr><td><p> This system does not support retrieval of Historical Allergies and Adverse Reactions data. <\/p><p>This data may still exist in the source system.<\/p><\/td><\/tr><\/table><\/div>"
                  }
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "Patient",
            "id": "7302348e-e090-4c5d-99e9-14147c266ebe",
            "meta": {
               "versionId": "1202600162206596780",
               "profile": [
                  "http://fhir.nhs.net/StructureDefinition/gpconnect-patient-1"
               ]
            },
            "identifier": [
               {
                  "system": "http://fhir.nhs.net/Id/nhs-number",
                  "value": "9480489457"
               }
            ],
            "name": [
               {
                  "family": [
                     "Dolby"
                  ],
                  "given": [
                     "Ivan"
                  ],
                  "prefix": [
                     "Mr"
                  ]
               }
            ],
            "gender": "male",
            "birthDate": "1923-03-02",
            "address": [
               {
                  "line": [
                     "",
                     "53 Burrett Road",
                     ""
                  ],
                  "city": "Wisbech",
                  "district": "0",
                  "postalCode": "PE13 3RT"
               }
            ],
            "careProvider": [
               {
                  "reference": "Practitioner/e26035eb-f0e6-4211-9997-6b5365a2eb76"
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "Organization",
            "id": "cafe1615-9232-47ae-80ea-e554f943fd9b",
            "meta": {
               "versionId": "9045189372685666075",
               "profile": [
                  "http://fhir.nhs.net/StructureDefinition/gpconnect-organization-1"
               ]
            },
            "identifier": [
               {
                  "system": "http://fhir.nhs.net/Id/ods-organization-code",
                  "value": "D82015"
               }
            ],
            "name": "BRIDGE STREET SURGERY",
            "address": [
               {
                  "use": "work",
                  "line": [
                     "Fulford Grange, Micklefield Lane",
                     "Rawdon",
                     "Rawdon"
                  ],
                  "city": "Leeds",
                  "district": "Yorkshire",
                  "postalCode": "LS19 6BA"
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "Device",
            "id": "5A084F08-29D0-4F5B-8809-D1F96578AFB1",
            "meta": {
               "versionId": "9008072080809363811",
               "profile": [
                  "http://fhir.nhs.net/StructureDefinition/gpconnect-device-1"
               ]
            },
            "identifier": [
               {
                  "system": "EMIS",
                  "value": "EMIS"
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "Practitioner",
            "id": "e26035eb-f0e6-4211-9997-6b5365a2eb76",
            "meta": {
               "versionId": "5944618252807509908",
               "profile": [
                  "http://fhir.nhs.net/StructureDefinition/gpconnect-practitioner-1"
               ]
            },
            "name": {
               "family": [
                  "Fidler"
               ],
               "given": [
                  "Josh"
               ],
               "prefix": [
                  "Mr"
               ]
            },
            "address": [
               {
                  "use": "work",
                  "line": [
                     "Fulford Grange, Micklefield Lane",
                     "Rawdon",
                     "Rawdon"
                  ],
                  "city": "Leeds",
                  "district": "Yorkshire",
                  "postalCode": "LS19 6BA"
               }
            ],
            "gender": "male"
         }
      }
   ]
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
FhirContext ctx = FhirContext.forstu3();
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
