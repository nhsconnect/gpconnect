---
title: Read an appointment
keywords: appointments, use case, read
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_read_an_appointment.html
summary: "Read a patient's appointment at an organisation"
---


## Use case ##

This specification describes a single use case enabling the consumer to obtain the details of a specific future appointment from a provider organisation.

A patient's future appointment, irrespective of the booking organisation, and irrespective of whether the appointment was booked via the GP Connect API, is returned by the provider system.

{% include important.html content="The Appointment Management capability is aimed at the administration of a patient's appointments. As a result of information governance (IG) requirements, the read appointments capability has been restricted to future appointments. More details are available on the [Design decisions](appointments_design.html#viewing-and-amending-booked-appointments) page." %}


## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)

## API usage ##

The consumer system SHALL only use the read appointment capability to retrieve future appointments, where the appointment start dateTime is after the current date and time. If the appointment start date is in the past the provider SHALL return an error.


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

Consumers SHALL include the following additional HTTP request headers:

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

- SHALL populate `Appointment.serviceType.text` with the practice defined slot type description, and where available `Appointment.serviceCategory.text` with a practice defined schedule type description (may be called session name or rota type).

- SHALL populate a reference to a `HealthcareService` in the `Appointment.participant.actor` element where:
  - the Appointment is [linked to a service](appointments_serviceid_configuration.html#linking-services-to-schedules) set up for service ID filtering
  - and the service ID filtering [organisation switch](appointments_serviceid_configuration.html#organisation-switch) is set to ON

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields where data is available, excluding those listed below

- SHALL NOT populate the following fields:
  - `reason`
  - `specialty`

## Examples ##

### Read an appointment by id ###

#### Request ####

```http
{% include appointments/read-appt-request-header-1.txt %}
```

#### Response ####

```json
{% include appointments/read-appt-response-payload-1.json %}
```
