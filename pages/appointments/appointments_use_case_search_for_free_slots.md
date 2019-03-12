---
title: Search for free slots
keywords: appointments, use case, search, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_search_for_free_slots.html
summary: "Search for free slots within a date range at an organisation"
---

## Use case ##

This specification describes a single use case enabling the consumer to request from the targeted provider system slots matching the selected date range, booking organisation ODS Code and Type, and other parameters including UC Disposition Code and Service ID. 

Refer to [Consumer sessions illustrated](appointments_consumer_sessions.html) for how this API use case could be used in the context of a typical consumer appointment management session.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- SHALL request a maximum date range covering a two-week period

{% include tip.html content="Multiple separate API calls can be made if a larger date range is required. However, consideration should be given to the load this placed on the provider system." %}

## Consumer display requirements ##

The fields below allow a patient to choose and attend an appointment appropriate to their needs.

In order to prevent incorrect or unsuitable bookings, and to allow a patient to attend the appointment at the correct time, place or via the correct delivery channel, consumer systems **SHALL** support the following fields: 

- Start date and time
- End date and time, or duration
- Delivery channel (in-person, telephone, video)
- Location name and address
- Practitioner role (e.g. General Medical Practitioner, Nurse)
- Practitioner name and gender

## Booking multiple adjacent slots ##

