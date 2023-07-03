---
title: Cross-organisation audit and provenance
keywords: spine, ssp, integration, audit, provenance
tags: [integration]
sidebar: overview_sidebar
permalink: integration_cross_organisation_audit_and_provenance.html
summary: "Overview of how audit and provenance data transported over GP Connect FHIR interfaces"
div: jwt-page
---

## Governance ##

Provider systems **SHALL** ensure that access to confidential data, including patient or clinical data, through the API must meet, as a minimum, the same requirements for information governance (IG), authentication and authorisation, and auditing as that of the host system the API exposes.

## Audit trail ##

{% include important.html content="As the GP Connect APIs are commissioned under the GPSoC framework, provider and consumer systems are expected to follow the standard 'IG Requirements for GP Systems V4' and 'GP Systems Interface Mechanism' requirements." %}

For implementers that don't have access to the GPSoC Framework / 'IG Requirements for GP Systems V4' requirements then the following extract of requirements covers the main audit trail requirements:

- provider systems **SHALL** record in an audit trail all access and data changes within the system as a result of API activity in the same way that internal access and changes are required to be recorded

- provider systems **SHALL** ensure that all API transactions are recorded in an audit trail and that audit trails must be subject to the standard IG audit requirements as defined in 'IG Requirements for GP Systems V4' or as subsequently amended

- provider systems **SHALL** ensure failed or rejected API transactions are recorded with the same detail as for successful API requests, with error codes as per the [error handling guidance](development_fhir_error_handling_guidance.html)

Audit trail records **SHALL** include the following minimum information:

- a record of the user identity - this is the User ID, Name, Role profile (including Role and Organisation, URP id when Smartcard authenticated) attribute values, obtained from the user’s session structure
- a record of the identity of the authority – the person authorising the entry of or access to data (if different from the user)
- the date and time on which the event occurred
- details of the nature of the audited event and the identity of the associated data (for example, patient ID, message ID) of the audited event
- a sequence number to protect against malicious attempts to subvert the audit trail by, for example, altering the system date
- audit trail records **SHOULD** include details of the end-user device (or system) involved in the recorded activity

Audit trails **SHALL** be enabled at all times and there shall be no means for users, or any other individuals, to disable any audit trail.

{% include note.html content="Whilst some details (such as name, role) associated with individual users are likely to change over time, the display of user information must reflect the state of such information as it was at the time of the associated event (such as data entry)." %}

## Provenance ##

Provider systems **SHALL** ensure that all additions, amendments or logical deletions to administrative and clinical data made via an API is clearly identified with information regarding the provenance of the data (such as timestamp, details of consumer system, details of user (including role)), so it is clear which information has been generated through an API rather than through the provider system itself.

Provider systems **SHALL** record the following provenance details of all API personal and sensitive personal data recorded within the system:

- author details (identified through unique ID), including name and role
- data entered by (if different from author)
- date and time (to the second) entered
- originating organisation
- API interaction

## Legal processing ##

Provider systems **SHALL** ensure that data provided to consumer systems only includes data for which the GP practice acts as data controller.

## Patient demographic cross-checking ##

Consumer systems **SHALL** always perform a patient demographic check as part of the use of a GP Connect capability to ensure that the patient for whom the information has been provided is the same patient for whom the request was made, and make clear to the end user any discrepancies.

## Cross-organisation audit and provenance transport ##

### Bearer token ###

