---
title: Book an appointment for a patient at an organisation
keywords: appointments, use case, book, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_book_an_appointment.html
summary: "Use case for booking an appointment for a patient with a given organisation."
---

## Use Case ##

The typical flow to book an appointment is:

 1. Search by `NHS Number` for, or otherwise obtain, a `Patient` resource.
 2. Search for available `Slot` resources by date range.
 3. Create an `Appointment` for the chosen `Slot` and `Patient` resources.

Refer to [Consumer sessions illustrated](appointments_consumer_sessions.html) for how this API Use Case could be used in the context of a typical consumer appointment management session.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint Base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service.
- SHALL have previously obtained the details for one or more free slots that are to be booked.
- SHALL have previously performed a GP Connect `Find a Patient` request to obtain the logical identifier for the patient on the organisation's fhir server.

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
POST /Appointment
```

#### FHIR Absolute Request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Appointment
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment` |


#### Payload Request Body ####

The request payload is a profiled version of the standard FHIR [Appointment](https://www.hl7.org/fhir/STU3/appointment.html) ![STU3](images/stu3.png) resource, see [FHIR Resources](/datalibraryappointment.html) page for more detail.

Consumer systems:
- SHALL send an `Appointment` resource that conform to the [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) ![STU3](images/stu3.png) profile.
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the appointment resource.

The following data-elements are mandatory (i.e data MUST be present).
- a patient `participant` of the appointment.
- a location `participant` of the appointment, representing the physical location where the appointment is to take place (see [design decisions](foundations_design.html#location-in-the-appointment-resource) page).
- an `actor` reference in any supplied `participant`
- the `start` and `end` of the appointment.
- the `status` identifying the appointment as "booked".
- the `slot` details of one or more free slots to be booked.
- the `bookingOrganisation` extension referencing a `contained` `organization` resource within the appointment resource.
  - the contained organization resource SHALL represent the organization booking the appointment.
  - the contained organization resource SHALL conform to [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) ![STU3](images/stu3.png) profile.
  - the contained organization resource SHALL contain at least `Name` and `Telecom` details.
- the `created` extension SHALL be populate with the date and time of the appointment was created.

The following data-elements SHOULD be included when available.
- a practitioner `participant` of the appointment.

{% include important.html content="Multiple adjacent free slots can be booked using the same appointment (i.e. two 15 minute slots to obtain one 30 minute consultation). Details on how providers will indicate that slots can be considered adjacent can be found in the [Payload Response Body](appointments_use_case_search_for_free_slots.html#payload-response-body) section of the [Search for free slots](appointments_use_case_search_for_free_slots.html) API Use Case page." %}

The following guidance around Appointment Resource element should be followed when populating any of the listed fields:

| Resource Element        | Guidance |
| ---                     | --- |
| Appointment.***comment***     | This field should be used for "Patient specific notes" and any additional comments relating to the appointment. |
| Appointment.***description*** | This field should be populated with a "Summary Label", a brief description of the appointment as would be shown on a subject line in a meeting request, or appointment list. |

{% include note.html content="For providers who only support the mandatory `description` element and not the `comment` element, if a `comment` is received as part of the booking the provider SHOULD append the content of the comment to the description within the appointment so that the additional information is not lost." %}

#### Example Request Body ####

On the wire a JSON serialised request would look something like the following:

```json
{
	"resourceType": "Appointment",
	"meta": {
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1"]
	},
	"contained": [{
		"resourceType": "Organization",
		"id": "1",
		"meta": {
			"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"]
		},
		"name": "Test Organization Name",
		"telecom": [{
			"system": "phone",
			"value": "0300 303 5678"
		}]
	}],
	"extension": [{
		"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-GPConnect-BookingOrganisation-1",
		"valueReference": {
			"reference": "#1"
		}
	}],
	"status": "booked",
	"description": "Free text description.",
	"start": "2016-05-30T10:00:00+01:00",
	"end": "2016-05-30T10:25:00+01:00",
	"slot": [{
		"reference": "Slot/1",
		"display": "Slot 1"
	}],
	"created": "2017-10-09T13:48:41+01:00",
	"comment": "Free text comment.",
	"participant": [{
		"actor": {
			"reference": "Patient/1",
			"display": "Mr. Mike Smith"
		},
		"status": "accepted"
	},
	{
		"actor": {
			"reference": "Location/32",
			"display": "Leeds GP Clinic"
		},
		"status": "accepted"
	}]
}
```

#### Error Handling ####

Provider systems:

- SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) ![STU3](images/stu3.png) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached.

For example:

- the submitted `start` and `end` date range does not match that of the requested `Slot(s)`.
- one or more of the requested `Slot` resources does not exist or already has a `status` of busy.

Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes.

{% include important.html content="Provider systems MAY implement business rules to protect the responsible use of the booking API, in line with current business rules already in place to prevent misuse of appointment booking outside of the GPConnect API implementation." %}


### Request Response ###

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `201` **Created** HTTP status code on successful execution of the operation.
- SHALL return a `Location` header as described in [FHIR API Guidance](development_fhir_api_guidance.html#create-resource).
- SHALL return an `Appointment` resource that conform to the [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) ![STU3](images/stu3.png) profile.
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the returned appointment resource.
- SHALL include the `versionId` of the current version of each appointment resource.

```json
{
	"resourceType": "Appointment",
	"id": "9",
	"meta": {
		"versionId": "636068818095315079",
		"lastUpdated": "2016-08-15T19:16:49.971+01:00",
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1"]
	},
	"contained": [{
		"resourceType": "Organization",
		"id": "1",
		"meta": {
			"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"]
		},
		"name": "Test Organization Name",
		"telecom": [{
			"system": "phone",
			"value": "0300 303 5678"
		}]
	}],
	"extension": [{
		"url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-GPConnect-BookingOrganisation-1",
		"valueReference": {
			"reference": "#1"
		}
	}],
	"status": "booked",
	"description": "Free text description.",
	"start": "2016-05-30T10:00:00+01:00",
	"end": "2016-05-30T10:25:00+01:00",
	"slot": [{
		"reference": "Slot/1",
		"display": "Slot 1"
	}],
	"created": "2017-10-09T13:48:41+01:00",
	"comment": "Free text comment.",
	"participant": [{
		"actor": {
			"reference": "Patient/1",
			"display": "Mr. Mike Smith"
		},
		"status": "accepted"
	},
	{
		"actor": {
			"reference": "Location/32",
			"display": "Leeds GP Clinic"
		},
		"status": "accepted"
	}]
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");
client.PreferredFormat = ResourceFormat.Json;

Appointment appointment = new Appointment();

appointment.Status = Appointment.AppointmentStatus.Booked;
appointment.Start = System.DateTimeOffset.Now;
appointment.End = System.DateTimeOffset.Now.AddMinutes(30);

var slotReference = new ResourceReference();
slotReference.Reference = "Slot/1982";
appointment.Slot.Add(slotReference);

var patientParticipant = new Appointment.ParticipantComponent();
patientParticipant.Actor = new ResourceReference();
patientParticipant.Actor.Reference = "Patient/2";
patientParticipant.Status = Appointment.ParticipationStatus.Accepted;
appointment.Participant.Add(patientParticipant);

var locationParticipant = new Appointment.ParticipantComponent();
locationParticipant.Actor = new ResourceReference();
locationParticipant.Actor.Reference = "Location/1";
locationParticipant.Status = Appointment.ParticipationStatus.Accepted;
appointment.Participant.Add(locationParticipant);

appointment.created = new FhirDateTime(DateTime.Now);
Organization organization = new Organization();
organization.Name = "Example Organization Name";
var contactPoint = new ContactPoint();
contactPoint.System = ContactPoint.ContactPointSystem.Phone;
contactPoint.Value = "0300 303 5678";
organization.Telecom.Add(contactPoint);
organization.Id = "1";
appointment.Contained.Add(organization);
var reference = new ResourceReference
{
Reference = "#1",
};
appointment.AddExtension("https://fhir.nhs.uk/StructureDefinition/extension-gpconnect-booking-organisation-1", reference);

Appointment appointmentCreated = client.Create<Appointment>(appointment);

FhirSerializer.SerializeResourceToJson(appointmentCreated).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext fhirContext = FhirContext.forStu3();
IGenericClient client = fhirContext.newRestfulGenericClient("http://gpconnect.aprovider.nhs.net/GP001/STU3/1/");

Appointment appointment = new Appointment();
appointment.setStatus(AppointmentStatusEnum.BOOKED);

Calendar startTime = Calendar.getInstance();
Calendar endTime = Calendar.getInstance();
endTime.add(Calendar.MINUTE, 30);
appointment.setStart(new InstantDt(startTime));
appointment.setEnd(new InstantDt(endTime));

appointment.setSlot(Collections.singletonList(new ResourceReferenceDt("Slot/1982")));

Appointment.Participant patientParticipant = new Appointment.Participant();
patientParticipant.setActor(new ResourceReferenceDt("Patient/2"));
patientParticipant.setStatus(ParticipationStatusEnum.ACCEPTED);
appointment.addParticipant(patientParticipant);

Appointment.Participant locationParticipant = new Appointment.Participant();
locationParticipant.setActor(new ResourceReferenceDt("Location/1"));
locationParticipant.setStatus(ParticipationStatusEnum.ACCEPTED);
appointment.addParticipant(locationParticipant);

Organization organization = new Organization();
organization.setName("Test Organization Name");
ContactPointDt telecom = new ContactPointDt();
telecom.setSystem(ContactPointSystemEnum.PHONE);
telecom.setValue("0300 303 5678");
organization.setTelecom(Collections.singletonList(telecom));

ExtensionDt extension = new ExtensionDt(false);
extension.setUrl("https://fhir.nhs.uk/StructureDefinition/extension-gpconnect-booking-organisation-1");
extension.setValue(new ResourceReferenceDt(organization));
appointment.addUndeclaredExtension(extension);

MethodOutcome response = client.create()
	.resource(appointment)
	.prefer(PreferReturnEnum.REPRESENTATION)
	.preferResponseType(Appointment.class)
	.execute();

System.out.println(fhirContext.newJsonParser().setPrettyPrint(true).encodeResourceToString(response.getResource()));
```