Please see the conditions in which a consumer may book multiple adjacent slots on the [Book an appointment](appointments_use_case_book_an_appointment.html#booking-multiple-adjacent-slots) page.

## API usage ##

### Parameters ###

#### Search parameters ####

Provider systems SHALL support the following search parameters:

| Name | Type | Description | Paths | Consumer to send? | 
|---|---|---|---|
| `status` | `token` | The free/busy status of the appointment | `Slot.status` | mandatory | 
| `start` | `date` | Slot start date, or date and time | `Slot.start` | mandatory | 
| `end` | `date` | Slot end date, or date and time | `Slot.end` | mandatory | 
| `searchFilter` | `token` &nbsp; &nbsp; &nbsp; | A generic token to pass additional search criteria &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; | *(n/a)* | required - see [enhanced slot filtering](#searchfilter-parameter-enhanced-slot-filtering) | 

Consumers SHALL send the following search parameters in the request:

- `status=free` specifies that only free slots will be returned. Note: the slot status value of `free` SHALL be specified, other slot status values are not permitted.
- The `start` parameter SHALL only be included once in the request.
- The `start` parameter SHALL be supplied with the `ge` search prefix. For example, `start=ge2017-09-22`, which indicates that the consumer would like slots where the slot start date is on or after "2017-09-22".
- The `end` parameter SHALL only be included once in the request.
- The `end` parameter SHALL be supplied with the `le` search prefix. For example, `end=le2017-09-26`, which indicates that the consumer would like slots where the slot end date is on or before "2017-09-26".
  
  ![Diagram - Date range parameters](images/appointments/SearchForFreeSlots.png)

{% include note.html content="Search for free slots does allow for searching for slots in the past, but all other appointment management capabilities do not allow for appointment management where the appointments start date element is in the past. Therefore, slots found in the past cannot be used to book an appointment." %}

#### _include parameters ####

Provider systems SHALL support the following _include parameters:

| Name and value | Description | Consumer to send? | 
|---|---|---|
| `_include=Slot:schedule` | Include referenced `Schedule` resources in the response | mandatory |
| `_include:recurse=Schedule:actor:Practitioner` | Include referenced `Practitioner` resources in the response | optional |
| `_include:recurse=Schedule:actor:Location` | Include referenced `Location` resources in the response | optional | 
| `_include:recurse=Location:managingOrganization` | Include referenced `Organization` resources in the response | optional |

Consumers SHALL send the following _include parameters in the request:

- `_include=Slot:schedule` specifies that associated `Schedule` resources are returned.

Consumers MAY send the following _include parameters in the request to minimise the number of API calls required to prepare an appointment booking:

- `_include:recurse=Schedule:actor:Practitioner`
- `_include:recurse=Schedule:actor:Location`
- `_include:recurse=Location:managingOrganization`

#### searchFilter parameter (enhanced slot filtering) ####

It is recognized that provider systems must offer GP practices more functionality to enable them to better manage their available appointment slots in the light of increasing access requirements from other organisations. In order to support this, GP Connect has specified additional [Slot availability management](appointments_slotavailabilitymanagement.html) providers requirements.

Provider systems SHALL support the following `searchFilter` parameters:

| Parameter name | Parameter value (system) | Parameter value (code) | Example value (code) | Consumer to send? | 
| --- | --- |
| `searchFilter` | `https://fhir.nhs.uk/Id/ods-organization-code` | Consumer ODS organisation code | `A11111`| required |
| `searchFilter` | `https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1` | Consumer ODS [organisation type](https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1) code | `urgent-care` | required |

Consumer systems SHOULD send the following `searchFilter` parameters in the request, populating both `system` and `code` elements of the search [token](https://www.hl7.org/fhir/STU3/search.html#token) using the format `parameterName=system|code`:

- `searchFilter` with a system of `https://fhir.nhs.uk/Id/ods-organization-code` and a value containing the consumer system's ODS organization code
- `searchFilter` with a system of `https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1` and a value containing the consumer system's organization type code

{% include important.html content="The `searchFilter` parameters enable providers to return slots to consumers that are restricted to the consumer's organisation type or code.  Consumers not sending `searchFilter` parameters will not receive these restricted slots." %}

Where search filters are sent by consumers which are not explicitly supported in this specification (for example, urgent care use a disposition code value set), providers who do not understand the additional parameters SHALL ignore them and SHALL NOT return an error.

### Example requests ###

On the wire, a search for free slots request sending all parameters would look something like the following:

```http
GET /Slot?start=ge2017-10-20T00:00:00&end=le2017-10-31T23:59:59&status=free&_include=Slot:schedule&_include:recurse=Schedule:actor:Practitioner&_include:recurse=Schedule:actor:Location&_include:recurse=Location:managingOrganization&searchFilter=https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1|gp-practice&searchFilter=https://fhir.nhs.uk/Id/ods-organization-code|A1001
```

A search for free slots request sending only mandatory and required parameters would look something like the following:

```http
GET /Slot?start=ge2017-10-20T00:00:00&end=le2017-10-31T23:59:59&status=free&_include=Slot:schedule&searchFilter=https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1|gp-practice&searchFilter=https://fhir.nhs.uk/Id/ods-organization-code|A1001
```


### Request operation ###

#### FHIR relative request ####

```http
GET /Slot?[start={search_prefix}start_date]
          [&end=[{search_prefix}end_date]
          [&status=free]
          [&_include=Slot:schedule]
          {&_include:recurse=Schedule:actor:Practitioner}
          {&_include:recurse=Schedule:actor:Location}
          {&_include:recurse=Location:managingOrganization}
          {&searchFilter={OrgTypeCodeSystem}|{OrgTypeCode}}
          {&searchFilter={OrgODSCodeSystem}|{OrgODSCode}}
```

#### FHIR absolute request ####

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]
          /Slot?[start={search_prefix}start_date]
          [&end=[{search_prefix}end_date]
          [&status=free]
          [&_include=Slot:schedule]
          {&_include:recurse=Schedule:actor:Practitioner}
          {&_include:recurse=Schedule:actor:Location}
          {&_include:recurse=Location:managingOrganization}
          {&searchFilter={OrgTypeCodeSystem}|{OrgTypeCode}}
          {&searchFilter={OrgODSCodeSystem}|{OrgODSCode}}
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (that is, GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot-1` |

#### Payload request body ####

N/A


#### Error handling ####

The provider system SHALL return an error if:

- the time period defined by `start` and `end` parameters is greater than a two week period
- the `status` parameter is absent or is present with a value other than `free`
- the `_include=Slot:schedule` is absent

SHALL return an [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more parameters are corrupt or a specific business rule/constraint is breached.

Refer to [Error handling guidance](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful retrieval of free slot details.

- SHALL return resources conforming to the GP Connect profiled versions of the base FHIR resources listed on the [Appointment Management resources](datalibraryappointment.html) page.

- SHALL return a `Bundle` of type `searchset` containing:

  - `Slot` resources for the organisation which:
    - have a `status` of `free`
    - **and** fall fully within the requested date range. That is, free slots which start before the `start` parameter and free slots which end after `end` search parameter SHALL NOT be returned.
    - **and** are bookable according to related defined 'Embargo/Booking Window' rules 
    - **and** which match the search filter parameters of Booking Organisation (ODS Code) and/or organisation type, or are not restricted for booking by ODS code and/or organisation type

  - `Schedule` resources associated with the returned `Slot` resources

  - `Practitioner` resources associated to the returned `Schedule` resources, where available, and where requested by the consumer using the `_include:recurse=Schedule:actor:Practitioner` parameter

    - SHALL populate the `Practitioner` resource according to population requirements for [Read a practitioner](foundations_use_case_read_a_practitioner.html#payload-response-body)

  - `Location` resources associated with the returned `Schedule` resources, where requested by the consumer using the `_include:recurse=Schedule:actor:Location` parameter

    - The `Location` referenced from the `Schedule` resource SHALL represent the location of the surgery where the appointment will take place.  `Location.managingOrganization` SHALL be populated.  See [Branch surgeries](development_branch_surgeries.html) for more details.

    - SHALL populate the `Location` resource according to population requirements for [Read a location](foundations_use_case_read_a_location.html#payload-response-body)

  - an `Organization` resource associated with the `Location` resources (via `Location.managingOrganization`) associated with the `Schedule`

    - This resource SHALL always be present, regardless of parameters, except where no slots are returned.  Please see [Known issues](appointments_known_issues.html) for more details.

    - Provider systems SHALL accept the `_include:recurse=Location:managingOrganization` parameter in the [Search for free slots](appointments_use_case_search_for_free_slots.html) request without returning an error, however SHALL continue to return the `Organization` resource regardless of whether this is present.

    - SHALL populate the `Organization` resource according to population requirements for [Read an organization](foundations_use_case_read_an_organisation.html#payload-response-body)

- If no free slots are returned for the requested time period then an empty response `Bundle` SHALL be returned.

- Only `Schedule`, `Practitioner`, `Location` and `Organization` resources SHALL be returned where they are are associated with the `Slot` resources matching the query

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields for `Schedule` and `Slot` where data is available, excluding those listed below

- SHALL NOT populate the `specialty` field on `Schedule` or `Slot`  

```json
{
  "resourceType": "Bundle",
  "type": "searchset",
  "entry": [
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
    {
      "resource": {
        "resourceType": "Slot",
        "id": "1644",
        "meta": {
          "versionId": "1471219260112",
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
        "start": "2016-08-15T12:00:00.000+01:00",
        "end": "2016-08-15T12:29:59.000+01:00"
      }
    },
    {
      "resource": {
        "resourceType": "Schedule",
        "id": "14",
        "meta": {
          "versionId": "1469444400000",
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Schedule-1"
          ]
        },
        "extension": [
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
          }
        ],
        "actor": [
          {
            "reference": "Location/17"
          },
          {
            "reference": "Practitioner/2"
          }
        ],
        "comment": "Schedule 1 for general appointments"
      }
    },
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
      "fullUrl": "https://gpconnect.aprovider.nhs.net/GP001/STU3/1/Location/17",
      "resource": {
        "resourceType": "Location",
        "id": "17",
        "meta": {
          "versionId": "636064088100870233",
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Location-1"
          ]
        },
        "name": "The Trevelyan Practice",
        "address": {
          "line": [
            "Trevelyan Square",
            "Boar Ln",
            "Leeds"
          ],
          "postalCode": "LS1 6AE"
        },
        "telecom": {
          "system": "phone",
          "value": "03003035678",
          "use": "work"
        },
        "managingOrganization": {
          "reference": "Organization/14"
        }
      }
    },
    {
      "fullUrl": "https://gpconnect.aprovider.nhs.net/GP001/STU3/1/Organization/23",
      "resource": {
        "resourceType": "Organization",
        "id": "23",
        "meta": {
          "versionId": "636064088098730113",
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"
          ]
        },
        "identifier": [
          {
            "system": "https://fhir.nhs.uk/Id/ods-organization-code",
            "value": "O001"
          }
        ],
        "name": "The Trevelyan Practice",
        "address": {
          "line": [
            "Trevelyan Square",
            "Boar Ln"
          ],
          "city": "Leeds",
          "district": "West Yorkshire",
          "postalCode": "LS1 6AE"
        },
        "telecom": {
          "system": "phone",
          "value": "03003035678",
          "use": "work"
        }
      }
    }
  ]
}
```

