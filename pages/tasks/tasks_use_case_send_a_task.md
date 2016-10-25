---
title: Send a task
keywords: tasks, use case, receive
tags: [tasks,use_case]
sidebar: tasks_sidebar
permalink: tasks_use_case_send_a_task.html
summary: "Use case for sending a task."
---

## Introduction ##

All resources and API interactions SHALL use [FHIR&reg; DSTU2](http://hl7.org/fhir/DSTU2/history.html) constructs.

## Use Case ##

For further details and clinical background please see [Task Management - Clinical Scenarios](tasks_clinical_scenarios.html)

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a Json Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- SHALL have previously traced the patient's NHS Number using PDS or an equivalent service.
- SHALL hold an up to date<sup>1</sup> record of GP Practice ODS Codes<sup>2</sup>.
- SHALL hold an up to date<sup>1</sup> record of GP Practitioner Organisation Codes<sup>2</sup>.

<sup>1</sup> The commissioning healthcare organisation SHALL define how often the GP Practice & GP Practitioner Provider Directory is updated.

<sup>2</sup> Details of GP Practice & GP Practitioners is available [periodically](http://systems.digital.nhs.uk/data/ods/guidance/schedule) from the NHS Digital run [Technology Reference data Update Distribution site](https://isd.hscic.gov.uk/trud3/user/guest/group/0/home) commonly known as [TRUD](https://isd.hscic.gov.uk/trud3/user/guest/group/0/home).

## API Usage ##

### Request Operation ###

#### FHIR Relative Request ####

```http
POST /Order
```

#### FHIR Absolute Request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Order
```

#### Request Headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:create:order`|

#### Payload Request Body ####

The request payload is a profiled version of the standard FHIR [Order](https://www.hl7.org/fhir/DSTU2/order.html) resource.

The following data-elements are mandatory (i.e data MUST be present).

- the `date` of when the order was made.
- the patient `subject` of the order.
- the `source` organisation of the sender.
- the `target` organisation of the recipient.
- the free-text `detail`<sup>1</sup> of what action is being ordered.
- the `taskType` identifying if this task requires a follow-up action.

<sup>1</sup> The free-text detail of what is being ordered will be encoded as a FHIR [Basic](https://www.hl7.org/fhir/DSTU2/basic.html) resource using a [Contained Reference](https://www.hl7.org/fhir/DSTU2/references.html#contained). Hence, the `detail` [Reference](https://www.hl7.org/fhir/DSTU2/references.html) is expected to be a pointer to the contained resource.

The Consumer system SHALL have resolved the patient `subject` reference from the Provider system.

Provider systems SHALL only expose `Patient` resources for patient's who have a valid PDS trace status.

For example, on the wire serialised as JSON this looks like the following:

```json
{
	"resourceType": "Order",
	"contained": [{
		"resourceType": "Basic",
		"id": "ad6a2e86-37a8-43c9-b0ae-f2adcff4de3a",
		"text": {
			"div": "<div>Please review the patient's medications at the next available opportunity.</div>"
		},
		"code": {
			"coding": [{
				"system": "http://hl7.org/fhir/basic-resource-type",
				"code": "OrderDetails"
			}]
		}
	}],
	"date": "23/07/2016",
	"subject": {
		"reference": "Patient/1",
		"display": "Mrs Jane Johnson"
	},
	"source": {
		"reference": "Organization/1",
		"display": "GP Super Clinic"
	},
	"target": {
		"reference": "Organization/2",
		"display": "GP Clinic Down The Road"
	},
	"reasonCodeableConcept": {
		"coding": [{
			"system": "http://fhir.nhs.net/ValueSet/gpconnect-reason-type-1",
			"code": "1"
		}],
		"text": "For your information"
	},
	"detail": [{
		"reference": "#ad6a2e86-37a8-43c9-b0ae-f2adcff4de3a"
	}]
}
```

The Consumer system SHALL populate the `subject`, `source` and `target` reference fields on the `Order` with the relative URL details of the remote resource (i.e. as it's represented on the Provider system).

The Consumer system SHALL populate the `detail` reference with a [Contained Resource](https://www.hl7.org/fhir/DSTU2/references.html#contained) reference to be included in the body of the `Order`.

#### Error Handling ####

The Provider system SHALL return an error if:

- one or more mandatory fields are not supplied.
- one or more `Reference` fields (i.e. subject, target etc.) don't resolve locally on the Provider system to a valid FHIR resource.
- the `subject` patient's record is not associated with a `NHS Number Status Indicator Code` of `Number present and verified`.
- the `date` is not today's date (i.e. is in the past).
- the `target` GP organisation has no existing direct care relationship with the patient.
- the `record` is invalild (i.e. isn't from the correct value set).

Servers are permitted to reject creating a task (i.e. `Order`) because of integrity concerns or other business rules, and return HTTP status codes accordingly (usually a `422` **Unprocessable Entity**).

Provider systems SHALL return an [OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached.

### Request Response ###

As specified in [FHIR Guidance - Common API Guidance](development_fhir_api_guidance.html) if no `return=minimal` header is specified in the `POST` request the `return=representation` behaviour will be used and the response body SHALL contain the full details of the newly created resource.

#### Response Headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload Response Body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful receipt and storage of a new task (i.e. Order).
- SHALL return as the response payload body in-line with the guidance provider in the [Development - FHIR API Guidance - Common API Guidance - Create Resource](development_fhir_api_guidance.html) section.
- SHALL include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned response.
- SHALL include the `versionId` of the current version of each `Order` resource.
- SHALL generate a business identifier to allow an individual task (i.e. `Order` resource) to be uniquely identifiable.

```json
{
	"resourceType": "Order",
	"id": "2",
	"meta": {
		"versionId": "636062814622034751",
		"lastUpdated": "2016-07-08T20:31:02.625+01:00"
	},
	"contained": [{
		"resourceType": "Basic",
		"id": "fa5db35a-af22-4d7c-aa59-74bc696d38e8",
		"text": {
			"div": "<div>Please review the patient's medications at the next available opportunity.</div>"
		},
		"code": {
			"coding": [{
				"system": "http://hl7.org/fhir/basic-resource-type",
				"code": "OrderDetails"
			}]
		}
	}],
	"date": "8/08/2016",
	"subject": {
		"reference": "http://gpconnect.fhir.nhs.net/fhir/Patient/1"
	},
	"source": {
		"reference": "http://gpconnect.fhir.nhs.net/fhir/Organization/1"
	},
	"target": {
		"reference": "http://gpconnect.fhir.nhs.net/fhir/Organization/2"
	},
	"reasonCodeableConcept": {
		"coding": [{
			"system": "http://fhir.nhs.net/ValueSet/gpconnect-reason-type-1",
			"code": "1"
		}],
		"text": "For your information"
	},
	"detail": [{
		"reference": "#fa5db35a-af22-4d7c-aa59-74bc696d38e8"
	}]
}
```

## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
var orderDetails = new Basic
{
	Id = Guid.NewGuid().ToString(),
	Text = new Narrative {
		Div = "<div>Please review the patient's medications at the next available opportunity.</div>"
	},
	Code = new CodeableConcept("http://hl7.org/fhir/basic-resource-type","OrderDetails")
};
var order = new Order
{
	Date = DateTime.Now.Date.ToShortDateString(),
	Subject = new ResourceReference {
		Display = "Mrs Jane Johnson",
		Reference = ResourceType.Patient + "/1"
	},
	Source = new ResourceReference {
		Display = "GP Super Clinic",
		Reference = ResourceType.Organization + "/1"
	},
	Target = new ResourceReference {
		Display = "GP Clinic Down The Road",
		Reference = ResourceType.Organization + "/2"
	},
	Contained = new List<Resource>() {
		orderDetails,
	},
	Reason = new CodeableConcept(null,null,"Reason for the appointment."),
	Detail = new List<ResourceReference> {
		new ResourceReference {
		 Reference = "#" + orderDetails.Id,
		}	
	}
};
FhirSerializer.SerializeResourceToJson(order).Dump();
var createdOrder = client.Create<Order>(order);
FhirSerializer.SerializeResourceToJson(createdOrder).Dump();
```

### Java ###

```java
Hello World
```
