---
title: Register a patient
keywords: foundations, patient, nhsnumber, pid, register
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_register_a_patient.html
summary: "Use case for registering a patient with an organization."
---

## API Use Case ##

This specification describes a single use case. For complete details and background please see the [Foundations Capability Bundle](foundations.html).

{% include note.html content="This API use case is designed only to support the need to  register a **temporary** patient at a federated organisation as an enabler for federated appointment bookings. It is not a full patient registration endpoint, and does not change a patients' registered practice information as held on Personal Demographics Service (PDS)" %}

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously traced the patient's NHS Number using PDS or an equivalent service.
- SHALL have previously ascertained that the patient isn't already registered at the provider organisation.

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
POST /Patient/$gpc.registerpatient
```

#### FHIR Absolute Request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/$gpc.registerpatient
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient`|

Example HTTP request headers:

```http
POST http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/Patient/$gpc.registerpatient HTTP/1.1
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
Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient
```

#### Payload Request Body ####

The following data-elements are mandatory (i.e. data SHALL be present):

- A `registerPatient` patient resource profiled to `gpconnect-register-patient-1`. This is the patient who you want to be registered. Within this resource: 
	-  The NHS Number and Date of Birth as a minimum SHALL be populated to enable a provider to perform a PDS trace.
	- Where the gender and name are available these SHALL be supplied (as indicated by the [Must-Support](https://www.hl7.org/fhir/DSTU2/conformance-rules.html#mustSupport) FHIR property)

The request payload is a set of [Parameters](https://www.hl7.org/fhir/DSTU2/parameters.html) conforming to the `gpconnect-registerpatient-operation-1` profiled `OperationDefinition`, see below:

{% include tip.html content="This is a type level operation (i.e. is not associated with a given resource instance)." %} 

```xml
<OperationDefinition>
    <id value="0857bd2a-9c1f-4e2a-ac48-f6a81f88ab01" />
    <meta>
        <versionId value="1" />
        <lastUpdated value="2016-11-07T12:21:35.991+00:00" />
        <tag>
            <system value="urn:hscic:examples" />
            <code value="Operation-Register-Patient" />
            <display value="Register Patient Operation" />
        </tag>
    </meta>
    <url value="http://fhir.nhs.net/OperationDefinition/gpconnect-registerpatient-operation-1" />
    <version value="0.0.1" />
    <name value="GPConnect-RegisterPatient-Operation-1" />
    <status value="active" />
    <kind value="operation" />
    <publisher value="NHS Digital" />
    <contact>
        <name value="Interoperability Team" />
        <telecom>
            <system value="email" />
            <value value="interoperabilityteam@nhs.net" />
            <use value="work" />
        </telecom>
    </contact>
    <date value="2016-08-03T00:00:00+01:00" />
    <description value="Request to register a patient at a healthcare organisation" />
    <code value="gpc.registerpatient" />
    <system value="false" />
    <type value="Patient" />
    <instance value="false" />
    <parameter>
        <name value="registerPatient" />
        <use value="in" />
        <min value="1" />
        <max value="1" />
        <documentation value="Patient demographic information captured in the patient resource to register the patient." />
        <type value="Patient" />
        <profile>
            <reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-register-patient-1" />
        </profile>
    </parameter>
    <parameter>
        <name value="response" />
        <use value="out" />
        <min value="1" />
        <max value="1" />
        <documentation value="The searchset bundle resource that has been returned in response to the given input parameters" />
        <type value="Bundle" />
        <profile>
            <reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-registerpatient-bundle-1" />
        </profile>
    </parameter>
</OperationDefinition>
```

{% include important.html content="Provider systems SHALL register the new `Patient` resource as a temporary patient record once a PDS trace has been confirmed." %}

On the wire a JSON serialised `$gpc.registerpatient` request would look something like the following:

```json
{
	"resourceType": "Parameters",
	"parameter": [{
		"name": "registerPatient",
		"resource": {
			"resourceType": "Patient",
			"identifier": [{
				"system": "http://fhir.nhs.net/Id/nhs-number",
				"value": "1234569999"
			}],
			"active": true,
			"name": [{
				"use": "official",
				"family": ["Smith"],
				"given": ["Mike"]
			}],
			"gender": "male",
			"birthDate": "1976-01-10"
		}
	}]
}
```

#### Error Handling ####

The Provider system SHALL return an error if:

- the `registerPatient` is invalid.
- the `registerPatient` doesn't include a single active NHS Number identifier.
- the `registerPatient` demographics don't match that of the triggered PDS trace.

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

- SHALL return a `200` **OK** HTTP status code on successful registration of the patient into the provider system.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned response.
- SHALL return a searchset `Bundle` profiled to `gpconnect-searchset-bundle-1` including the following resources 
	- `Patient` profiled to `gpconnect-patient-1` containing details of the newly registered patient. This will include details sourced from PDS.
	- `Practitioner` profiled to `gpconnect-practitioner-1`
	- `Organization` profiled to `gpconnect-organization-1`

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
			"id": "9",
			"meta": {
				"versionId": "636180880331209494",
				"lastUpdated": "2016-08-10T13:35:57.319+01:00",
				"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-register-patient-1"]
			},
			"identifier": [{
				"system": "http://fhir.nhs.net/Id/nhs-number",
				"value": "1234569999"
			}],
			"name": [{
				"use": "official",
				"family": ["Smith"],
				"given": ["Mike"]
			}],
			"gender": "male",
			"birthDate": "10/01/1976"
		}
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
parameters.Add("registerPatient", new Patient
{
	Active = true,
	BirthDate = "1976-01-10",
	Gender = (AdministrativeGender)Enum.Parse(typeof(AdministrativeGender),"Male"),
	Name = new List<HumanName>
	{
		new HumanName()
		{
			Given = new[] {"Mike"},
			Family = new[] {"Smith"},
			Use = HumanName.NameUse.Official
		}
	},
	Identifier =
	{
		new Identifier("http://fhir.nhs.net/Id/nhs-number","1234569999")
	}
});
var resource = client.TypeOperation("gpc.registerpatient","Patient",parameters);
FhirSerializer.SerializeResourceToJson(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forDstu2();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/");
client.registerInterceptor(new LoggingInterceptor(true));

Patient patient = new Patient();
patient.addIdentifier()
   .setSystem("http://fhir.nhs.net/Id/nhs-number")
   .setValue("1234569999");
patient.addName()
   .addFamily("Smith")
   .addGiven("Mike")
   .setUse(NameUseEnum.OFFICIAL);
patient.setGender(AdministrativeGenderEnum.MALE);
patient.setBirthDate(new DateDt("1976-01-10"));

// Create the input parameters to pass to the server
Parameters inParams = new Parameters();
inParams.addParameter().setName("registerPatient").setValue(patient);

Parameters outParams = client
		.operation()
		.onType(Patient.class)
		.named("gpc.registerpatient")
		.withParameters(inParams)
		.execute();

Bundle responseBundle = (Bundle) outParams.getParameter().get(0).getResource();
System.out.println(ctx.newXmlParser().setPrettyPrint(true).encodeResourceToString(responseBundle));
```