Consumer systems **SHALL** provide audit and provenance details in the HTTP `Authorization` header as an OAuth Bearer Token (as outlined in [RFC 6749](https://tools.ietf.org/html/rfc6749) in the form of a JSON Web Token (JWT) as defined in [RFC 7519](https://tools.ietf.org/html/rfc7519).

An example such an HTTP header is given below:

```
     Authorization: Bearer jwt_token_string
```

Provider systems **SHALL** respond to OAuth Bearer Token errors in line with [RFC 6750 - section 3.1](https://tools.ietf.org/html/rfc6750#section-3.1).

It is highly recommended that standard libraries are used for creating the JWT as constructing and encoding the token manually may lead to issues with parsing the token. A good source of information about JWT and libraries to use can be found on the [JWT.io site](https://jwt.io/).

### JWT generation ###

Consumer system **SHALL** generate a new JWT for each API request. The consumer generated JWT **SHALL** consist of three [base64url encoded](https://tools.ietf.org/html/rfc4648#section-5) parts separated by dots `.`, which are:

- header
- payload
- signature

#### Header ####

Consumer systems **SHALL** generate an unsecured JWT using the 'none' algorithm parameter in the header to indicate that no digital signature or MAC has been performed (please refer to section 6 of [RFC 7519](https://tools.ietf.org/html/rfc7519){:target="_blank"}_ for details).

```json
{
  "alg": "none",
  "typ": "JWT"
}
```

#### Payload ####

Consumers systems **SHALL** generate a JWT payload conforming to the requirements set out in the [JWT Payload](#jwt-payload) section of this page.

#### Signature ####

Consumer systems **SHALL** generate an empty signature.

#### Complete JWT ####

The final output is three [base64url](https://tools.ietf.org/html/rfc4648#section-5) encoded strings separated by dots (note: there is some canonicalisation done to the JSON before it is base64url encoded, which the JWT code libraries will do for you).

```shell
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpc3MiOiJodHRwOi8vZWMyLTU0LTE5NC0xMDktMTg0LmV1LXdlc3QtMS5jb21wdXRlLmFtYXpvbmF3cy5jb20vIy9zZWFyY2giLCJzdWIiOiIxIiwiYXVkIjoiaHR0cHM6Ly9hdXRob3JpemUuZmhpci5uaHMubmV0L3Rva2VuIiwiZXhwIjoxNDgxMjUyMjc1LCJpYXQiOjE0ODA5NTIyNzUsInJlYXNvbl9mb3JfcmVxdWVzdCI6ImRpcmVjdGNhcmUiLCJyZXF1ZXN0ZWRfcmVjb3JkIjp7InJlc291cmNlVHlwZSI6IlBhdGllbnQiLCJpZGVudGlmaWVyIjpbeyJzeXN0ZW0iOiJodHRwOi8vZmhpci5uaHMubmV0L0lkL25ocy1udW1iZXIiLCJ2YWx1ZSI6IjkwMDAwMDAwMzMifV19LCJyZXF1ZXN0ZWRfc2NvcGUiOiJwYXRpZW50LyoucmVhZCIsInJlcXVlc3RpbmdfZGV2aWNlIjp7InJlc291cmNlVHlwZSI6IkRldmljZSIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6IldlYiBJbnRlcmZhY2UiLCJ2YWx1ZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn1dLCJtb2RlbCI6IkRlbW9uc3RyYXRvciIsInZlcnNpb24iOiIxLjAifSwicmVxdWVzdGluZ19vcmdhbml6YXRpb24iOnsicmVzb3VyY2VUeXBlIjoiT3JnYW5pemF0aW9uIiwiaWQiOiIxIiwiaWRlbnRpZmllciI6W3sic3lzdGVtIjoiaHR0cDovL2ZoaXIubmhzLm5ldC9JZC9vZHMtb3JnYW5pemF0aW9uLWNvZGUiLCJ2YWx1ZSI6IltPRFNDb2RlXSJ9XSwibmFtZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn0sInJlcXVlc3RpbmdfcHJhY3RpdGlvbmVyIjp7InJlc291cmNlVHlwZSI6IlByYWN0aXRpb25lciIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6Imh0dHA6Ly9maGlyLm5ocy5uZXQvc2RzLXVzZXItaWQiLCJ2YWx1ZSI6IkcxMzU3OTEzNSJ9LHsic3lzdGVtIjoibG9jYWxTeXN0ZW0iLCJ2YWx1ZSI6IjEifV0sIm5hbWUiOnsiZmFtaWx5IjpbIkRlbW9uc3RyYXRvciJdLCJnaXZlbiI6WyJHUENvbm5lY3QiXSwicHJlZml4IjpbIk1yIl19fX0.
```

**Note**: the final section (the signature) is empty, so the JWT will end with a trailing `.` (this must not be omitted, otherwise it would be an invalid token)

### JWT payload ###

Consumers **SHALL** populate the payload section of the JWT with the following claims:

- [`iss`](#iss-issuer-claim) (issuer)
- [`sub`](#sub-subject-claim) (subject)
- [`aud`](#aud-audience-claim) (audience)
- [`exp`](#exp-expiry-claim) (expiry)
- [`iat`](#iat-issued-at-claim) (issued at)
- [`reason_for_request`](#reason_for_request-claim)
- [`requested_scope`](#requested_scope-claim)
- [`requesting_device`](#requesting_device-claim)
- [`requesting_organization`](#requesting_organization-claim)
- [`requesting_practitioner`](#requesting_practitioner-claim)

Please see details below on how to populate each claim.

{% include important.html content="The JWT payload used in **GP Connect API 0.x (DSTU2)** is different to that displayed on this page.  Please ensure you consult the relevant specification from the [GP Connect specifications page](https://developer.nhs.uk/gp-connect-specification-versions/) when constructing the JWT for different GP Connect API major versions." %}

---

#### `iss` (issuer) claim

Consumer systems token issuer URI.

As the consuming system is presently responsible for generating the access token, this **SHALL** contain the URL of the Spine endpoint of the consumer system.

In future OAuth2 implementation, the `iss` claim will contain the URL of the OAuth2 authorisation server token endpoint.

**Example**: `"iss": "https://consumersupplier.thirdparty.nhs.uk/"`

---

#### `sub` (subject) claim

ID for the user on whose behalf this request is being made. Matches [`requesting_practitioner.id`](#requesting_practitioner-claim).

**Example**: `"sub": "10019"`

---

#### `aud` (audience) claim

The [service root URL](development_general_api_guidance.html#service-root-url) of the provider system.

This is the value returned from the [SDS endpoint lookup service](integration_spine_directory_service.html) in the `nhsMhsEndPoint` field.

**Example**: `"aud": "https://providersupplier.thirdparty.nhs.uk/GP0001/STU3/1"`

---

#### `exp` (expiry) claim

Identifies the expiration time in UTC on and after which the JWT **SHALL NOT** be accepted for processing.

The expiration time **SHALL** be set to 5 minutes after the token creation time (populated in the [`iat` claim](#iat-issued-at-claim)).

The value must be an integer representing seconds past 01 Jan 1970 00:00:00 UTC, i.e. [UNIX time](https://en.wikipedia.org/wiki/Unix_time).

Providers **SHALL** reject requests with expired tokens.

**Example**: `"exp": 1469436987`

{% include important.html content="To ensure accuracy of timestamps, and minimise the likelihood of tokens being rejected due to clock skew providers and consumers **SHALL** synchronise their server clocks with NHS Network Time Protocol (NTP) servers." %}

---

#### `iat` (issued at) claim

The time the request and token were generated in UTC.

The value **SHALL** be an integer representing seconds past 01 Jan 1970 00:00:00 UTC, i.e. [UNIX time](https://en.wikipedia.org/wiki/Unix_time).

**Example**: `"iat": 1469436687`

---

#### `reason_for_request` claim

The purpose for which access is being requested.

GP Connect supports two reasons for requesting the patient record:

- `directcare` where the record is being requested to support direct care
- `migration` where the record is being retrieved for the purpose of migration, for example, a GP2GP record transfer

**Example**: `"reason_for_request": "directcare"`

---

#### `requested_scope` claim

The scope of the request.

Please see the table below for which values to populate.

| Claim value            | Description                  | When to use                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| -----------            | -----------                  | -----------                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| `patient/*.read`       | Patient record read request  | - [Find a patient](foundations_use_case_find_a_patient.html)<br/> - [Read a patient](foundations_use_case_read_a_patient.html)<br/> - [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html)<br/> - [Read an appointment](appointments_use_case_read_an_appointment.html)<br/> - [Get patient's structured record](accessrecord_structured_development_retrieve_patient_record.html)<br/> - [Migrate patient's structured record](accessrecord_structured_development_migrate_patient_record.html)<br/> - [Find a patient (Access Document)](access_documents_use_case_find_a_patient.html)<br/> - [Search for a patient's documents](access_documents_development_search_patient_documents.html)<br/> - [Retrieve a patient's documents](access_documents_development_retrieve_patient_documents.html)<br/>
| `patient/*.write`      | Patient record write request | - [Register a patient](foundations_use_case_register_a_patient.html)<br/>- [Book an appointment](appointments_use_case_book_an_appointment.html)<br/>- [Amend an appointment](appointments_use_case_amend_an_appointment.html)<br/>- [Cancel an appointment](appointments_use_case_cancel_an_appointment.html)<br/>                                                                                                                                                                                                                                                                                                                                                                            |
| `organization/*.read`  | Other read request           | - [Get the capability statement](foundations_use_case_get_the_fhir_capability_statement.html)<br/>- [Find a practitioner](foundations_use_case_find_a_practitioner.html)<br/>- [Read practitioner](foundations_use_case_read_a_practitioner.html)<br/>- [Find an organisation](foundations_use_case_find_an_organisation.html)<br/>- [Read organisation](foundations_use_case_read_an_organisation.html)<br/>- [Read location](foundations_use_case_read_a_location.html)<br/>- [Search for free slots](appointments_use_case_search_for_free_slots.html)<br/>- [Get the capability statement (Access Record Structured)](accessrecord_structured_get_the_fhir_capability_statement.html)<br/> |
| `organization/*.write` | Other write request          | _(none currently)_                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

In addition to the above values, the table below contains claims around the sensitivity/confidentiality of the requested information.

| Claim value | Description                | When to use                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ----------- | -----------                | -----------                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| conf/N      | Normal confidentiality     | - [Get patient's structured record](accessrecord_structured_development_retrieve_patient_record.html)<br/> - [Migrate patient's structured record](accessrecord_structured_development_migrate_patient_record.html)<br/> - [Search for a patient's documents](access_documents_development_search_patient_documents.html)<br/> - [Retrieve a patient's documents](access_documents_development_retrieve_patient_documents.html)<br/>                                                                                                                                                                                                                                                                                                                  |
| conf/R      | Restricted confidentiality | Restricted confidentiality This MUST be only be used in a restricted set of use cases, this is currently restricted to GP2GP record transfers. In this scenario, provider systems will check whether the requesting organisation is permitted to retrieve sensitive information from the patient's record. <br/> - [Get patient's structured record](accessrecord_structured_development_retrieve_patient_record.html)<br/> - [Migrate patient's structured record](accessrecord_structured_development_migrate_patient_record.html)<br/> - [Search for a patient's documents](access_documents_development_search_patient_documents.html)<br/> - [Retrieve a patient's documents](access_documents_development_retrieve_patient_documents.html)<br/> |

Where multiple values are required, they **MUST** be provided as a space separated string. Where no confidentiality scope has been included, provider systems **MUST** interpret this as normal confidentiality, `conf/N`.

Providers should also read the associated [Security guidance](development_api_security_guidance.html#authorisation-of-access-to-endpoints) in relation to this claim.

**Example**: `"requested_scope": "patient/*.read conf/N"`

---

#### `requesting_device` claim

The system or device making the request, populated as a minimal [Device](https://www.hl7.org/fhir/STU3/device.html) resource.

The consumer **SHALL** populate the following [Device](https://www.hl7.org/fhir/STU3/device.html) fields:

- an `identifier` element, with:
  - `system` containing a consumer-defined system URL representing the type of identifier in the value field, e.g. `https://consumersupplier.com/Id/device-identifier`
  - `value` containing the device or system identifier
- `model` with the consumer product or system name
- `version` with the version number of the consumer product or system

The [Device](https://www.hl7.org/fhir/STU3/device.html) resource populated in this claim is a minimally populated resource to convey key details for audit, conforming to the base STU3 FHIR resources definition, and is not required to conform to a GP Connect FHIR resource profile.

**Example**:

<pre class="remove-highlight"><code class="no-highlight">"requesting_device": {
  "resourceType": "Device",
  "identifier": [
    {
      "system": "https://consumersupplier.com/Id/device-identifier",
      "value": "CONS-APP-4"
    }
  ],
  "model": "Consumer product name",
  "version": "5.3.0"
}
</code></pre>

---

#### `requesting_organization` claim

The consumer organisation making the request, populated as a minimal [Organization](https://www.hl7.org/fhir/STU3/organization.html) resource.

The consumer **SHALL** populate the following [Organization](https://www.hl7.org/fhir/STU3/organization.html) fields:

- `name` with the name of the organisation
- an `identifier` element, with:
  - `system` containing `https://fhir.nhs.uk/Id/ods-organization-code`, and
  - `value` containing the ODS code of the organisation

{% include important.html content="In consumer system topologies where GP Connect consumer applications are provisioned via a portal or middleware hosted by another organisation, it is vital for audit purposes that the organisation populated in the JWT reflects the organisation from where the request originates, rather than the hosting organisation.<br/>
This is normally determined as the organisation of the logged on user making the request." %}

The [Organization](https://www.hl7.org/fhir/STU3/organization.html) resource populated in this claim is a minimally populated resource to convey key details for audit, conforming to the base STU3 FHIR resources definition, and is not required to conform to a GP Connect FHIR resource profile.

**Example**:

<pre class="remove-highlight"><code class="no-highlight">"requesting_organization": {
  "resourceType": "Organization",
  "identifier": [
    {
      "system": "https://fhir.nhs.uk/Id/ods-organization-code",
      "value": "A1001"
    }
  ],
  "name": "Test Hospital"
}
</code></pre>

---

#### `requesting_practitioner` claim

The user making the request, populated as a minimal [Practitioner](https://www.hl7.org/fhir/STU3/practitioner.html) resource.

To contain the logged on user's identifier(s) (for example, login details / username). Where the user has both a local system user role as well as a nationally-recognised user role, then both **SHALL** be provided.

{% include important.html content="This field **SHALL NOT** be populated with fixed values or a generic \"system\" user. The values **SHALL** represent the logged on user making the request." %}

The consumer **SHALL** populate the following [Practitioner](https://www.hl7.org/fhir/STU3/practitioner.html) fields. The only exception to this is for the [Migrate patient's structured record](accessrecord_structured_development_migrate_patient_record.html) interaction where the fields **SHOULD** be populated:

- `id` with a unique [logical](https://www.hl7.org/fhir/STU3/resource.html#id) identifier (e.g. user ID or GUID) for the logged on user. This **SHALL** match the value of the [`sub` (subject) claim](integration_cross_organisation_audit_and_provenance.html#sub-subject-claim).
- `name` with:
  - `family` containing the user's family name
  - `given` containing the user's given name
  - `prefix` containing the user's title, where available
- an `identifier` element with:
  - `system` containing `https://fhir.nhs.uk/Id/sds-user-id`
  - `value` containing the SDS user ID from the user's NHS smartcard, or the value `UNK` if the user is not logged on with an NHS smartcard
- an `identifier` element with:
  - `system` containing `https://fhir.nhs.uk/Id/sds-role-profile-id`
  - `value` containing the SDS user role profile ID from the user's NHS smartcard, or the value `UNK` if the user is not logged on with an NHS smartcard
- an `identifier` element containing a unique local user or user-role identifier for the logged on user (e.g. user ID, user role ID, logon name) from the consumer system:
  - `system` containing a consumer-defined system URL representing the type of identifier in the value field, e.g. `https://consumersupplier.com/Id/user-guid`
  - `value` containing the unique local identifier for the logged on user

{% include important.html content="Providers should be aware of variance in the population of the `identifier` field amongst existing consumer systems when reading this claim, specifically the latter two elements (SDS role profile ID, and local user identifier) are not always present." %}

The [Practitioner](https://www.hl7.org/fhir/STU3/practitioner.html) resource populated in this claim is a minimally populated resource to convey key details for audit, conforming to the base STU3 FHIR resources definition, and is not required to conform to a GP Connect FHIR resource profile.

**Example**:

<pre class="remove-highlight"><code class="no-highlight">"requesting_practitioner": {
  "resourceType": "Practitioner",
  "id": "10019",
  "identifier": [
    {
      "system": "https://fhir.nhs.uk/Id/sds-user-id",
      "value": "111222333444"
    },
    {
      "system": "https://fhir.nhs.uk/Id/sds-role-profile-id",
      "value": "444555666777"
    },
    {
      "system": "https://consumersupplier.com/Id/user-guid",
      "value": "98ed4f78-814d-4266-8d5b-cde742f3093c"
    }
  ],
  "name": [
    {
      "family": "Jones",
      "given": [
        "Claire"
      ],
      "prefix": [
        "Dr"
      ]
    }
  ]
}</code></pre>

### JWT payload full example ###

```json
{
  "iss": "https://consumersupplier.thirdparty.nhs.uk/",
  "sub": "10019",
  "aud": "https://providersupplier.thirdparty.nhs.uk/GP0001/STU3/1",
  "exp": 1469436987,
  "iat": 1469436687,
  "reason_for_request": "directcare",
  "requested_scope": "patient/*.read",
  "requesting_device": {
    "resourceType": "Device",
    "identifier": [
      {
        "system": "https://consumersupplier.com/Id/device-identifier",
        "value": "CONS-APP-4"
      }
    ],
    "model": "Consumer product name",
    "version": "5.3.0"
  },
  "requesting_organization": {
    "resourceType": "Organization",
    "identifier": [
      {
        "system": "https://fhir.nhs.uk/Id/ods-organization-code",
        "value": "A1001"
      }
    ],
    "name": "Test Hospital"
  },
  "requesting_practitioner": {
    "resourceType": "Practitioner",
    "id": "10019",
    "identifier": [
      {
        "system": "https://fhir.nhs.uk/Id/sds-user-id",
        "value": "111222333444"
      },
      {
        "system": "https://fhir.nhs.uk/Id/sds-role-profile-id",
        "value": "444555666777"
      },
      {
        "system": "https://consumersupplier.com/Id/user-guid",
        "value": "98ed4f78-814d-4266-8d5b-cde742f3093c"
      }
    ],
    "name": [
      {
        "family": "Jones",
        "given": [
          "Claire"
        ],
        "prefix": [
          "Dr"
        ]
      }
    ]
  }
}
```

## External documents/policy documents ##

| Name | Author | Version | Updated |
| GPSoC IG Requirements for GP Systems | NHS Digital | v4.0 | 19/09/2014 |
| GP Systems Interface Mechanism Requirements V 1| NHS Digital | v0.10|
