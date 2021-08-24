---
title: Retrieve a patient's appointments
keywords: appointments, use case, retrieve
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_retrieve_a_patients_appointments.html
summary: "Retrieve a patient's future appointments at an organisation"
---

## Use case ##

This specification describes a single use case enabling the consumer to retrieve a patient's future appointment bookings from a targeted provider system. 

All future appointments for the requested patient, irrespective of the booking organisation, and irrespective of whether the appointment was booked via the GP Connect API, will be returned from the provider system.

{% include important.html content="The Appointment Management capability pack is aimed at administration of a patient's appointments. As part of information governance (IG) requirements the retrieval of a patient's appointments has been restricted to future appointments only. Additional details are available on the [Design decisions](appointments_design.html#viewing-and-amending-booked-appointments) page." %}

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( integration_personal_demographic_service.html) or an equivalent service
- SHALL have previously [resolved the logical ID of the patient](foundations_use_case_find_a_patient.html) on the server using the NHS Number

## Consumer display requirements ##

Consumer systems SHALL support the following fields in order to provide the full context of the appointment: 

- Start date and time
- End date and time, or duration
- Delivery channel (in-person, telephone, video)
- Slot type and schedule type (see `Appointment.serviceType` and `Appointment.serviceCategory`)
- Service name (where present, see [service ID filtering](appointments_serviceid_filtering.html) for more information)
- Location name and address
- Practitioner role (e.g. General Medical Practitioner, Nurse)
- Practitioner name and gender

Consumer systems displaying a list of a patient's appointments SHALL use [Read practitioner](foundations_use_case_read_a_practitioner.html), [Read location](foundations_use_case_read_a_location.html) and [Read healthcare service](foundations_use_case_read_a_healthcareservice.html) endpoints to retrieve service, location and practitioner fields associated with the patient's appointments.

## API usage ##

### Request operation ###

#### Search parameters ####

Provider systems SHALL implement the following search parameters:

| Name | Type | Description | Paths |
| --- | --- | --- | --- |
| `start` | `date` | Appointment start date | `Appointment.start` |


Consumer systems:
- SHALL include two `start` search parameter with every request
  - One of the `start` search parameter SHALL be supplied with the `ge` search prefix. For example, `start=ge2017-09-22`, which indicates that the consumer would like appointments where the appointment start date is on or after "2017-09-22".
  - One of the `start` search parameter SHALL be supplied with the `le` search prefix. For example, `start=le2017-09-25`, which indicates that the consumer would like appointments where the appointment start date is on or before "2017-09-25"
- SHALL only include the date component of the search parameter and not a time component. The date SHALL include day, month and year elements.
- SHALL NOT request a date range where any part of the date range is in the past
- SHALL indicate to the end user that only appointments in the future will be returned from GP Connect and that the earliest that the user can request appointments is today's date

  ![Diagram - Date range parameters](images/appointments/RetrievePatientsApp.png)

Provider systems:
- SHALL support the search prefixes `ge` and `le`
- SHALL return an error if any part of the consumer requested search range is in the past
  - If the consumer sends today's date the provider SHALL return all appointments for today, if the appointments are in the past because the current time is after the appointment time but the appointment start date is today's date, then the appointment SHALL still be returned in the response bundle
  - The error returned SHALL include a meaningful error message to indicate that the search parameters cannot request appointments in the past
- SHALL return an error if either of the date parameters contain a time element
- SHALL return an error if either of the two start date parameters are not sent with the consumers request

#### FHIR relative request ####


```http
GET /Patient/[id]/Appointment?start=ge[lower_date_range_boundary]&start=le[upper_date_range_boundary]
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/[id]/Appointment?start=ge[lower_date_range_boundary]&start=le[upper_date_range_boundary]
```

#### Example request ####

Retrieve all appointments for patient with logical id 1001 which start on or between 2017-07-11 and 2017-09-14:

```json
GET /Patient/1001/Appointment?start=ge2017-07-11&start=le2017-09-14
```


#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:patient_appointments-1` |

#### Payload request body ####

N/A

### Error handling ###

Provider systems:

- SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached. Refer to [Development - FHIR API guidance - error handling](development_fhir_error_handling_guidance.html) for details of error codes.
- SHALL return an error if any part of the consumer supplied date range is in the past. The OperationOutcome returned SHALL include a meaningful error message to indicate that the search parameters can not request appointments in the past.
- Where the use of the `start` search parameter does not define a valid date range, `HTTP Status code 422` with error code `INVALID_PARAMETER` will be returned. Additional details SHALL be returned in the diagnostics element.


### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL only return appointments where the `start` element is in the future (greater than or equal to the current date)
- SHALL return a `200` **OK** HTTP status code on successful execution of the operation
- SHALL return zero or more matching [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) resources in a `Bundle` of `type` searchset
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the returned `Appointment` resources
- SHALL include the versionId of the current version of each `Appointment` resource returned
- SHALL return all appointments for the patient within the requested period signified by the `start` search parameter(s). All appointments including cancelled appointments should be returned as part of the response, no additional filtering should be applied.

- SHALL populate `Appointment.start`, `Appointment.end`, `Appointment.created` elements in (UK) local time in the format `yyyy-mm-ddThh:mm:ss+hh:mm`, with the timezone offset `+00:00` for UTC and `+01:00` for BST

- SHALL populate `Appointment.serviceType.text` with the practice defined slot type description, and where available `Appointment.serviceCategory.text` with a practice defined schedule type description (may be called session name or rota type).

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields where data is available, excluding those listed below

- SHALL NOT populate the following fields:
  - `reason`
  - `specialty`

```json
{% include appointments/retrieve_patients_appts_response_example.json %}
```