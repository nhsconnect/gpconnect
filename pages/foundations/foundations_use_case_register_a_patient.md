---
title: Register a patient
keywords: foundations, patient, nhsnumber, pid, register
tags: [foundations,use_case]
sidebar: foundations_sidebar
permalink: foundations_use_case_register_a_patient.html
summary: "Use case for registering a patient with an organization."
---

## API Use Case ##

The "Register a patient" capability should either create a new temporary patient registration or re-activate an existing "Inactive" patient registration, as a temporary patient registration within the GP Practice system ([Definition of a GP Connect Active Patient](/overview_glossary.html#active-patient)).

This specification describes a single use case. For complete details and background please see the [Foundations Capability Bundle](foundations.html).

{% include note.html content="This API use case is designed only to support the need to  register a **temporary** patient at a federated organisation as an enabler for federated appointment bookings. It is not a full patient registration endpoint, and does not change a patients' registered practice information as held on Personal Demographics Service (PDS)" %}

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service.


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
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient-1`|

Example HTTP request headers:

```http
POST http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/Patient/$gpc.registerpatient HTTP/1.1
User-Agent: .NET FhirClient for FHIR 1.2.0
Accept: application/fhir+json;charset=utf-8
Prefer: return=representation
Host: michaelm-pc
Content-Type: application/fhir+json;charset=utf-8
Content-Length: 289
Expect: 100-continue
Connection: Keep-Alive
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:operation:gpc.registerpatient-1
```

#### Payload Request Body ####

The following data-elements are mandatory (i.e. data SHALL be present):
- A `registerPatient` parameter containing a patient resource profiled to the [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) profile. This is the patient who you want to be registered. Within this resource: 
	- The NHS Number and Date of Birth as a minimum SHALL be populated to enable a provider to perform a PDS trace.
	- Where the gender, name or birth date are available these SHALL also be supplied (as indicated by the [Must-Support](https://www.hl7.org/fhir/STU3/conformance-rules.html#mustSupport) FHIR property)
    - The consumer SHALL NOT populate the "registrationDetails" extension within the patient resource.
	- The patient resource SHALL contain at least a single name element. The patient resource SHALL contain a single instance of the name element with the `use` of `official`. This official name should contain the name registered on the spine which is returned by a PDS lookup for the patient.

The following data-elements SHOULD be populated if available:
- Within the patient resource of the `registerPatient` parameter:
  - the `telecom` element SHOULD be populated
	- the consumer SHALL NOT populate the `telecom.use` value with `old`
	- the consumer SHOULD populate only one `telecom` per `telecom.use` value

  - the `address` element SHOULD be populated
	- the consumer SHALL NOT populate the `address.use` value with `old`
	- the consumer SHOULD populate only one `address` per `address.use` value
	- the `address.use` value `home` SHOULD be mapped to PDS Address Use `HP` (Primary Home)

  {% include note.html content="The consumer SHOULD include telecom and address information within the temporary patient registration so that the receiving system has relevant contact details for the patient." %}
  {% include note.html content="The provider system receiving the telecom and address details SHOULD store these details in addition to any telecom or address details obtained through the PDS trace done as part of the patient registration." %}
  
The request payload is a set of [Parameters](https://www.hl7.org/fhir/STU3/parameters.html) conforming to the `gpconnect-registerpatient-operation-1` profiled `OperationDefinition`, see below:

{% include tip.html content="This is a type level operation (i.e. is not associated with a given resource instance)." %} 

```xml
<OperationDefinition>
    <id value="0857bd2a-9c1f-4e2a-ac48-f6a81f88ab01" />
    <meta>
        <versionId value="1" />
        <lastUpdated value="2017-11-03T12:21:35.991+00:00" />
        <tag>
            <system value="urn:hscic:examples" />
            <code value="Operation-Register-Patient" />
            <display value="Register Patient Operation" />
        </tag>
    </meta>
    <url value="https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-Registerpatient-Operation-1" />
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
            <reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1" />
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
            <reference value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1" />
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
			"meta": {
				"profile": [
					"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"
				]
			},
			"identifier": [
				{
					"extension": [
						{
							"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-NHSNumberVerificationStatus-1",
							"valueCodeableConcept": {
								"coding": [
									{
										"system": "https://fhir.nhs.uk/CareConnect-NHSNumberVerificationStatus-1",
										"code": "01",
										"display": "Number present and verified"
									}
								]
							}
						}
					],
					"system": "https://fhir.nhs.uk/Id/nhs-number",
					"value": "9476719931"
				}
			],
			"name": [
				{
					"use": "official",
					"text": "Minnie DAWES",
					"family": "Jackson",
					"given": ["Jane"],
					"prefix": ["Miss"]
				}
			],
			"telecom": [
				{
					"system": "phone",
					"value": "01454587554",
					"use": "home"
				}
			],
			"gender": "female",
			"birthDate": "1952-05-31",
			"address": [
				{
					"use": "home",
					"type": "physical",
					"text": "Trevelyan Square, Boar Ln, Leeds, LS1 6AE"
					"address": {
						"line": [
							"Trevelyan Square",
							"Boar Ln",
							"Leeds"
						],
						"postalCode": "LS1 6AE"
					}
				}
			]
		}
	}]
}
```

#### Error Handling ####

The Provider system SHALL return an error if:

- the `registerPatient` is invalid.
- the `registerPatient` doesn't include a single active NHS Number identifier.
- the `registerPatient` demographics don't match that of the triggered PDS trace.

Provider systems SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request Response ###

#### Response Headers ####

```http
HTTP/1.1 200 OK
Cache-Control: no-store
Content-Type: application/fhir+json; charset=utf-8
Date: Sun, 07 Aug 2016 11:13:05 GMT
Content-Length: 1464
```

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful registration of the patient into the provider system.
- SHALL include the URI of the relevant GP Connect `StructureDefinition` profile in the `{Resource}.meta.profile` element of the returned resources.
- SHALL return a searchset `Bundle` profiled to [GPConnect-Searchset-Bundle-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1) including the following resources 
	- `Patient` profiled to [CareConnect-GPC-Patient-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) containing details of the newly registered or re-activated patient. This will include details sourced from PDS.
- SHALL populate the "registrationDetails" extension within the returned patient resource, within the "registrationDetails" extension:
  - The "registrationType" SHALL be populated with a value from the valueset which matches the registration type used within the provider system. If an appropriate registration type is not available within the valueset then the `Other` type SHALL be use and more detail around the specific type of registration SHOULD be added using the "text" element of the CodeableConcept.

```json
{
	"resourceType": "Bundle",
	"meta": {
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Searchset-Bundle-1"]
	},
	"type": "searchset",
	"entry": [{
		"resource": {
			"resourceType": "Patient",
			"id": "2",
			"meta": {
				"versionId": "1469448000000",
				"lastUpdated": "2016-07-25T12:00:00.000+00:00",
				"profile": [
					"https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"
				]
			},
			"extension": [{
				"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-RegistrationDetails-1",
				"extension": [{
						"url": "registrationPeriod",
						"valuePeriod": {
							"start": "2017-09-07T14:17:44+01:00"
						}
					},
					{
						"url": "registrationType",
						"valueCodeableConcept": {
							"coding": [{
								"system": "https://fhir.nhs.uk/CareConnect-RegistrationType-1",
								"code": "T"
							}]
						}
					},
					{
						"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-RegistrationDetails-1",
						"extension": [
							{
								"url": "preferredBranchSurgery",
								"valueReference": {
									"reference": "Location/785b4ff5-aced-4bdf-b7ed-34f92131ce97"
								}
							}
						]
					}]
			}],
			"identifier": [
				{
					"extension": [
						{
							"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-NHSNumberVerificationStatus-1",
							"valueCodeableConcept": {
								"coding": [
									{
										"system": "https://fhir.nhs.uk/CareConnect-NHSNumberVerificationStatus-1",
										"code": "01",
										"display": "Number present and verified"
									}
								]
							}
						}
					],
					"system": "https://fhir.nhs.uk/Id/nhs-number",
					"value": "9476719931"
				}
			],
			"active": true,
			"name": [
				{
					"use": "official",
					"text": "Minnie DAWES",
					"family": "Jackson",
					"given": ["Jane"],
					"prefix": ["Miss"]
				}
			],
			"telecom": [
				{
					"system": "phone",
					"value": "01454587554",
					"use": "home"
				}
			],
			"gender": "female",
			"birthDate": "1952-05-31",
			"address": [
				{
					"use": "home",
					"type": "physical",
					"text": "Trevelyan Square, Boar Ln, Leeds, LS1 6AE"
					"address": {
						"line": [
							"Trevelyan Square",
							"Boar Ln",
							"Leeds"
						],
						"postalCode": "LS1 6AE"
					}
				}
			]
		}
	}]
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
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
			Use = HumanName.NameUse.Usual
		}
	},
	Identifier =
	{
		new Identifier("https://fhir.nhs.uk/Id/nhs-number","1234569999")
	}
});
var resource = client.TypeOperation("gpc.registerpatient","Patient",parameters);
FhirSerializer.SerializeResourceToJson(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forStu3();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
Patient patient = new Patient();
patient.addIdentifier()
   .setSystem("https://fhir.nhs.uk/Id/nhs-number")
   .setValue("1234569999");
patient.addName()
   .addFamily("Smith")
   .addGiven("Mike")
   .setUse(NameUseEnum.USUAL);
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
