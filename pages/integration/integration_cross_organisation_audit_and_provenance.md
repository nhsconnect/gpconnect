---
title: Cross organisation audit and provenance
keywords: spine, ssp, integration, audit, provenance
tags: [integration]
sidebar: overview_sidebar
permalink: integration_cross_organisation_audit_and_provenance.html
summary: "Overview of how audit and provenance data is expected to be transported over the GP Connect FHIR interfaces."
---

## Cross organisation audit and provenance ##

### Governance ###

Provider systems **MUST** ensure that access to confidential data, including patient or clinical data, through the API must meet, as a minimum, the same requirements for information governance, authentication and authorisation, and auditing as that of the host system the API exposes.

### Audit trail ###

{% include important.html content="As the GP Connect APIs are commissioned under the GPSoC framework, Provider and Consumer systems are expected to follow the standard 'IG Requirements for GP Systems V4' and 'GP Systems Interface Mechanism' requirements." %}

For implementers that don't have access to the GP SoC Framework / 'IG Requirements for GP Systems V4' requirements then the following extract of requirements covers the main audit trail requirements:

Provider systems **MUST** record in an audit trail all access and data changes within the system as a result of API activity in the same way that internal access and changes are required to be recorded.

Provider systems **MUST** ensure that all API transactions are recorded in an audit trail, and that audit trails must be subject to the standard IG audit requirements as defined in “IG Requirements for GP Systems V4” or as subsequently amended.

Provider systems **MUST** ensure failed or rejected API transactions are recorded with the same detail as for successful API requests, with error codes as per the [error handling guidance](development_fhir_error_handling_guidance.html).

Audit trail records **MUST** include the following minimum information:

- a record of the user identity. This is the User ID, Name, Role profile (including Role and Organisation, URP id when Smartcard authenticated) attribute values, obtained from the user’s Session structure
- a record of the identify of the authority – the person authorising the entry of, or access to data (if different from the user)
- the date and time on which the event occurred
- details of the nature of the audited event and the identity of the associated data (e.g. patient ID, message ID) of the audited event;
- a sequence number to protect against malicious attempts to subvert the audit trail by, for example, altering the system date
- audit trail records should include details of the end-user device (or system) involved in the recorded activity

Audit trails **MUST** be enabled at all times and there **MUST NOT** be means for users, or any other individuals, to disable any Audit Trail.

{% include note.html content="Whilst some details (such as name, role) associated with individual users are likely to change over time, the display of user information must reflect the state of such information as it was at the time of the associated event (such as data entry)." %}

### Provenance ###

