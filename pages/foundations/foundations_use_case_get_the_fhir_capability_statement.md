---
title: Get the FHIR&reg; capability statement
keywords: foundations, fhir
tags: [foundations,use_case,fhir]
sidebar: foundations_sidebar
permalink: foundations_use_case_get_the_fhir_capability_statement.html
summary: "Use case for getting the GP Connect FHIR server's capability statement"
---

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)

## API usage ##

### Request operation ###

#### FHIR relative request ####

```http
GET /metadata
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/metadata
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems are expected to always be able to return a valid capability statement.

### Request response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful retrival of the capability statement
- SHALL return a capability statement which conforms to the standard [FHIR CapabilityStatement](http://hl7.org/fhir/STU3/capabilitystatement.html)

An example GP Connect CapabilityStatement is shown below ready for customisation and embedding into GP Connect assured provider systems. Providers should use this CapabilityStatement as a base for their own CapabilityStatement, replacing the element in square brackets (`[` & `]`) with specific information of their implementation. The main version at the top of the CapabilityStatement should represent the GP Connect specification version which the FHIR server implements.

```xml
<CapabilityStatement xmlns="http://hl7.org/fhir">

	<!-- the GP Connect specification name and version ------------------->
	<version value="1.2.0" />
	<name value="GP Connect" />
	
	<status value="active" />
	<date value="2018-02-23" />

	<!-- to be completed by the provider --------------------------------->
	<publisher value="[Provider software vendor name]" />
	<contact>
		<name value="[Provider software vendor contact name]" />
	</contact>

	<description value="This FHIR API implements the GP Connect specification" />
	<copyright value="Copyright NHS Digital 2018" />
	<kind value="capability" />

	<!-- to be completed by the provider --------------------------------->
	<software>
		<name value="[Provider software product name]" />
		<version value="[Provider software production version]" />
		<releaseDate value="[Provider software release date]" />
	</software>

	<fhirVersion value="3.0.1" />
	<acceptUnknown value="both" />
	<format value="application/fhir+json" />

	<!-- include only if provider supports XML --------------------------->
	<format value="application/fhir+xml" />

	<profile>

		<!-- Profiles: common to all capabilities -------------------->
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"/>
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"/>
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1"/>
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1"/>
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"/>

		<!-- Profiles: Appointment Management ------------------------>
 		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1"/>
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Schedule-1"/>
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Slot-1"/>

		<!-- Profiles: Access Record Structured ---------------------->
 		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"/>
 		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1"/>
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1"/>
		<reference value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"/>

	</profile>

	<rest>
		<mode value="server" />
		<security>
			<cors value="true" />
		</security>
		
		<!-- REST definitions: Foundations --------------------------->
		<resource>
			<type value="Patient" />
			<interaction>
				<code value="read" />
			</interaction>
			<interaction>
				<code value="search-type" />
			</interaction>
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="NHS Number (i.e. https://fhir.nhs.uk/Id/nhs-number|123456789)" />
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
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="ODS Code (i.e. https://fhir.nhs.uk/Id/ods-organization-code|Y12345)" />
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
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="SDS User Id (i.e. https://fhir.nhs.uk/Id/sds-user-id|999999)" />
			</searchParam>
		</resource>
		<resource>
			<type value="Location" />
			<interaction>
				<code value="read" />
			</interaction>
		</resource>

		<!-- REST definitions: Appointment Management ---------------->
		<resource>
			<type value="Slot" />
			<interaction>
				<code value="search-type" />
			</interaction>
			<searchParam>
				<name value="start" />
				<type value="date" />
			</searchParam>
			<searchParam>
				<name value="end" />
				<type value="date" />
			</searchParam>
			<searchParam>
				<name value="status" />
				<type value="token" />
			</searchParam>
			<searchParam>
				<name value="searchFilter" />
				<type value="token" />
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
				<code value="update" />
			</interaction>
			<interaction>
				<code value="search-type" />
			</interaction>
			<updateCreate value="false" />
			<searchParam>
				<name value="identifier" />
				<type value="token" />
				<documentation value="NHS Number (i.e. https://fhir.nhs.uk/Id/nhs-number|123456789)" />
			</searchParam>
		</resource>

		<!-- Operation definitions: Foundations ---------------------->
		<operation>
			<name value="gpc.registerpatient" />
			<definition>
				<reference value="https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-RegisterPatient-Operation-1" />
			</definition>
		</operation>

		<!-- Operation definitions: Access Record Structured --------->
		<operation>
			<name value="gpc.getstructuredrecord" />
			<definition>
				<reference value="https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1" />
			</definition>
		</operation>

	</rest>
</CapabilityStatement>
```

Consumer systems:
- SHOULD request the capability statement from the FHIR server endpoint in order to ascertain details of the implementation of GP Connect capabilities delivered by the FHIR server
- Consumers may also cache the capability statement information retrieved from an endpoint to reduce the number of future calls they make to to the target organization's FHIR server.

### C# client request to get the capability statement ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.CapabilityStatement();
FhirSerializer.SerializeResourceToXml(resource).Dump();
```
