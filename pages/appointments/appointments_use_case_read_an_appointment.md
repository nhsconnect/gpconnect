---
title: Read an appointment
keywords: appointments, use case, read
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_read_an_appointment.html
summary: "Read a patient's appointment at an organisation"
---


## Use case ##

This specification describes a single use case enabling the consumer application to obtain the details of a specific future appointment from a targeted provider system.

A patient's future appointment, irrespective of the booking organisation, and irrespective of whether the appointment was booked via the GP Connect API, is  returned by the provider system.

{% include important.html content="The Appointment Management capability pack is aimed at the administration of a patient's appointments. As a result of information governance (IG) requirements, the read appointments capability has been restricted to future appointments. More details are available on the [Design decisions](appointments_design.html#viewing-and-amending-booked-appointments) page." %}


## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer application:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API usage ##

The consumer application SHALL only use the read appointment capability to retrieve future appointments, where the appointment start dateTime is after the current date and time. If the appointment start date is in the past the provider SHALL return an error.


### Request operation ###

#### FHIR relative request ####

```http
GET /Appointment/[id]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Appointment/[id]
```

#### Request headers ####

Consumer applications SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:read:appointment-1`|

#### Payload request body ####

N/A

#### Error handling ####

Provider systems:
- SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.
- SHALL return an error if the appointment being read is in the past (the appointment start dateTime is before the current date and time).

Examples of other scenarios which may result in error being returned:
- Where a logical identifier of the resource is not valid/can't be found on the server, a 404 HTTP Status code would be returned with the relevant OperationOutcome resource.
- Where insufficient data about an appointment is present in the provider system to populate an appointment resource which validates to the `GPConnect-Appointment-1` profile, a 500 HTTP Status code should be returned, together with the appropriate OperationOutcome resource providing diagnostic detail.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return `Appointment` resources that conform to the [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) resource profile.
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the returned appointment resource.
- SHALL include the `versionId` of the current version of the appointment resource.
- SHALL include all relevant business `identifier` details (if any) for the appointment resource.

- SHALL populate `Appointment.start`, `Appointment.end`, `Appointment.created` elements in (UK) local time in the format `yyyy-mm-ddThh:mm:ss+hh:mm`, with the timezone offset `+00:00` for UTC and `+01:00` for BST

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields where data is available, excluding those listed below

- SHALL NOT populate the following fields:
  - `reason`
  - `specialty`

```json
{
  "resourceType": "Appointment",
  "id": "148",
  "meta": {
    "versionId": "1503310820000",
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1"
    ]
  },
  "contained": [
    {
      "resourceType": "Organization",
      "id": "1",
      "meta": {
        "profile": [
          "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"
        ]
      },
      "identifier": [
        {
          "system": "https://fhir.nhs.uk/Id/ods-organization-code",
          "value": "A00001"
        }
      ],
      "type": [
        {
          "coding": [
            {
              "system": "https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1",
              "code": "gp-practice"
            }
          ]
        }
      ],
      "name": "Test Organization Name",
      "telecom": [
        {
          "system": "phone",
          "value": "0300 303 5678"
        }
      ]
    }
  ],
  "extension": [
    {
      "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-GPConnect-BookingOrganisation-1",
      "valueReference": {
        "reference": "#1"
      }
    },
    {
      "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-GPConnect-PractitionerRole-1",
      "valueCodeableConcept": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-SDSJobRoleName-1",
            "code": "R0260",
            "display": "General Medical Practitioner"
          }
        ]
      }
    },
    {
      "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-GPConnect-DeliveryChannel-2",
      "valueCode": "In-person"
    }
  ],
  "status": "booked",
  "description": "GP Connect Appointment description 148",
  "start": "2017-08-21T10:20:00+01:00",
  "end": "2017-08-21T10:50:00+01:00",
  "slot": [
    {
      "reference": "Slot/544"
    },
    {
      "reference": "Slot/545"
    },
    {
      "reference": "Slot/546"
    }
  ],
  "created": "2017-07-09T13:48:41+01:00",
  "comment": "Test Appointment Comment 148",
  "participant": [
    {
      "actor": {
        "reference": "Patient/2"
      },
      "status": "accepted"
    },
    {
      "actor": {
        "reference": "Location/1"
      },
      "status": "accepted"
    },
    {
      "actor": {
        "reference": "Practitioner/2"
      },
      "status": "accepted"
    }
  ]
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library, which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;
var resource = client.Read<Appointment>("Appointment/148");
FhirSerializer.SerializeResourceToJson(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forStu3();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1");
Appointment appointment = client.read().resource(Appointment.class).withId("148").execute();
System.out.println(fhirContext.newJsonParser().setPrettyPrint(true).encodeResourceToString(appointment));
```
