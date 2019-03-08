---
title: FHIR resource guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_resource_guidance.html
summary: "Where to find details of what resources and operations a FHIR server should expose to be a fully compliant GP Connect solution"
---

## Introduction

GP Connect versions 1.x use the [FHIR STU3](http://hl7.org/fhir/STU3/) standard to specify the API and profiles.

## Profiling principles

> Please see the [Data model principles](designprinciples_data_model_principles.html) page for further information.

## Profiles for each capability pack

The profiled FHIR resources required for each of the GP Connect capability packs are specified within the specific specification sections for each of the capabilities:

* [Foundations](datalibraryfoundation.html)
* [Access Record HTML](accessrecord.html)
* [Access Record Structured](accessrecord_structured_development_resources_overview.html)
* [Appointment Management](datalibraryappointment.html)

## General FHIR resource population requirements

### Population of optional elements

The purpose of GP Connect is to make the patient data stored within the GP systems available externally so that it can be used to help improve the quality of patient care across the NHS. To give patients the best care possible the data made available through the GP Connect API should be as complete as possible. Therefore, it is expected that both provider and consumers:

* ***SHALL*** populate all the elements within FHIR resources subject to any Capability-specific variance, where data is available within their system irrespective of the cardinality of the elements within the FHIR resource profiles.

As GP Connect has made the FHIR resources open to aid in interoperability this means that there are some elements included in FHIR profiles which are not applicable to our deployment settings, for example 'specialism' in the appointment resource. For these elements if the provider or consumer does not have data stored within their system the element will not be populated.

### Use of Must-Support flag

Some resource profiles used in GP Connect make use of the [Must-Support](https://www.hl7.org/fhir/STU3/conformance-rules.html#mustSupport) flag. 

Where a Must-Support flag is present on a resource element, a `consumer` system SHALL populate the field in the request body if data is available to do so, irrespective of the fact that field cardinality may be `0..1` or `0..*`. 

Similarly, `provider` systems SHALL populate an element in responses where data is available to do so, irrespective of optional cardinality. When a `provider` system receives data from a consumer for a field marked with the Must-Support flag, the provider system SHALL store this data field in such a way that the data element is preserved and the element can be populated in future responses to consumer requests for the resource in question.

If an element within a fhir profile is marked as must support then all sub elements of that element SHALL also be considered must support. For example, within the GP Connect Appointment profile the booking organization extension is flagged with must support on the extension, this means that the extension and all sub elements within the extension are must support and SHALL be stored in a way that the data is preserved and the booking organization can be populated in future responses to consumers requesting that resource.

For example, see the [Register a patient request body](foundations_use_case_register_a_patient.html#payload-request-body).


## FHIR resource element/data type specific population requirements

### id

The logical id of all FHIR resources SHALL be populated in accordance with the [FHIR specification requirements](https://www.hl7.org/fhir/STU3/resource.html#id), meaning that population of the element is expected.


### Address

The `Address` data type is used in many of the FHIR resources across the GP Connect API. Where an element using the `Address` data type is present in a FHIR resource the following population guidance SHALL be followed:

- The address SHALL be populated using the elements:
  - `line`
    - E.g. House name, flat number, house number and street & village or locality.  Multiple `line` elements SHALL be populated, where more than one line is present.
  - `city`
  - `district`
    - This element is to carry county, where present.
  - `postalCode`
  - `country`
- Where an element is not present, the element SHALL NOT be populated.
  
- The `text` element SHOULD NOT be populated within the address.

- `use` SHALL be populated for patient or patient contact addresses and SHOULD be populated in other contexts.

Example:

```
{
  "use": "home",
  "line": [
    "Trevelyan Square",
    "Boar Ln"
  ],
  "city": "Leeds",
  "district": "West Yorkshire",
  "postalCode": "LS1 6AE"
}
```

### ContactPoint

The `ContactPoint` data type is used in many of the FHIR resources across the GP Connect API. Where an element using the `ContactPoint` data type is present in a FHIR resource the following population guidance SHALL be followed:

- The telecom number or address (telephone number, email address etc) SHALL be populated in the `value` element
- `system` SHALL be populated in all circumstances
- `use` SHALL be populated for patient or patient contact telecom details and SHOULD be populated in other contexts.

Example:

```
{
  "system": "phone",
  "value": "01454587554",
  "use": "home"
}
```

### Patient.contact

The Patient.contact element SHALL be populated where demographic information is available in the Patient record for those individuals who may need to be contacted in connection with the Patient’s appointment.  In accordance with the FHIR definition, it is "Not applicable to register pedigree and family ties beyond use of having contact".

- `relationship.text` SHALL be populated with the type of relationship, for example *Emergency context*, *Next of kin*, or *Carer*.  The element SHALL also be used where a family relationship is recorded, for example *Daughter*.  Multiple relationship entries are allowed.
- `relationship.coding` SHALL NOT be populated
- `name`, `telecom`, `address`, `gender`, `organization` and `period` SHALL be populated where data is available
- `address` and `telecom` SHALL follow the [Address](development_fhir_resource_guidance.html#address) and [ContactPoint](development_fhir_resource_guidance.html#contactpoint) rules above for population of these elements

Example:

```
{
  "relationship": [
    {
      "text": "Emergency contact"
    },
    {
      "text": "Next of kin"
    },
    {
      "text": "Daughter"
    }
  ],
  "name": {
    "use": "official",
    "text": "JACKSON Jane (Miss)",
    "family": "Jackson",
    "given": [
      "Jane"
    ],
    "prefix": [
      "Miss"
    ]
  },
  "telecom": [
    {
      "system": "phone",
      "value": "07777123123",
      "use": "mobile"
    }
  ],
  "address": {
    "use": "home",
    "type": "physical",
    "line": [
      "Trevelyan Square",
      "Boar Ln"
    ],
    "city": "Leeds",
    "district": "West Yorkshire",
    "postalCode": "LS1 6AE"
  },
  "gender": "female"
}
```

### Bundle.entry.fullUrl

When populating a `Bundle` resource, providers SHALL populate the `Bundle.entry.fullUrl` element where there is a [read](https://www.hl7.org/fhir/STU3/http.html#read) endpoint for the resource.

So for example, the `Appointment` resource has a read endpoint `/Appointment/[id]` provided by [Read an appointment](appointments_use_case_read_an_appointment.html) and therefore `Bundle.entry.fullUrl` is populated for resources of this type, whereas `Slot` and `Schedule` resources do not have a read endpoint and therefore `Bundle.entry.fullUrl` is not be populated for resources of these types. `Slot` has a [search](https://www.hl7.org/fhir/STU3/http.html#search) endpoint, though this does not allow a single resource to be read directly and, therefore cannot be used when populating `fullUrl`.

Providers SHALL populate `Bundle.entry.fullUrl` with an absolute version independent URL to the resource. The URL SHALL end with the logical id of the resource, and SHALL NOT contradict the resource's `id` element.

The example below shows a `Bundle` containing a Practitioner with `fullUrl` populated and a `Slot` without `fullUrl` populated.

```json
{
  "resourceType": "Bundle",
  "type": "searchset",
  "entry": [
    {
      "fullUrl": "https://gpconnect.aprovider.nhs.net/GP001/STU3/1/Practitioner/2",
      "resource": {
        "resourceType": "Practitioner",
        "id": "2",
        "meta": {
          "versionId": "636064088099800115",
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1"
          ]
        },
        "identifier": [
          {
            "system": "https://fhir.nhs.uk/Id/sds-user-id",
            "value": "S001"
          }
        ],
        "name": {
          "family": [ "Black" ],
          "given": [ "Sarah" ],
          "prefix": [ "Mrs" ]
        },
        "gender": "female"
      }
    },
    {
      "resource": {
        "resourceType": "Slot",
        "id": "1584",
        "meta": {
          "versionId": "1471219260000",
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Slot-1"
          ]
        },
        "extension": [
          {
            "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-GPConnect-DeliveryChannel-2",
            "valueCode": "In-person"
          }
        ],
        "schedule": {
          "reference": "Schedule/14"
        },
        "status": "free",
        "start": "2016-08-15T11:30:00.000+01:00",
        "end": "2016-08-15T11:59:59.000+01:00"
      }
    },
    ...
  ]
}
```