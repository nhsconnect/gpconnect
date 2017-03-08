---
title: Get the FHIR Conformance Statement
keywords: foundations, fhir
tags: [foundations,use_case,fhir]
sidebar: foundations_sidebar
permalink: foundations_use_case_get_the_fhir_conformance_profile.html
summary: "Use case for getting the GP Connect FHIR server's conformance statement."
---

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

{% include important.html content="The following draft conformance statement does not contain details for resource profiles that are to be accessed though the searchset bundles." %}

{% gist michaelmeasures/486aa287a7ea5911fa9de6c55b0d46bb %}

Consumer Systems:

- SHALL, during development, request the conformance statement from the FHIR server endpoint in order to ascertain details of the implementation of GPConnect capabilities delivered by the FHIR server.
- SHOULD, at run-time, request the conformance statement from the FHIR server endpoint in order to ascertain details of the implementation of GPConnect capabilities delivered by the FHIR server.
- SHOULD cache conformance statement information retrieved from an endpoint at run-time on a per-session basis. 

### C# client request to get the conformance statement ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Conformance();
FhirSerializer.SerializeResourceToXml(resource).Dump();
```