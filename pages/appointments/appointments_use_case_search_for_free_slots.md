---
title: Search for free slots
keywords: appointments, use case, search, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_search_for_free_slots.html
summary: "Search for free slots within a date range at an organisation"
---

## Use case ##

This specification describes a single use case enabling the consumer application to request from the targeted provider system slots matching the selected date range, booking organisation Organisation Data Service (ODS) Code and Type, and other parameters including Urgent Care (UC) Disposition Code and Service ID. 

Refer to [Consumer sessions illustrated](appointments_consumer_sessions.html) for how this API use case could be used in the context of a typical consumer appointment management session.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Search parameters ##

Provider systems SHALL support the following search parameters:

| Name | Type | Description | Paths |
|---|---|---|---|
| `status` | `token` | The free/busy status of the appointment | `Slot.status` |
| `start` | `date` or `dateTime` | Slot start date, or date and time | `Slot.start` |
| `end` | `date` or `dateTime` | Slot end date, or date and time | `Slot.end` |
| `searchFilter` | `token` | A generic token to allow consumers to pass additional search criteria to the provider. | (n/a) |

{% include note.html content="The supported search parameters should be included in the [FHIR Capability Statement](foundations_use_case_get_the_fhir_capability_statement.html)." %}

## _include parameters ##

Provider systems SHALL support the following include parameters:

| Name | Description | Paths |
|---|---|---|
| `_include=Slot:schedule` | Include `Schedule` resources referenced within the returned `Slot` Resources | `Slot.schedule` |
| `_include:recurse= Schedule:actor:Practitioner` | Include `Practitioner` resources referenced within the returned `Schedule` resources | `Schedule.actor:Practitioner` |
| `_include:recurse= Schedule:actor:Location` | Include `Location` resources referenced within the returned `Schedule` resources | `Schedule.actor:Location` |
| `_include:recurse= Location:managingOrganization` | Include `Organization` resources references from matching `Location` resources | `Location.managingOrganization` |

Consumer applications SHALL send the following parameters in the request:

- The `start` parameter SHALL only be included once in the request.
- The `start` parameter SHALL be supplied with the `ge` search prefix. For example, `start=ge2017-09-22`, which indicates that the consumer would like slots where the slot start date is on or after "2017-09-22".
- The `end` parameter SHALL only be included once in the request.
- The `end` parameter SHALL be supplied with the `le` search prefix. For example, `end=le2017-09-26`, which indicates that the consumer would like slots where the slot end date is on or before "2017-09-26".
 
  ![Diagram - Date range parameters](images/appointments/SearchForFreeSlots.png)

- The `start` and `end` parameters SHALL contain a search prefix as specified above, and:
  - either, a `date` in the format `yyyy-mm-dd`. Partial dates are not allowed.
  - or, a `dateTime` in the format `yyyy-mm-ddThh:mm:ss+hh:mm` in (UK) local time, with the timezone offset `+00:00` for UTC and `+01:00` for BST.

- `status=free` specifies that only free slots will be returned. Note: the slot status value of `free` SHALL be specified, other slot status values are not permitted.

- `_include=Slot:schedule` specifies that associated `Schedule` resources are returned.

Consumer applications SHOULD send the following parameters in the request:

