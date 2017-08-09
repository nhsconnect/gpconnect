---
title: Get the FHIR Conformance Statement
keywords: foundations, fhir
tags: [foundations,use_case,fhir]
sidebar: foundations_sidebar
permalink: foundations_use_case_get_the_fhir_conformance_profile.html
summary: "Use case for getting the GP Connect FHIR server's conformance statement."
---

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
GET /metadata
```

#### FHIR Absolute Request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/metadata
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata`|

#### Payload Request Body ####

N/A

#### Error Handling ####

Provider systems are expected to always be able to return a valid conformance statement.

### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful retrival of the conformance statement.
- SHALL ensure that the FHIR version number returned by the FHIR server endpoint conformance statement matches the FHIR version stated in the endpoint base URL. Refer to [Spine Directory Services](integration_spine_directory_service.html) for details of the format of the FHIR base URL to be used. 

An example GP Connect Conformance Statement of type `Instance` is shown below ready for customisation and embedding into GP Connect assured provider systems.

```xml
<Conformance xmlns="http://hl7.org/fhir">
	<version value="1.0.0-rc.1" />
	<name value="GP Connect" />
	<status value="draft" />
	<experimental value="true" />
	<publisher value="NHS Digital" />
	<contact>
		<name value="Software Vendor Contact Name" />
	</contact>
	<date value="2016-08-08" />
	<description value="This server is a reference implementation of the GP Connect FHIR APIs" />
	<copyright value="Copyright NHS Digital 2016" />
	<software>
		<name value="Software Name" />
		<version value="Software Verson" />
		<releaseDate value="Software Release Date" />
	</software>
	<fhirVersion value="1.0.2" />
	<acceptUnknown value="both" />
	<format value="application/xml+fhir" />
	<format value="application/json+fhir" />
	<profile>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-device-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-location-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-organization-1"/>
 		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-patient-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/gpconnect-practitioner-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/GPConnect-Appointment-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/GPConnect-Schedule-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/GPConnect-Slot-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/GPConnect-Schedule-Operation-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/GPConnect-GetSchedule-Bundle-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/GPConnect-Register-Patient-1"/>
		<reference value="http://fhir.nhs.net/StructureDefinition/GPConnect-RegisterPatient-Bundle-1"/>
	</profile>
	<rest>
		<mode value="server" />
		<security>
			<cors value="true" />
			<certificate>
				<blob />
			</certificate>
		</security>
		<resource>
			<type value="Patient" />
			<interaction>
				<code value="read" />
			</interaction>
			<interaction>
				<code value="search-type" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="NHS Number (i.e. http://fhir.nhs.net/Id/nhs-number|123456789)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Organization" />
			<interaction>
				<code value="read" />
			</interaction>
			<interaction>
				<code value="search-type" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="ODS Code (i.e. http://fhir.nhs.net/Id/ods-organization-code|Y12345) OR ODS Site Code (i.e. http://fhir.nhs.net/Id/ods-site-code|Y12345678)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Practitioner" />
			<interaction>
				<code value="read" />
			</interaction>
			<interaction>
				<code value="search-type" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="SDS User Id (i.e. http://fhir.nhs.net/sds-user-id|999999)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Appointment" />
			<interaction>
				<code value="read" />
			</interaction>
			<interaction>
				<code value="create" />
			</interaction>
			<interaction>
				<code value="vread" />
			</interaction>
			<interaction>
				<code value="update" />
			</interaction>
			<interaction>
				<code value="search-type" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="NHS Number (i.e. http://fhir.nhs.net/Id/nhs-number|123456789)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Location" />
			<interaction>
				<code value="read" />
			</interaction>
			<interaction>
				<code value="search-type" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="ODS Code (i.e. http://fhir.nhs.net/Id/ods-organization-code|Y12345) OR ODS Site Code (i.e. http://fhir.nhs.net/Id/ods-site-code|Y12345678)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Order" />
			<interaction>
				<code value="create" />
			</interaction>
			<interaction>
				<code value="search-type" />
			</interaction>
			<versioning value="versioned" />
			<readHistory value="false" />
			<updateCreate value="false" />
		</resource>
		<operation>
			<name value="gpc.getcarerecord" />
			<definition>
				<reference value="OperationDefinition/gpc.getcarerecord" />
			</definition>
		</operation>
		<operation>
			<name value="gpc.getschedule" />
			<definition>
				<reference value="OperationDefinition/gpc.getschedule" />
			</definition>
		</operation>
		<operation>
			<name value="gpc.registerpatient" />
			<definition>
				<reference value="OperationDefinition/gpc.registerpatient" />
			</definition>
		</operation>
	</rest>
	<rest>
		<mode value="server" />
	</rest>
</Conformance>
```

{% include tip.html content="Please see capability packs for examples of conformance statements specific to those capabilities" %}
- [Access Record Conformance Statement](accessrecord_development_conformance_profile.html)


Consumer Systems:

- SHALL, during development, request the conformance statement from the FHIR server endpoint in order to ascertain details of the implementation of GPConnect capabilities delivered by the FHIR server.
- SHOULD, at run-time, request the conformance statement from the FHIR server endpoint in order to ascertain details of the implementation of GPConnect capabilities delivered by the FHIR server.
- SHOULD cache conformance statement information retrieved from an endpoint at run-time on a per-session basis. 

### C# client request to get the conformance statement ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Conformance();
FhirSerializer.SerializeResourceToXml(resource).Dump();
```