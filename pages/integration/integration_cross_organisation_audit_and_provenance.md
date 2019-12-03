---
title: Cross organisation audit and provenance
keywords: spine, ssp, integration, audit, provenance
tags: [integration]
sidebar: overview_sidebar
permalink: integration_cross_organisation_audit_and_provenance.html
summary: "Overview of how audit and provenance data transported over GP Connect FHIR interfaces"
div: jwt-page
---

## Governance ##

Provider systems **MUST** ensure that access to confidential data, including patient or clinical data, through the API must meet, as a minimum, the same requirements for information governance (IG), authentication and authorisation, and auditing as that of the host system the API exposes.

## Audit trail ##

{% include important.html content="As the GP Connect APIs are commissioned under the GPSoC framework, Provider and Consumer systems are expected to follow the standard 'IG Requirements for GP Systems V4' and 'GP Systems Interface Mechanism' requirements." %}

For implementers that don't have access to the GPSoC Framework / 'IG Requirements for GP Systems V4' requirements then the following extract of requirements covers the main audit trail requirements:

- provider systems **MUST** record in an audit trail all access and data changes within the system as a result of API activity in the same way that internal access and changes are required to be recorded

- provider systems **MUST** ensure that all API transactions are recorded in an audit trail, and that audit trails must be subject to the standard IG audit requirements as defined in 'IG Requirements for GP Systems V4' or as subsequently amended

- provider systems **MUST** ensure failed or rejected API transactions are recorded with the same detail as for successful API requests, with error codes as per the [error handling guidance](development_fhir_error_handling_guidance.html)

Audit trail records **MUST** include the following minimum information:

- a record of the user identity - this is the User ID, Name, Role profile (including Role and Organisation, URP id when Smartcard authenticated) attribute values, obtained from the user’s Session structure
- a record of the identity of the authority – the person authorising the entry of or access to data (if different from the user)
- the date and time on which the event occurred
- details of the nature of the audited event and the identity of the associated data (for example patient ID, message ID) of the audited event
- a sequence number to protect against malicious attempts to subvert the audit trail by, for example, altering the system date
- audit trail records **SHOULD** include details of the end-user device (or system) involved in the recorded activity

Audit trails **MUST** be enabled at all times and therefore **MUST NOT** be means for users, or any other individuals, to disable any Audit Trail.

{% include note.html content="Whilst some details (such as name, role) associated with individual users are likely to change over time, the display of user information must reflect the state of such information as it was at the time of the associated event (such as data entry)." %}

## Provenance ##

Provider systems **MUST** ensure that all additions, amendments or logical deletions to administrative and clinical data made via an API is clearly identified with information regarding the provenance of the data (such as timestamp, details of consumer system, details of user (including role)), so it is clear which information has been generated through an API rather than through the provider system itself.

Provider systems **MUST** record the following provenance details of all API personal and sensitive personal data recorded within the system:

- author details (identified through unique ID), including name and role
- data entered by (if different from author)
- date and time (to the second) entered
- originating organisation
- API interaction

## Legal processing ##

Provider systems **MUST** ensure that data provided to consumer systems only includes data for which the GP practice acts as data controller.




## Patient demographic cross-checking ##

Consumer systems **MUST** always perform a patient demographic check as part of the use of a GP Connect capability to ensure that the patient for whom the information has been provided is the same patient for whom the request was made, and make clear to the end user any discrepancies. 

### Patient dissent ###

Provider systems **MUST** ensure that Patient Consent is respected (for example where express dissent is recorded then data is not shared).

## Cross organisation audit and provenance transport ##

### Bearer token ###