Provider systems **MUST** ensure that all additions, amendments or logical deletions to administrative and clinical data made via an API is clearly identified with information regarding the provenance of the data (e.g. timestamp, details of Consumer system, details of user (including role), so it is clear which information has been generated through an API rather than through the Provider system itself.

Provider systems **MUST** record the following provenance details of all API personal and sensitive personal data recorded within the system:

- author details (identified through unique ID), including name and role
- data entered by (if different from author)
- date & time (to the second) entered
- originating organisation
- API interaction

### Legal processing ###

Provider systems **MUST** ensure that data provided to Consumer systems only include data for which the GP practice acts as Data Controller.

### Patient dissent ###

Provider systems **MUST** ensure that Patient Consent is respected (i.e. where express dissent is recorded then data is not shared).

## Cross organisation audit and provenance transport ##

### Bearer token ###

Consumer systems **MUST** provide audit and provenance details in the HTTP authorization header as an oAuth Bearer Token (as outlined in [RFC 6749](https://tools.ietf.org/html/rfc6749){:target="_blank"}) in the form of a JSON Web Token (JWT) as defined in [RFC 7519](https://tools.ietf.org/html/rfc7519){:target="_blank"}.

An example such an HTTP header is given below:

```
     Authorization: Bearer jwt_token_string
```

Provider systems **MUST** respond to oAuth Bearer Token errors inline with [RFC 6750 - section 3.1](https://tools.ietf.org/html/rfc6750#section-3.1).

### JSON Web Tokens (JWT) ###

- Consumer system **MUST** generate a new JWT for each API request containing the claims outlined in the table below
- Where the claim contains a FHIR resource the FHIR resource should conform to the GP Connect FHIR resource profiles outlined on the [FHIR Resources](datalibraryaccessRecord.html) page
  - An exeption to this requirement is that in the `requesting_practitioner` claim the `Practitioner` resource should contain an identifier with the system `"http://fhir.nhs.net/sds-user-id` rather than the system required by the resource profile `http://fhir.nhs.net/Id/sds-user-id`. This is required as there was a error during testing and assurance which resulted in the providers validate that the identifier in the resource has the incorrect value, so for consumers to make a successful call the incorrect system value needs to be included.

| Claim | Priority | Description | Fixed Value | Dynamic Value |
|-------|----------|-------------|-------------|------------------|
| iss | R | Requesting systems issuer URI | No | Yes |
| sub | R | ID for the user on whose behalf this request is being made. Matches `requesting_practitioner.id` | No | Yes |
| aud | R | Authorization server's `token_URL` | `https://authorize.fhir.nhs.net/token` | No |
| exp | R | Expiration time integer after which this authorization MUST be considered invalid. | `exp` | (now + 5 minutes) UTC time in seconds |
| iat | R | The UTC time the JWT was created by the requesting system | `iat` | now UTC time in seconds |
| reason_for_request | R | Purpose for which access is being requested | `directcare` | No |
| requested_record | R | The FHIR patient resource being requested (i.e. NHS Number identifier details) | No | FHIR Patient<sup>1</sup> <br/>OR <br/>FHIR Organization<sup>2</sup> |
| requested_scope | R | Data being requested<sup>2</sup> | `patient/*.[read|write]` <br/>OR <br/>`organization/*.[read|write]` | No |
| requesting_device | R | FHIR device resource making the request | No | FHIR Device<sup>1</sup> |
| requesting_organization | R | FHIR organisation resource making the request | No | FHIR Organization<sup>1+4</sup> | 
| requesting_practitioner | R | FHIR practitioner resource making the request | No | FHIR Practitioner<sup>1+3</sup> |

<sup>1</sup> Minimal FHIR resource to include any relevant business identifier(s).

<sup>2</sup> Patient scope for patient centric APIs (i.e. Get Care Record and Patient's Appointments, Patient Task) or scope for organisation centric APIs (i.e. Get Organization Schedule)

<sup>3</sup> To contain the practitioners local system identifier(s) (i.e. login details / username). Where the user has both a local system 'role' as well as a nationally-recognised role, then the latter **MUST** be provided. Default usernames (e.g. referring to systems or groups) **MUST NOT** be used in this field.

<sup>4</sup> The requesting organisation resource **MUST** refer to the care organisation from where the request originates rather than any other organisation which may host hardware or software, route requests to Spine, and/or hold the endpoint registration. 

{% include important.html content="In topologies where GP Connect consumer applications are provisioned via a portal or middleware hosted by another organisation (see [Topologies](integration_system_topologies.html)) it is important for audit purposes that the practitioner and organisation populated in the JWT reflect the originating organisation rather than the hosting organisation." %}

#### JWT generation ####
Consumer systems **MUST** generate the JSON Web Token (JWT) consisting of three parts separated by dots (.), which are:

- header
- payload
- signature

Consumer systems **MUST** generate an Unsecured JSON Web Token (JWT) using the "none" algorithm parameter in the header to indicate that no digital signature or MAC has been performed (please refer to section 3.6 of RFC 7513 for details).

```json
{
  "alg": "none",
  "typ": "JWT"
}
```

Consumer systems **MUST** generate an empty signature.

The final output is three base64url encoded strings separated by dots.

For example:

```shell
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpc3MiOiJodHRwOi8vZWMyLTU0LTE5NC0xMDktMTg0LmV1LXdlc3QtMS5jb21wdXRlLmFtYXpvbmF3cy5jb20vIy9zZWFyY2giLCJzdWIiOiIxIiwiYXVkIjoiaHR0cHM6Ly9hdXRob3JpemUuZmhpci5uaHMubmV0L3Rva2VuIiwiZXhwIjoxNDgxMjUyMjc1LCJpYXQiOjE0ODA5NTIyNzUsInJlYXNvbl9mb3JfcmVxdWVzdCI6ImRpcmVjdGNhcmUiLCJyZXF1ZXN0ZWRfcmVjb3JkIjp7InJlc291cmNlVHlwZSI6IlBhdGllbnQiLCJpZGVudGlmaWVyIjpbeyJzeXN0ZW0iOiJodHRwOi8vZmhpci5uaHMubmV0L0lkL25ocy1udW1iZXIiLCJ2YWx1ZSI6IjkwMDAwMDAwMzMifV19LCJyZXF1ZXN0ZWRfc2NvcGUiOiJwYXRpZW50LyoucmVhZCIsInJlcXVlc3RpbmdfZGV2aWNlIjp7InJlc291cmNlVHlwZSI6IkRldmljZSIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6IldlYiBJbnRlcmZhY2UiLCJ2YWx1ZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn1dLCJtb2RlbCI6IkRlbW9uc3RyYXRvciIsInZlcnNpb24iOiIxLjAifSwicmVxdWVzdGluZ19vcmdhbml6YXRpb24iOnsicmVzb3VyY2VUeXBlIjoiT3JnYW5pemF0aW9uIiwiaWQiOiIxIiwiaWRlbnRpZmllciI6W3sic3lzdGVtIjoiaHR0cDovL2ZoaXIubmhzLm5ldC9JZC9vZHMtb3JnYW5pemF0aW9uLWNvZGUiLCJ2YWx1ZSI6IltPRFNDb2RlXSJ9XSwibmFtZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn0sInJlcXVlc3RpbmdfcHJhY3RpdGlvbmVyIjp7InJlc291cmNlVHlwZSI6IlByYWN0aXRpb25lciIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6Imh0dHA6Ly9maGlyLm5ocy5uZXQvc2RzLXVzZXItaWQiLCJ2YWx1ZSI6IkcxMzU3OTEzNSJ9LHsic3lzdGVtIjoibG9jYWxTeXN0ZW0iLCJ2YWx1ZSI6IjEifV0sIm5hbWUiOnsiZmFtaWx5IjpbIkRlbW9uc3RyYXRvciJdLCJnaXZlbiI6WyJHUENvbm5lY3QiXSwicHJlZml4IjpbIk1yIl19fX0.
```

{% include tip.html content="The [JWT.io](https://jwt.io/) website includes a number of rich resources to aid in developing JWT enabled applications." %}

## JWT payload example ##

```json
{
	"iss": "https://[ConsumerSystemURL]",
	"sub": "[PractitionerID]",
	"aud": "https://authorize.fhir.nhs.net/token",
	"exp": 1469436987,
	"iat": 1469436687,
	"reason_for_request": "directcare",
	"requested_record": {
		"resourceType": "Patient",
		"identifier": [{
			"system": "http://fhir.nhs.net/Id/nhs-number",
			"value": "[NHSNumber]"
		}]
	},
	"requesting_device": {
		"resourceType": "Device",
		"id": "[DeviceID]",
		"identifier": [{
			"system": "[DeviceSystem]",
			"value": "[DeviceID]"
		}],
		"model": "[SoftwareName]",
		"version": "[SoftwareVersion]"
	},
	"requesting_organization": {
		"resourceType": "Organization",
		"id": "[OrganizationID]",
		"identifier": [{
			"system": "http://fhir.nhs.net/Id/ods-organization-code",
			"value": "[ODSCode]"
		}],
		"name": "Requesting Organisation Name"
	},
	"requesting_practitioner": {
		"resourceType": "Practitioner",
		"id": "[PractitionerID]",
		"identifier": [{
			"system": "http://fhir.nhs.net/sds-user-id",
			"value": "[SDSUserID]"
		},
		{
			"system": "[UserSystem]",
			"value": "[UserID]"
		}],
		"name": {
			"family": ["[Family]"],
			"given": ["[Given]"],
			"prefix": ["[Prefix]"]
		},
		"practitionerRole": [{
			"role": {
				"coding": [{
					"system": "http://fhir.nhs.net/ValueSet/sds-job-role-name-1",
					"code": "[SDSJobRoleName]"
				}]
			}
		}]
	}
}
```

{% include important.html content="Whilst the use of a JWT and the claims naming is inspired by the [SMART on FHIR](https://github.com/smart-on-fhir/smart-on-fhir.github.io/wiki/cross-organizational-auth) the GP Connect programme hasn't committed to using the SMART on FHIR specification." %}

Where the Practitioner has both a local system role as well as a Spine RBAC role, then the Spine RBAC role **MUST** be supplied

### Example code ###

#### C# ####

{% include tip.html content="The following code snippet utilise the [Microsoft Identity Model JWT Token Nuget Package](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/) for creating, serializing and validating JWT tokens." %}

{% gist michaelmeasures/d6a75e52acdbee93c4c30d23e639fb1a %}

## External documents/policy documents ##

| Name | Author | Version | Updated |
| GPSoC IG Requirements for GP Systems | NHS Digital | v4.0 | 19/09/2014 |
| GP Systems Interface Mechanism Requirements V 1| NHS Digital | v0.10|