- `searchFilter` parameters - see [Enhanced slot filtering](#enhanced-slot-filtering).

Consumer applications MAY send the following *_include* parameters in the request, to minimise the number of API calls required to prepare an appointment booking:

- `_include:recurse=Schedule:actor:Practitioner`
- `_include:recurse=Schedule:actor:Location`
- `_include:recurse=Location:managingOrganization`

{% include note.html content="Search for free slots does not prevent searching for slots in the past, but all other appointment management capabilities do not allow for appointment management where the appointments start date element is in the past. Therefore, slots found in the past cannot be used to book an appointment." %}

### Enhanced slot filtering ###

{% include important.html content="It is recognized that provider systems must offer GP practices more functionality to enable them to better manage their available appointment slots in the light of increasing access requirements from other organisations. GP Connect has specified additional provider requirements to enable this. These additional requirements are outlined on the [Slot availability management](appointments_slotavailabilitymanagement.html) page" %}

In order for providers to return the appropriate slots for the consumer, the consumer SHOULD send in the following parameters using the `searchFilter` parameter using the [token](https://www.hl7.org/fhir/STU3/search.html#token) parameter format of `system|code`:

| Parameter name | Parameter value - system element | Parameter value - code element |
| --- | --- |
| `searchFilter` | `https://fhir.nhs.uk/Id/ods-organization-code` | Consumer ODS organisation code, e.g. `A11111`|
| `searchFilter` | `https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1` | Consumer organisation type code from [GPConnect-OrganisationType-1 valueset](https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1), e.g. `urgent-care` |

Where search filters are sent by consumer applications which are not explicitly supported in this specification (for example, urgent care use a disposition code value set), provider systems who do not understand the additional parameters SHALL ignore them and SHALL NOT return an error.

## Search for free slots on the wire ##

On the wire, a search for free slots request sending all parameters, and searching on date, would look something like the following:

```http
GET /Slot?status=free&start=ge2017-10-20&end=le2017-10-31&_include=Slot:schedule&_include:recurse=Schedule:actor:Practitioner&_include:recurse=Schedule:actor:Location&_include:recurse=Location:managingOrganization&searchFilter=https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1|gp-practice&searchFilter=https://fhir.nhs.uk/Id/ods-organization-code|A1001
```

A search for free slots request sending only mandatory and required parameters, and searching on date and time, would look something like the following:

```http
GET /Slot?status=free&start=ge2019-03-29T12:00:00+00:00&end=le2019-04-01T17:00:00+01:00&_include=Slot:schedule&searchFilter=https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1|gp-practice&searchFilter=https://fhir.nhs.uk/Id/ods-organization-code|A1001
```

## Booking multiple adjacent slots ##

Please see the conditions in which a consumer may book multiple adjacent slots on the [Book an appointment](appointments_use_case_book_an_appointment.html#booking-multiple-adjacent-slots) page.

## Consumer application display requirements ##

The fields below allow a patient to choose and attend an appointment appropriate to their needs.

In order to prevent incorrect or unsuitable bookings, and to allow a patient to attend the appointment at the correct time, place or via the correct delivery channel, consumer applications SHALL support the following fields: 

- Start date and time
- End date and time, or duration
- Delivery channel (in-person, telephone, video)
- Location name and address
- Practitioner role (e.g. General Medical Practitioner, Nurse)
- Practitioner name and gender

## Prerequisites ##

### Consumer ###

The consumer application:

- SHALL have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- SHALL request a maximum date range covering a two-week period

{% include tip.html content="Multiple separate API calls can be made if a larger date range is required. However, consideration should be given to the load this placed on the provider system." %}

## API usage ##

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

SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more parameters are corrupt or a specific business rule/constraint is breached.

Refer to [Error handling guidance](development_fhir_error_handling_guidance.html) for details of error codes.

### Request response ###

#### Response headers ####

Provider systems are not expected to add any specific headers beyond that described in the HTTP and FHIR&reg; standards.

#### Payload response body ####

Provider systems:

- SHALL return a `200` **OK** HTTP status code on successful retrieval of free slot details

- SHALL return resources conforming to the GP Connect profiled versions of the base FHIR resources listed on the [Appointment Management resources](datalibraryappointment.html) page

- SHALL return a `Bundle` of type `searchset` containing:

  - `Slot` resources for the organisation which:
    - have a `status` of `free`
    - **and** fall fully within the requested date range. That is, free slots which start before the `start` parameter and free slots which end after `end` search parameter SHALL NOT be returned.
    - **and** are bookable according to related defined [embargo/booking window](appointments_slotavailabilitymanagement.html#booking-windowembargo) rules 
    - **and** which match the search filter parameters of Booking Organisation (ODS Code) and/or organisation type, or are not restricted for booking by ODS code and/or organisation type

  - `Schedule` resources associated with the returned `Slot` resources

  - `Practitioner` resources associated to the returned `Schedule` resources, where available, and where requested by the consumer using the `_include:recurse=Schedule:actor:Practitioner` parameter

    - SHALL populate the `Practitioner` resource according to population requirements for [Read a practitioner](foundations_use_case_read_a_practitioner.html#payload-response-body)

  - `Location` resources associated with the returned `Schedule` resources, where requested by the consumer using the `_include:recurse=Schedule:actor:Location` parameter

    - The `Location` referenced from the `Schedule` resource SHALL represent the location of the surgery where the appointment will take place.  `Location.managingOrganization` SHALL be populated.  See [Branch surgeries](development_branch_surgeries.html) for more details.

    - SHALL populate the `Location` resource according to population requirements for [Read a location](foundations_use_case_read_a_location.html#payload-response-body)

  - an `Organization` resource associated with the `Location` resources (via `Location.managingOrganization`) associated with the `Schedule`

    - This resource SHALL always be present, regardless of parameters, except where no slots are returned.  Please see [Known issues](appointments_known_issues.html) for more details.

    - Provider systems SHALL accept the `_include:recurse=Location:managingOrganization` parameter in the [Search for free slots](appointments_use_case_search_for_free_slots.html) request without returning an error, however SHALL continue to return the `Organization` resource regardless of whether this is present

    - SHALL populate the `Organization` resource according to population requirements for [Read an organization](foundations_use_case_read_an_organisation.html#payload-response-body)

- If no free slots are returned for the requested time period then an empty response `Bundle` SHALL be returned

- Only `Schedule`, `Practitioner`, `Location` and `Organization` resources SHALL be returned where they are associated with the `Slot` resources matching the query

- SHALL populate `Slot.start`, `Slot.end`, `Schedule.planningHorizon.start` and `Schedule.planningHorizon.end` elements in (UK) local time in the format `yyyy-mm-ddThh:mm:ss+hh:mm`, with the timezone offset `+00:00` for UTC and `+01:00` for BST

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields for `Schedule` and `Slot` where data is available, excluding those listed below

- SHALL NOT populate the `specialty` field on `Schedule` or `Slot`  

```json
{% include appointments/search_for_free_slots_response_example.json %}
```
