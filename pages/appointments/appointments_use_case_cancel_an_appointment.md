---
title: Cancel an appointment
keywords: appointments, use case, cancel, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_cancel_an_appointment.html
summary: "Cancel an appointment for a patient at an organisation"
---

## Use case ##

This API is used to cancel a patient's future appointment, obtained via use of either Retrieve a Patient's Appointments, or Read an Appointment APIs.

Any future appointment, irrespective of booking organisation and irrespective of whether the appointment was booked via the GP Connect API, can be cancelled by a consuming organisation participating with the appointment hosting organisation in a GP Connect deployment.

The typical flow to cancel an appointment is:

 1. Search by NHS number for, or otherwise obtain, a `Patient` resource.
 2. Search for `Appointment` resources for the `Patient` resource.
 3. Choose an `Appointment` resource and cancel it by amending the `status` to `cancelled`.

{% include important.html content="The Appointment Management capability is aimed at administration of a patient's appointments. As a result of information governance (IG) requirements, the cancel appointments capability has been restricted to future appointments. More details are available on the [Design decisions](appointments_design.html#viewing-and-amending-booked-appointments) page." %}
 
## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details 

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR&reg; endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service.
- SHALL have previously found the appointment ID using [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html).

## API usage ##

The consumer system SHALL only use the cancel appointment capability to cancel future appointments where appointment start dateTime is after the current date and time. If the appointment start date is in the past the provider SHALL return an error.

### Request operation ###

#### FHIR relative request ####

```http
PUT /Appointment/[id]
```

#### FHIR absolute request ####

```http
PUT https://[proxy_server]/https://[provider_server]/[fhir_base]/Appointment/[id]
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (that is, GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:cancel:appointment-1` |
| `If-Match`           | The Appointment's current [ETag](development_general_api_guidance.html#managing-resource-contention), e.g. `W/"23"` |

#### Payload request body ####

The request payload is a profiled version of the standard FHIR&reg; [Appointment](https://www.hl7.org/fhir/STU3/appointment.html) resource. See the [FHIR resources](/datalibraryappointment.html) page for more details.

Consumer systems:
- SHALL send an `Appointment` resource that conforms to the [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) profile.
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the appointment resource.

  {% include important.html content="It is recommended that Consumers read the Appointment they wish to cancel (via Read an appointment or Retrieve a patient's appointments), then update the fields allowed below in place. Attempting to recreate the Appointment resource from local transformed data formats/structures is not advised, and may result in the provider system rejecting the amendment due to an unintended change or missing field." %}

Only the following data elements can be modified when performing an appointment cancellation:
- the appointment `status` MUST be updated to "cancelled"
- the appointment `cancellation-reason` extension SHALL be included with the cancellation reason details

  {% include important.html content="If any content other than the appointment cancellation reason or appointment status is updated the server SHALL reject the amendment and return an error." %}

  {% include note.html content="GP Connect does not impose a character limit on the cancellation reason extension within the cancellation request, but due to differences in the provider system the cancellation reason may be truncated when stored in the provider system due to character limits." %}

#### Error handling ####

The provider system:

- SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional details when one or more data fields are corrupt or a specific business rule/constraint is breached.
- SHALL return an error if any appointment details other than the appointment `status` and `cancellation-reason` fields are attempted to be updated.
- SHALL return an error if the appointment being cancelled is in the past (the appointment start dateTime is before the current date and time).
- SHALL return an error if the version identifier in the `If-Match` header does not match the Appointment's current version identifier.  See [Managing resource contention](development_general_api_guidance.html#managing-resource-contention).

Refer to [Development - FHIR API guidance - error handling](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful execution of the operation.
- SHALL return an `Appointment` resource that conform to the [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) profile.
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the returned appointment resource.
- SHALL include the `versionId` of the current version of each appointment resource.
- SHALL have updated the appointment `status` to "cancelled".
- SHALL have updated the appointment `cancellation-reason` in line with any details supplied in the request.

- SHALL populate `serviceType.text` with the practice defined slot type description, and where available `serviceCategory.text` with a practice defined schedule type description (may be called session name or rota type).

- SHALL populate a reference to a `HealthcareService` in the `Appointment.participant.actor` element where:
  - the Appointment is [linked to a service](appointments_serviceid_configuration.html#linking-services-to-schedules) set up for service ID filtering
  - and the service ID filtering [organisation switch](appointments_serviceid_configuration.html#organisation-switch) is set to ON

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields where data is available, excluding those listed below

- SHALL NOT populate the following fields:
  - `reason`
  - `specialty`

{% include important.html content="A status response `200` **OK** implies that the state of any resources affected by the appointment cancellation (for example, the associated `Slot`) subsequently reflects the cancellation (for example, `Appointment.status`, `Slot.status` are updated in line with any internal integrity constraints)." %}

## Examples ##

### Cancel an appointment ###

#### Request ####

```http
{% include appointments/cancel-appt-request-header-1.txt %}
```

```json
{% include appointments/cancel-appt-request-payload-1.json %}
```

#### Response ####

```json
{% include appointments/cancel-appt-response-payload-1.json %}
```