Consumer systems **MUST** provide audit and provenance details in the HTTP `Authorization` header as an OAuth Bearer Token (as outlined in [RFC 6749](https://tools.ietf.org/html/rfc6749) in the form of a JSON Web Token (JWT) as defined in [RFC 7519](https://tools.ietf.org/html/rfc7519).

An example such an HTTP header is given below:

```
     Authorization: Bearer jwt_token_string
```

Provider systems **MUST** respond to oAuth Bearer Token errors in line with [RFC 6750 - section 3.1](https://tools.ietf.org/html/rfc6750#section-3.1).
It is highly recommended that standard libraries are used for creating the JWT as constructing and encoding the token manually may lead to issues with parsing the token. A good source of information about JWT and libraries to use can be found on the [JWT.io site](https://jwt.io/).



  
### JWT generation ###
Consumer systems **MUST** generate the JSON Web Token (JWT) consisting of three parts separated by dots (.), which are:

- header
- payload
- signature


#### Header ####
Consumer systems **MUST** generate an unsecured JWT using the 'none' algorithm parameter in the header to indicate that no digital signature or MAC has been performed (please refer to section 6 of [RFC 7519](https://tools.ietf.org/html/rfc7519){:target="_blank"}_ for details).

```json
{
  "alg": "none",
  "typ": "JWT"
}
```

#### Payload ####

Consumers systems **MUST** generate a JWT payload conforming to the requirements set out in the [JWT Payload](#jwt-payload) section of this page.

#### Signature ####

Consumer systems **MUST** generate an empty signature.

#### Complete JWT ####

The final output is three [base64url](https://tools.ietf.org/html/rfc4648#section-5) encoded strings separated by dots (note: there is some canonicalisation done to the JSON before it is base64url encoded, which the JWT code libraries will do for you).

```shell
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpc3MiOiJodHRwOi8vZWMyLTU0LTE5NC0xMDktMTg0LmV1LXdlc3QtMS5jb21wdXRlLmFtYXpvbmF3cy5jb20vIy9zZWFyY2giLCJzdWIiOiIxIiwiYXVkIjoiaHR0cHM6Ly9hdXRob3JpemUuZmhpci5uaHMubmV0L3Rva2VuIiwiZXhwIjoxNDgxMjUyMjc1LCJpYXQiOjE0ODA5NTIyNzUsInJlYXNvbl9mb3JfcmVxdWVzdCI6ImRpcmVjdGNhcmUiLCJyZXF1ZXN0ZWRfcmVjb3JkIjp7InJlc291cmNlVHlwZSI6IlBhdGllbnQiLCJpZGVudGlmaWVyIjpbeyJzeXN0ZW0iOiJodHRwOi8vZmhpci5uaHMubmV0L0lkL25ocy1udW1iZXIiLCJ2YWx1ZSI6IjkwMDAwMDAwMzMifV19LCJyZXF1ZXN0ZWRfc2NvcGUiOiJwYXRpZW50LyoucmVhZCIsInJlcXVlc3RpbmdfZGV2aWNlIjp7InJlc291cmNlVHlwZSI6IkRldmljZSIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6IldlYiBJbnRlcmZhY2UiLCJ2YWx1ZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn1dLCJtb2RlbCI6IkRlbW9uc3RyYXRvciIsInZlcnNpb24iOiIxLjAifSwicmVxdWVzdGluZ19vcmdhbml6YXRpb24iOnsicmVzb3VyY2VUeXBlIjoiT3JnYW5pemF0aW9uIiwiaWQiOiIxIiwiaWRlbnRpZmllciI6W3sic3lzdGVtIjoiaHR0cDovL2ZoaXIubmhzLm5ldC9JZC9vZHMtb3JnYW5pemF0aW9uLWNvZGUiLCJ2YWx1ZSI6IltPRFNDb2RlXSJ9XSwibmFtZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn0sInJlcXVlc3RpbmdfcHJhY3RpdGlvbmVyIjp7InJlc291cmNlVHlwZSI6IlByYWN0aXRpb25lciIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6Imh0dHA6Ly9maGlyLm5ocy5uZXQvc2RzLXVzZXItaWQiLCJ2YWx1ZSI6IkcxMzU3OTEzNSJ9LHsic3lzdGVtIjoibG9jYWxTeXN0ZW0iLCJ2YWx1ZSI6IjEifV0sIm5hbWUiOnsiZmFtaWx5IjpbIkRlbW9uc3RyYXRvciJdLCJnaXZlbiI6WyJHUENvbm5lY3QiXSwicHJlZml4IjpbIk1yIl19fX0.
```

**Note**: the final section (the signature) is empty, so the JWT will end with a trailing `.` (this must not be omitted, otherwise it would be an invalid token)



### JWT payload ###

Consumers **MUST** populate the payload section of the JWT with the following claims:

- [`iss`](#iss-issuer-claim) (issuer)
- [`sub`](#sub-subject-claim) (subject)
- [`aud`](#aud-audience-claim) (audience)
- [`exp`](#exp-expiry-claim) (expiry)
- [`iat`](#iat-issued-at-claim) (issued at)
- [`reason_for_request`](#reason_for_request-claim)
- [`requested_record`](#requested_record)
- [`requested_scope`](#requested_scope-claim)
- [`requesting_device`](#requesting_device-claim)
- [`requesting_organization`](#requesting_organization-claim)
- [`requesting_practitioner`](#requesting_practitioner-claim)

Please see details below on how to populate each claim.

{% include important.html content="The JWT payload used in **GP Connect API 0.x (DSTU2)** is different to that used in **GP Connect API 1.x (STU3)**.  Please ensure you consult the relevant specification from the [GP Connect specifications page](https://developer.nhs.uk/gp-connect-specification-versions/) when constructing the JWT for different GP Connect API major versions." %}

---

#### `iss` (issuer) claim

Consumer systems token issuer URI.

As the consuming system is presently responsible for generating the access token, this **MUST** contain the URL of the Spine endpoint of the consumer system.

In future OAuth2 implementation, the `iss` claim will contain the URL of the OAuth2 authorisation server token endpoint.

**Example**: `"iss": "https://consumersupplier.thirdparty.nhs.uk/"`

---

#### `sub` (subject) claim

ID for the user on whose behalf this request is being made. Matches [`requesting_practitioner.id`](#requesting_practitioner-claim).

**Example**: `"sub": "10019"`

---

#### `aud` (audience) claim

The Authorization server’s token URL.

The value **MUST** be fixed to `https://authorize.fhir.nhs.net/token`

**Example**: `"aud": "https://authorize.fhir.nhs.net/token"`

---

#### `exp` (expiry) claim

Identifies the expiration time in UTC on and after which the JWT **MUST NOT** be accepted for processing.

The expiration time **MUST** be set to 5 minutes after the token creation time (populated in the [`iat` claim](#iat-issued-at-claim)).

The value must be an integer representing seconds past 01 Jan 1970 00:00:00 UTC, i.e. [UNIX time](https://en.wikipedia.org/wiki/Unix_time).

Providers **MUST** reject requests with expired tokens.

**Example**: `"exp": 1469436987`

{% include important.html content="To ensure accuracy of timestamps, and minimise the likelihood of tokens being rejected due to clock skew providers and consumers **MUST** synchronise their server clocks with NHS Network Time Protocol (NTP) servers." %}

---

#### `iat` (issued at) claim

The time the request and token were generated in UTC.

The value **MUST** be an integer representing seconds past 01 Jan 1970 00:00:00 UTC, i.e. [UNIX time](https://en.wikipedia.org/wiki/Unix_time).

**Example**: `"iat": 1469436687`

---

#### `reason_for_request` claim

The purpose for which access is being requested.

As GP Connect only supports usage for direct care, this value **MUST** be set to `directcare`.

**Example**: `"reason_for_request": "directcare"`

---

#### `requested_record` claim

The identifier of the record being requested. 

The request can be made using the FHIR Patient or FHIR Organization resource.

**Patient example**:

<pre class="remove-highlight"><code class="no-highlight">"requesting_record": {
  "resourceType": "Patient",
  "identifier": [
    {
      "system": "http://fhir.nhs.net/Id/nhs-number",
      "value": "9658218873"
    }
  ]
}
</code></pre>

**Organization example**:

<pre class="remove-highlight"><code class="no-highlight">"requesting_record": {
  "resourceType": "Organization",
  "identifier": [
    {
      "system": "http://fhir.nhs.net/Id/ods-organization-code",
      "value": "A1001"
    }
  ]
}
</code></pre>


#### `requested_scope` claim

The scope of the request.

Please the table below for which values to populate.

| Claim value | Description | When to use |
|-------|-------------|------|
| `patient/*.read` | Patient record read request | - [Get patient's record](accessrecord_use_case_retrieve_a_care_record_section.html)<br/>  |
| `organization/*.read` | Other read request | - [Get the conformance profile](foundations_use_case_get_the_fhir_conformance_profile.html)<br/> |

Providers should also read the associated [Security guidance](development_api_security_guidance.html#authorisation-of-access-to-endpoints) in relation to this claim.

**Example**: `"requested_scope": "patient/*.read"`

---

#### `requesting_device` claim

The system or device making the request, populated as a minimal [Device](https://www.hl7.org/fhir/DSTU2/device.html) resource.

The consumer **MUST** populate the following [Device](https://www.hl7.org/fhir/DSTU2/device.html) fields:

- an `id` with a unique [logical](https://www.hl7.org/fhir/DSTU2/resource.html#id) identifier
- an `identifier` element, with:
  - `system` containing a consumer-defined system URL representing the type of identifier in the value field, for example `http://consumersupplier.com/Id/device-identifier`
  - `value` containing the device or system identifier
- `model` with the consumer product or system name
- `version` with the version number of the consumer product or system

The [Device](https://www.hl7.org/fhir/DSTU2/device.html) resource populated in this claim is a minimally populated resource to convey key details for audit, conforming to the base DSTU2 FHIR resources definition, and is not required to conform to a GP Connect FHIR resource profile.

**Example**:

<pre class="remove-highlight"><code class="no-highlight">"requesting_device": {
  "resourceType": "Device",
  "id": "c4c8d038-913a-490c-9682-47047f4155fb",
  "identifier": [
    {
      "system": "http://consumersupplier.com/Id/device-identifier",
      "value": "CONS-APP-4"
    }
  ],
  "model": "Consumer product name",
  "version": "5.3.0"
}
</code></pre>

---

#### `requesting_organization` claim

The consumer organisation making the request, populated as a minimal [Organization](https://www.hl7.org/fhir/DSTU2/organization.html) resource.

The consumer **MUST** populate the following [Organization](https://www.hl7.org/fhir/DSTU2/organization.html) fields:

- `name` with the name of the organisation
- an `id` with a unique [logical](https://www.hl7.org/fhir/DSTU2/resource.html#id) identifier
- an `identifier` element, with:
  - `system` containing `http://fhir.nhs.net/Id/ods-organization-code`, and
  - `value` containing the ODS code of the organisation

{% include important.html content="In consumer system topologies where GP Connect consumer applications are provisioned via a portal or middleware hosted by another organisation, it is vital for audit purposes that the organisation populated in the JWT reflects **the true originating organisation of the request** rather than the hosting organisation.<br/>
This is normally determined as the organisation of the logged on user making the request." %}

The [Organization](https://www.hl7.org/fhir/DSTU2/organization.html) resource populated in this claim is a minimally populated resource to convey key details for audit, conforming to the base DSTU2 FHIR resources definition, and is not required to conform to a GP Connect FHIR resource profile.

**Example**:

<pre class="remove-highlight"><code class="no-highlight">"requesting_organization": {
  "resourceType": "Organization",
  "id": "79600119-ebaf-4362-bb89-d473a33b1675",
  "identifier": [
    {
      "system": "http://fhir.nhs.net/Id/ods-organization-code",
      "value": "A1001"
    }
  ],
  "name": "Test Hospital"
}
</code></pre>

---

#### `requesting_practitioner` claim

The user making the request, populated as a minimal [Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html) resource.

To contain the practitioner's local system identifier(s) (for example login details / username). Where the user has both a local system user role as well as a nationally-recognised user role, then both **MUST** be provided.

{% include important.html content="This field **MUST NOT** be populated with fixed values or a generic \"system\" user. The values **MUST** represent the logged on user making the request." %}

The consumer **MUST** populate the following [Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html) fields:

- `id` with a unique [logical](https://www.hl7.org/fhir/DSTU2/resource.html#id) identifier (for example user ID or GUID) for the logged on user. This **MUST** match the value of the [`sub` (subject) claim](integration_cross_organisation_audit_and_provenance.html#sub-subject-claim).
- `name` with:
  - `family` containing the user's family name
  - `given` containing the user's given name
  - `prefix` containing the user's title, where available
- an `identifier` element with:
  - `system` containing `http://fhir.nhs.net/sds-user-id`
  - `value` containing the SDS user ID from the user's NHS smartcard, or the value `UNK` if the user is not logged with an NHS smartcard
- an `identifier` element containing a unique local user or user-role identifier for the logged on user (for example, user ID, user role ID, logon name) from the consumer system:
  - `system` containing a consumer-defined system URL representing the type of identifier in the value field, for example `http://consumersupplier.com/Id/user-guid`
  - `value` containing the unique local identifier for the logged on user
- `practitionerRole` with:
  - `system` containing `http://fhir.nhs.net/ValueSet/sds-job-role-name-1`
  - `value` containing the SDS Job Role ID from the user's NHS smartcard, or the value `UNK` if the user is not logged with an NHS smartcard

{% include important.html content= "the `Practitioner` resource **MUST** contain an identifier with the system `http://fhir.nhs.net/sds-user-id` rather than the system required by the resource profile `http://fhir.nhs.net/Id/sds-user-id`. This is required as there was an error during testing and assurance which resulted in the providers validating that the identifier in the resource has the incorrect value, so for consumers to make a successful call the incorrect system value needs to be included." %}

<div class="alert alert-warning" role="alert"><em class="fa fa-warning"></em> <strong>Important:</strong> Providers should be aware of variance in the population of certain fields amongst existing consumer systems when reading this claim, specifically, the following are not always present: <ul><li> local user <code class="highlighter-rouge">identifier</code> </li><li> the <code class="highlighter-rouge">practitionerRole</code> </li></ul></div>
 
The [Practitioner](https://www.hl7.org/fhir/DSTU2/practitioner.html) resource populated in this claim is a minimally populated resource to convey key details for audit, conforming to the base DSTU2 FHIR resources definition, and is not required to conform to a GP Connect FHIR resource profile.

**Example**:

<pre class="remove-highlight"><code class="no-highlight">"requesting_practitioner": {
  "resourceType": "Practitioner",
  "id": "f7737bf5-cfe7-491c-af3a-6f7177d5aee1",
  "identifier": [
    {
      "system": "http://fhir.nhs.net/sds-user-id",
      "value": "111222333444"
    },
    {
      "system": "http://consumersupplier.com/Id/user-guid",
      "value": "54b9d987-c2f1-4fdd-a449-e67cdf41dd2b"
    }
  ],
  "name": {
    "family": [
      "Jones"
    ],
    "given": [
      "Claire"
    ],
    "prefix": [
      "Dr"
    ]
  },
  "practitionerRole": [
    {
      "role": {
        "coding": [
          {
            "system": "http://fhir.nhs.net/ValueSet/sds-job-role-name-1",
            "code": "R8000"
          }
        ]
      }
    }
  ]
}
</code></pre>




## JWT payload example ##

```json
{
  "iss": "http://consumersupplier.thirdparty.nhs.uk/",
  "sub": "10019",
  "aud": "https://authorize.fhir.nhs.net/token",
  "exp": 1469436987,
  "iat": 1469436687,
  "reason_for_request": "directcare",
  "requested_scope": "patient/*.read",
  "requested_record": {
    "resourceType": "Patient",
    "identifier": [
      {
        "system": "http://fhir.nhs.net/Id/nhs-number",
        "value": "9658218873"
      }
    ]
  },
  "requesting_device": {
    "resourceType": "Device",
    "id": "c4c8d038-913a-490c-9682-47047f4155fb",
    "identifier": [
      {
        "system": "http://consumersupplier.com/Id/device-identifier",
        "value": "CONS-APP-4"
      }
    ],
    "model": "Consumer product name",
    "version": "5.3.0"
  },
  "requesting_organization": {
    "resourceType": "Organization",
    "id": "79600119-ebaf-4362-bb89-d473a33b1675",
    "identifier": [
      {
        "system": "http://fhir.nhs.net/Id/ods-organization-code",
        "value": "A1001"
      }
    ],
    "name": "Test Hospital"
  },
  "requesting_practitioner": {
    "resourceType": "Practitioner",
    "id": "f7737bf5-cfe7-491c-af3a-6f7177d5aee1",
    "identifier": [
      {
        "system": "http://fhir.nhs.net/sds-user-id",
        "value": "111222333444"
      },
      {
        "system": "http://consumersupplier.com/Id/user-guid",
        "value": "54b9d987-c2f1-4fdd-a449-e67cdf41dd2b"
      }
    ],
    "name": {
      "family": [
	      "Jones"
	    ],
      "given": [
        "Claire"
      ],
      "prefix": [
        "Dr"
      ]
    },
  "practitionerRole": [
    {
      "role": {
        "coding": [
          {
            "system": "http://fhir.nhs.net/ValueSet/sds-job-role-name-1",
            "code": "R8000"
          }
        ]
      }
    }
  ]
}
```

## External documents / policy documents ##

| Name | Author | Version | Updated |
| GPSoC IG Requirements for GP Systems | NHS Digital | v4.0 | 19/09/2014 |
| GP Systems Interface Mechanism Requirements V 1| NHS Digital | v0.10|
