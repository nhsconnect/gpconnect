---
title: Search for free slots
keywords: appointments, use case, search, free, slots, schedule
tags: [appointments,use_case]
sidebar: appointments_sidebar
permalink: appointments_use_case_search_for_free_slots.html
summary: "Search for free slots within a date range at an organisation"
---

## Use case ##

This specification describes a single use case enabling the consumer to search for free appointment slots from the  provider system, matching the selected date range, booking organisation ODS code and booking organisation type, and optionally other parameters including service ID.

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
| `searchFilter` | `token` | A generic token to allow consumers to pass additional search criteria to the provider. | *(n/a)* |
| `service.identifier` | `token` | HealthcareService identifier of the schedule of the slots being requested<br/>See [GPConnect-Slot-ServiceIdentifier-1 SearchParameter definition](https://fhir.nhs.uk/STU3/SearchParameter/GPConnect-Slot-ServiceIdentifier-1) | `Slot.schedule.actor: HealthcareService.identifier` |

## _include parameters ##

Provider systems SHALL support the following include parameters:

| Name | Description | Paths |
|---|---|---|
| `_include=Slot:schedule` | Include `Schedule` resources referenced within the returned `Slot` Resources | `Slot.schedule` |
| `_include:recurse= Schedule:actor:Practitioner` | Include `Practitioner` resources referenced within the returned `Schedule` resources | `Schedule.actor:Practitioner` |
| `_include:recurse= Schedule:actor:Location` | Include `Location` resources referenced within the returned `Schedule` resources | `Schedule.actor:Location` |
| `_include:recurse= Schedule:actor:HealthcareService` | Include `HealthcareService` resources referenced within the returned `Schedule` resources | `Schedule.actor:Location` |
| `_include:recurse= Location:managingOrganization` | Include `Organization` resources references from matching `Location` resources | `Location.managingOrganization` |

Consumer systems SHALL send the following parameters in the request:

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

Where a Consumer system has used [Directory of Services (DOS) to locate a service to book at](appointments_service_discovery.html#directory-of-services-dos---currently-for-uec-consumers-only), the consumer system SHALL send the following parameter in the request:

- The `service.identifier` parameter with the service ID of the chosen DOS service, e.g. `service.identifier=https://fhir.nhs.uk/Id/uec-dos-service-id|1000123`  (see [Service filtering](appointments_service_filtering.html) for more information)

Consumer systems SHOULD send the following parameters in the request:

- `searchFilter` parameters - see [Enhanced slot filtering](#enhanced-slot-filtering).

Consumer systems MAY send the following *_include* parameters in the request, to minimise the number of API calls required to prepare an appointment booking:

- `_include:recurse=Schedule:actor:Practitioner`
- `_include:recurse=Schedule:actor:Location`
- `_include:recurse=Schedule:actor:HealthcareService`
- `_include:recurse=Location:managingOrganization`

{% include note.html content="Search for free slots does not prevent searching for slots in the past, but all other appointment management capabilities do not allow for appointment management where the appointments start date element is in the past. Therefore, slots found in the past cannot be used to book an appointment." %}

### Enhanced slot filtering ###

{% include important.html content="It is recognized that provider systems must offer GP practices more functionality to enable them to better manage their available appointment slots in the light of increasing access requirements from other organisations. GP Connect has specified additional provider requirements to enable this. These additional requirements are outlined on the [Slot availability management](appointments_slotavailabilitymanagement.html) page" %}

In order for providers to return the appropriate slots for the consumer, the consumer SHOULD send in the following parameters using the `searchFilter` parameter using the [token](https://www.hl7.org/fhir/STU3/search.html#token) parameter format of `system|code`:

| Parameter name | Parameter value - system element | Parameter value - code element |
| --- | --- |
| `searchFilter` | `https://fhir.nhs.uk/Id/ods-organization-code` | Consumer ODS organisation code, e.g. `A11111`|
| `searchFilter` | `https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1` | Consumer organisation type code from [GPConnect-OrganisationType-1 valueset](https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-OrganisationType-1), e.g. `urgent-care` |

Where search filters are sent by consumers which are not explicitly supported in this specification (for example, urgent care use a disposition code value set), providers who do not understand the additional parameters SHALL ignore them and SHALL NOT return an error.

## Booking multiple adjacent slots ##

Please see the conditions in which a consumer may book multiple adjacent slots on the [Book an appointment](appointments_use_case_book_an_appointment.html#booking-multiple-adjacent-slots) page.

## Consumer display requirements ##

The fields below allow a patient to choose and attend an appointment appropriate to their needs.

In order to prevent incorrect or unsuitable bookings, and to allow a patient to attend the appointment at the correct time, place or via the correct delivery channel, consumer systems SHALL support the following fields: 

- Start date and time
- End date and time, or duration
- Delivery channel (in-person, telephone, video)
- Slot type and schedule type (see `Slot.serviceType` and `Schedule.serviceCategory`)
- Service name (where present, see [service filtering](appointments_service_filtering.html) for more information)
- Location name and address
- Practitioner role (e.g. General Medical Practitioner, Nurse)
- Practitioner name and gender

{% include note.html content="*Start date and time*, *End date and time or duration*, *Delivery channel*, *Slot type* are part of or derived from the `Slot` resource.  The remaining fields are part of or derived from the `Schedule` resource, or resources referenced by it." %}

## Prerequisites ##

### Consumer ###

The consumer system:

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
          {&_include:recurse=Schedule:actor:HealthcareService}
          {&_include:recurse=Location:managingOrganization}
          {&searchFilter={OrgTypeCodeSystem}|{OrgTypeCode}}
          {&searchFilter={OrgODSCodeSystem}|{OrgODSCode}}
          {&service.identifier={ServiceIDCodeSystem|ServiceID}}
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
          {&_include:recurse=Schedule:actor:HealthcareService}
          {&_include:recurse=Location:managingOrganization}
          {&searchFilter={OrgTypeCodeSystem}|{OrgTypeCode}}
          {&searchFilter={OrgODSCodeSystem}|{OrgODSCode}}
          {&service.identifier={ServiceIDCodeSystem|ServiceID}}
```

#### Request headers ####

Consumers SHALL include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's trace ID (that is, GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:rest:search:slot-1` |

#### Payload request body ####

No payload is sent in the request.

### Request response ###

#### FHIR resource relationships ####

This diagram shows the relationships between FHIR resources in the search for free slots response message.

![Diagram - Slot resource relationship structure](images/appointments/appointment-fhir-resources-slot.png)

{% include important.html content="A Schedule may not have Practitioner or HealthcareService references present in the actor element, and therefore the Practitioner and HealthcareService resources may not be returned in the response Bundle, regardless of the _include parameters sent." %}

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
    - **and** which match the search filter parameters of booking organisation (ODS code) and/or organisation type, or are not restricted for booking by ODS code and/or organisation type
    - **and** reference a `Schedule` with a `actor` of type `HealthcareService`, **where**:
      - the consumer has sent a `service.identifier` search parameter in the request
      - **and** the service filtering [organisation switch is ON](appointments_service_configuration.html#organisation-switch-set-to-on)
      - **and** a `HealthcareService.identifier` element matches the token passed in the `service` parameter

      {% include important.html content="The `service.identifier` and the HealthcareService `_include` parameters do not take effect (i.e. are ignored) if the provider organisation has the service filtering [organisation switch set to OFF](appointments_service_configuration.html#organisation-switch-set-to-off)" %}

  - `Schedule` resources associated with the returned `Slot` resources

  - `Practitioner` resources associated to the returned `Schedule` resources, where available, and where requested by the consumer using the `_include:recurse=Schedule:actor:Practitioner` parameter

    - SHALL populate the `Practitioner` resource according to population requirements for [Read a practitioner](foundations_use_case_read_a_practitioner.html#payload-response-body)

  - `Location` resources associated with the returned `Schedule` resources, where requested by the consumer using the `_include:recurse=Schedule:actor:Location` parameter

    - The `Location` referenced from the `Schedule` resource SHALL represent the location of the surgery where the appointment will take place.  `Location.managingOrganization` SHALL be populated.  See [Branch surgeries](development_branch_surgeries.html) for more details.

    - SHALL populate the `Location` resource according to population requirements for [Read a location](foundations_use_case_read_a_location.html#payload-response-body)

  - `HealthcareService` resources associated with the returned `Schedule` resources where requested by the consumer using the `_include:recurse=Schedule:actor:HealthcareService` parameter and where the service filtering [organisation switch is ON](appointments_service_configuration.html#organisation-switch-set-to-on)

    - `HealthcareService` resources and their reference in `Schedule.actor` SHALL NOT be populated when the service filtering [organisation switch is OFF](appointments_service_configuration.html#organisation-switch-set-to-off) regardless of the parameters sent by the consumer

    - SHALL populate the `HealthcareService` resource according to population requirements for [Read a healthcare service](foundations_use_case_read_a_healthcareservice.html#payload-response-body)


  - an `Organization` resource associated with the `Location` resources (via `Location.managingOrganization`) associated with the `Schedule`

    - This resource SHALL always be present, regardless of parameters, except where no slots are returned.  Please see [Known issues](appointments_known_issues.html) for more details.

    - Provider systems SHALL accept the `_include:recurse=Location:managingOrganization` parameter in the [Search for free slots](appointments_use_case_search_for_free_slots.html) request without returning an error, however SHALL continue to return the `Organization` resource regardless of whether this is present

    - SHALL populate the `Organization` resource according to population requirements for [Read an organization](foundations_use_case_read_an_organisation.html#payload-response-body)

- If no free slots are returned for the requested time period then an empty response `Bundle` SHALL be returned

- Only `Schedule`, `Practitioner`, `Location`, `HealthcareService` and `Organization` resources SHALL be returned where they are associated with the `Slot` resources matching the query

- SHALL populate `Slot.start`, `Slot.end`, `Schedule.planningHorizon.start` and `Schedule.planningHorizon.end` elements in (UK) local time in the format `yyyy-mm-ddThh:mm:ss+hh:mm`, with the timezone offset `+00:00` for UTC and `+01:00` for BST

- SHALL populate `Slot.serviceType.text` with a practice defined slot type description, and where available `Schedule.serviceCategory.text` with a practice defined schedule type description (may be called session name or rota type).  The slot and schedule description fields SHOULD be the same as those visible in the NHS App.

- SHALL meet [General FHIR resource population requirements](development_fhir_resource_guidance.html#general-fhir-resource-population-requirements) populating all fields for `Schedule` and `Slot` where data is available, excluding those listed below

- SHALL NOT populate the `specialty` field on `Schedule` or `Slot`  

- SHALL indicate the service filtering status of the search:
  - only when the consumer sends the `service.identifier` parameter in the request
  - by using the [Extension-GPConnect-ServiceFilteringStatus-1](https://fhir.nhs.uk/STU3/Extension/Extension-GPConnect-ServiceFilteringStatus-1) extension populating the valueCode element with [GPConnect-ServiceFilteringStatus-1]((https://fhir.nhs.uk/STU3/CodeSystem/GPConnect-ServiceFilteringStatus-1))
  - matching the `supplier-disabled`, `organization-disabled`, `enabled` values with the current state of the supplier switch and organisation switch 

### Error handling ####

The provider system:

- SHALL return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource that provides additional detail when one or more parameters are corrupt or a specific business rule/constraint is breached

- SHALL return an error if:
  - the time period defined by `start` and `end` parameters is greater than a two week period
  - the `status` parameter is absent or is present with a value other than `free`
  - the `_include=Slot:schedule` parameter is absent

- SHALL return a [RECORD_NOT_FOUND](development_fhir_error_handling_guidance.html#example-resource-not-found) error with the diagnostics element providing detail of the issue when:
  - the consumer system has populated the `service.identifier` parameter in the request
  - *AND* the provider organisation has the [service filtering switch set to ON](appointments_service_configuration.html#organisation-switch-set-to-on)
  - *AND* the DOS service ID in the `service.identifier` parameter value is not contained in the provider organisation's [service list](appointments_service_configuration.html#service-list)

Refer to [Error handling guidance](development_fhir_error_handling_guidance.html) for details of error codes.


## Examples ##

### Example - Searching without a DOS service ID ###

#### Request ####

The example below shows a typical search for free slots request from a consumer system that has used [PDS or local configuration](appointments_service_discovery.html) to determine a provider organisation to book at - they *have not* used [Directory of Services (DOS)](appointments_service_discovery.html#directory-of-services-dos---currently-for-uec-consumers-only) to locate a service, and therefore do not have a DOS service ID to search on.

The consumer system is:
  
- sending all search parameters
  - except for service.identifier (a DOS service ID is required to send this)
- and searching on date

```http
{% include appointments/search-for-free-slots-request-header-1.txt %}
```
{% include note.html content="Please note: Newlines and spacing have been added for readability in the example above, these are not included in an actual request." %}

#### Response ####

The example response includes two Slot resources matching the search criteria, and associated Schedule, Location, Practitioner, HealthcareService and Organization resources.

Because the consumer has not sent the service.identifier parameter, the response has not been filtered by service - schedules linked to any service, or not linked to a service at all, could be returned.

In this example the schedule matching the search criteria has been linked to a service by the provider organisation (and they have switched on the service filtering feature) so the service has been returned in the Bundle as a HealthcareService resource.  Please see the examples further down this page for a response where a HealthcareService resource is not returned.

```json
{% include appointments/search-for-free-slots-response-payload-1.json %}
```

### Example - Searching with a DOS service ID ###

##### Request #####

The example below shows a typical search for free slots request from a consumer system that has used Directory of Services (DOS) to [locate a service](appointments_service_discovery.md) to book at (e.g. a 111 system), and therefore has a DOS service ID to search on:

- sending all request parameters
  - including service.identifier (using the service ID taken from DOS)
- and searching on date

```http
{% include appointments/search-for-free-slots-request-header-2.txt %}
```

{% include note.html content="Please note: Newlines and spacing have been added for readability in the example above, these are not included in an actual request." %}

#### Response ####

The example response includes two Slot resources matching the search criteria, and associated Schedule, Location, Practitioner and Organization resources.

The consumer has searched with a service ID from DOS, however in this example the provider organisation has not enabled [service filtering](appointments_service_filtering.html) and has therefore ignored the service.identifier parameter sent in the request.  Because the consumer sent the service.identifier parameter in the request, the `Bundle.extension` element is populated to indicate whether the service filtering is enabled and therefore whether the parameter was applied.

```json
{% include appointments/search-for-free-slots-response-payload-2.json %}
```

### Example - Sending the minimum parameters ###

#### Request ####

The example below shows a typical search for free slots request:

- from a consumer system that has *NOT* used Directory of Services (DOS) to [locate a service](appointments_service_discovery.md) to book at
- sending mandatory and required parameters only
- and searching on date and time

```http
{% include appointments/search-for-free-slots-request-header-3.txt %}
```

{% include note.html content="Please note: Newlines and spacing have been added for readability in the example above, these are not included in an actual request." %}

#### Response ####

The example response includes two Slot resources matching the search criteria, and associated Schedule and Organization resources.

In this example the provider organisation has not enabled [service filtering](appointments_service_filtering.html).  This can be seen in the example response below as the Schedule resource is not linked to a HealthcareService resource, and there are no HealthcareService resources in the response Bundle. Please see the example above for a response where a HealthcareService resource is returned.

This example also shows the absence of a Practitioner resource.  This may happen where a provider organisation has not yet assigned a named practitioner to an appointment schedule.

Please note:  the Organization resource is returned in this Bundle despite the Organization _include parameter not being sent (this is a [Known issue](appointments_known_issues.html#organization-resource-in-search-for-free-slots-returned-bundle)).

```json
{% include appointments/search-for-free-slots-response-payload-3.json %}
```

### Example - No slots returned ###

#### Request ####

The example below shows a typical search for free slots request:

- from a consumer system that has *NOT* used Directory of Services (DOS) to [locate a service](appointments_service_discovery.md) to book at
- sending all request parameters
  - except for service.identifier (a DOS service ID is required to send this)
- and searching on date

```http
{% include appointments/search-for-free-slots-request-header-4.txt %}
```

{% include note.html content="Please note: Newlines and spacing have been added for readability in the example above, these are not included in an actual request." %}

#### Response ####

The example response shows an empty Bundle as no slots were found matching the search criteria.

```json
{% include appointments/search-for-free-slots-response-payload-4.json %}
```
