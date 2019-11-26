---
title: Get the FHIR conformance statement
keywords: foundations, fhir
tags: [foundations,use_case,fhir]
sidebar: foundations_sidebar
permalink: foundations_use_case_get_the_fhir_conformance_profile.html
summary: "Use case for getting the GP Connect FHIR server's conformance statement"
---

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

Consumers **MUST** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:metadata`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems are expected to always be able to return a valid conformance statement.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- **MUST** return a `200` **OK** HTTP status code on successful retrieval of the conformance statement
- **MUST** ensure that the FHIR version number returned by the FHIR server endpoint conformance statement matches the FHIR version stated in the endpoint base URL. Refer to [Spine Directory Services](integration_spine_directory_service.html) for details of the format of the FHIR base URL to be used. 

An example GP Connect Conformance Statement of type `capability` is shown below ready for customisation and embedding into GP Connect assured provider systems. Providers should use this conformance statement as a base for their own conformance statement, replacing the element in square brackets (`[` & `]`) with specific information of their implementation. The main version at the top of the conformance statement should represent the GP Connect specification version which the FHIR server implements.

```json
{
   "version": {
      "value": "0.7.2"
   },
   "name": {
      "value": "GP Connect"
   },
   "publisher": {
      "value": "[Provider Software Vendor Name]"
   },
   "contact": {
      "name": {
         "value": "[Provider Software Vendor Contact Name]"
      }
   },
   "date": {
      "value": "2018-02-23"
   },
   "description": {
      "value": "This server implements the GP Connect API version 0.7.2"
   },
   "copyright": {
      "value": "Copyright NHS Digital 2016"
   },
   "kind": {
      "value": "capability"
   },
   "software": {
      "name": {
         "value": "[Provider Software Name]"
      },
      "version": {
         "value": "[Provider Software Version]"
      },
      "releaseDate": {
         "value": "[Provider Software Release Date]"
      }
   },
   "fhirVersion": {
      "value": "1.0.2"
   },
   "acceptUnknown": {
      "value": "both"
   },
   "format": [
      {
         "value": "application/xml+fhir"
      },
      {
         "value": "application/json+fhir"
      }
   ],
	"profile": {
		  "reference": [
			 {
				"reference": "http://fhir.nhs.net/StructureDefinition/gpconnect-patient-1"
			 },
			 {
				" reference ": "http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"
			 },
			 {
				" reference ": "http://fhir.nhs.net/StructureDefinition/gpconnect-practitioner-1"
			 },
			 {
				" reference ": "http://fhir.nhs.net/StructureDefinition/gpconnect-organization-1"
			 },
			 {
				" reference ": "http://fhir.nhs.net/StructureDefinition/gpconnect-searchset-bundle-1"
			 },
			 {
				" reference ": "http://fhir.nhs.net/StructureDefinition/gpconnect-carerecord-composition-1"
			 }
		  ]
	   },
   "rest": {
      "mode": {
         "value": "server"
      },
      "operation": {
         "name": {
            "value": "gpc.getcarerecord"
         },
         "definition": {
            "reference": {
               "value": "OperationDefinition/gpc.getcarerecord"
            }
         }
      }
   }
}
```

Consumer systems:

- **SHOULD**, at run-time, request the conformance statement from the FHIR server endpoint in order to ascertain details of the implementation of GP Connect capabilities delivered by the FHIR server
- **SHOULD** cache conformance statement information retrieved from an endpoint at run-time on a per-session basis

### C# client request to get the conformance statement ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/DSTU2/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Conformance();
FhirSerializer.SerializeResourceToXml(resource).Dump();
```
