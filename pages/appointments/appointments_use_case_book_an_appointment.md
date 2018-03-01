---
title: Book an appointment for a patient at an organisation
keywords: appointments, use case, book, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_book_an_appointment.html
summary: "Use case for booking an appointment for a patient with a given organisation."
---

## Use case ##

{% include important.html content="The Appointment Management capability pack is aimed at administration of a patient's appointments. As a result of information governance (IG) requirements the book appointment capability has been restricted to future appointments. See [Design decisions](appointments_design.html#viewing-and-amending-booked-appointments)." %}

The typical flow to book an appointment is:

 1. Search by `NHS Number` for, or otherwise obtain, a `Patient` resource.
 2. Search for available `Slot` resources by date range.
 3. Create an `Appointment` for the chosen `Slot` and `Patient` resources.

Refer to [Consumer sessions illustrated](appointments_consumer_sessions.html) for how this API use case could be used in the context of a typical consumer appointment management session.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details 

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR&reg; endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL have previously traced the patient's NHS Number using the [Personal Demographics Service]( https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service.
- SHALL have previously obtained the details for one or more free slots that are to be booked.
- SHALL have previously performed a GP Connect `Find a Patient` request to obtain the logical identifier for the patient on the organisation's FHIR server.

## API usage ##

The consumer system SHALL only use the book appointment capability to book future appointments, where the appointment start dateTime is after the current date and time. If the appointment start date is in the past the provider SHALL return an error.

### Request operation ###

#### FHIR&reg; relative request ####

```http
POST /Appointment
```

#### FHIR absolute request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Appointment
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:create:appointment-1` |


#### Payload request body ####

The request payload is a profiled version of the standard FHIR [Appointment](https://www.hl7.org/fhir/STU3/appointment.html) resource. See the [FHIR resources](/datalibraryappointment.html) page for more detail.

Consumer systems:
- SHALL send an `Appointment` resource that conforms to the [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) profile.
- SHALL include the URI of the `GPConnect-Appointment-1` profile StructureDefinition in the `Appointment.meta.profile` element of the appointment resource.

The following data elements are mandatory (that is, data MUST be present):
- a patient `participant` of the appointment.
- a location `participant` of the appointment, representing the physical location where the appointment is to take place (see [Design decisions](foundations_design.html#location-in-the-appointment-resource) page).
- an `actor` reference in any supplied `participant`.
- the `start` and `end` of the appointment.
- the `status` identifying the appointment as "booked".
- the `slot` details of one or more free slots to be booked.
- the `bookingOrganisation` extension referencing a `contained` `organization` resource within the appointment resource.
  - the contained organization resource SHALL represent the organization booking the appointment.
  - the contained organization resource SHALL conform to [CareConnect-GPC-Organization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1) profile.
  - the contained organization resource SHALL contain at least `Name` and `Telecom` details.
- the `created` element SHALL be populated with the date and time the appointment was created.

The following data elements SHOULD be included when available:
- a practitioner `participant` of the appointment.

{% include important.html content="Multiple adjacent free slots can be booked using the same appointment (that is, two 15 minute slots to obtain one 30 minute consultation). Details on how providers will indicate that slots can be considered adjacent can be found in the [Payload response body](appointments_use_case_search_for_free_slots.html#payload-response-body) section of the [Search for free slots](appointments_use_case_search_for_free_slots.html) API use case page." %}

{% include note.html content="The provider system receiving the bookingOrganization details SHALL store, return and display these details as required by the [Must-Support](development_fhir_api_guidance.html#use-of-must-support-flag) flag." %}


#### Element specific guidance ####

The following guidance around the Appointment resource element SHALL be followed when populating any of the listed fields:

| Resource Element        | Guidance |
| ---                     | --- |
| Appointment.***description*** | This field SHALL be populated with a "Summary Label", a brief description of the appointment as would be shown on a subject line in a meeting request, or appointment list. Consumers SHALL impose a character limit of 100 characters for this element. |
| Appointment.***comment***     | This field SHALL be used for "Patient specific notes" and any additional comments relating to the appointment. Consumers SHALL impose a character limit of 500 characters for this element. |
| Appointment.***reason***     | Consumers and providers SHOULD NOT use the appointment `reason` element as the GP Connect appointment management capability is for administration of appointment booting and should not be used to transfer clinical data between systems. As the reason element is for recording 'clinical' codes it goes against the purpose of the GP Connect Appointment Management capability, so it should not be used by consumers or providers. |

#### Resource guidance ####

The following guidance SHALL be followed when populating an appointment resource:

* For providers who only support the mandatory `description` element and not the `comment` element. If a `comment` is received as part of the booking the provider SHOULD append the content of the comment to the description within the appointment so that the additional information is not lost. The consumer imposed character limit specified above should restrict the total number of characters received so that all providers can store any text they receive.
* If the consumer wishes to include ***patient temporary contact details*** for the purposes of the appointment they SHALL include them within the `description` element of the appointment, so that the details are retained against that specific appointment.
* Elements within the appointment (such as 'comment' and 'description') SHALL only contain limited amounts of information to support the appointment. The content of the appointment SHALL NOT be used for "Transfer of Care" clinical information.

{% include warning.html content="Due to differences in the provider systems and the amount of information their data models can hold, there is a risk that information sent within the appointment may be truncated by the provider system if too large. Consumers and providers should be aware and try to limit risk where possible or make users aware of the risk when booking or amending an appointment. The consumer imposed character limit specified above should help mitigate this risk." %}


#### Example request body ####

On the wire, a JSON serialised request would look something like the following:

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

#### Error handling ####

Provider systems:

- SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more request fields are corrupt or a specific business rule/constraint is breached.

For example:

- the submitted `start` and `end` date range does not match that of the requested `Slot(s)`
- one or more of the requested `Slot` resources does not exist or already has a `status` of busy

Refer to [Development - FHIR API guidance - error handling](development_fhir_error_handling_guidance.html) for details of error codes.

{% include important.html content="Provider systems MAY implement business rules to protect the responsible use of the booking API, in line with current business rules already in place, to prevent misuse of appointment booking outside of the GP Connect API implementation." %}


### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `201` **Created** HTTP status code on successful execution of the operation.
- SHALL return a `Location` header as described in [FHIR API guidance](development_fhir_api_guidance.html#create-resource).
- SHALL return an `Appointment` resource that conform to the [GPConnect-Appointment-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Appointment-1) profile.
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

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library, which is the official .NET API for HL7&reg; FHIR&reg;." %}

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
