---
title: Cross organisation audit and provenance
keywords: spine, ssp, integration, audit, provenance
tags: [integration]
sidebar: overview_sidebar
permalink: integration_cross_organisation_audit_and_provenance.html
summary: "Overview of how audit and provenance data transported over GP Connect FHIR interfaces."
---

## Governance ##

Provider systems SHALL ensure that access to confidential data, including patient or clinical data, through the API must meet, as a minimum, the same requirements for information governance (IG), authentication and authorisation, and auditing as that of the host system the API exposes.

## Audit trail ##

{% include important.html content="As the GP Connect APIs are commissioned under the GPSoC framework, provider and consumer systems are expected to follow the standard 'IG Requirements for GP Systems V4' and 'GP Systems Interface Mechanism' requirements." %}

For implementers that don't have access to the GPSoC Framework / 'IG Requirements for GP Systems V4' requirements then the following extract of requirements covers the main audit trail requirements:

- provider systems SHALL record in an audit trail all access and data changes within the system as a result of API activity in the same way that internal access and changes are required to be recorded

- provider systems SHALL ensure that all API transactions are recorded in an audit trail and that audit trails must be subject to the standard IG audit requirements as defined in 'IG Requirements for GP Systems V4' or as subsequently amended

- provider systems SHALL ensure failed or rejected API transactions are recorded with the same detail as for successful API requests, with error codes as per the [error handling guidance](development_fhir_error_handling_guidance.html)

Audit trail records shall include the following minimum information:

- a record of the user identity - this is the User ID, Name, Role profile (including Role and Organisation, URP id when Smartcard authenticated) attribute values, obtained from the user’s session structure
- a record of the identity of the authority – the person authorising the entry of or access to data (if different from the user)
- the date and time on which the event occurred
- details of the nature of the audited event and the identity of the associated data (for example, patient ID, message ID) of the audited event
- a sequence number to protect against malicious attempts to subvert the audit trail by, for example, altering the system date
- audit trail records should include details of the end-user device (or system) involved in the recorded activity

Audit trails shall be enabled at all times and there shall be no means for users, or any other individuals, to disable any audit trail.

{% include note.html content="Whilst some details (such as name, role) associated with individual users are likely to change over time, the display of user information must reflect the state of such information as it was at the time of the associated event (such as data entry)." %}

## Provenance ##

Provider systems SHALL ensure that all additions, amendments or logical deletions to administrative and clinical data made via an API is clearly identified with information regarding the provenance of the data (such as, timestamp, details of consumer system, details of user (including role)), so it is clear which information has been generated through an API rather than through the provider system itself.

Provider systems SHALL record the following provenance details of all API personal and sensitive personal data recorded within the system:

- author details (identified through unique ID), including name and role
- data entered by (if different from author)
- date and time (to the second) entered
- originating organisation
- API interaction

## Legal processing ##

Provider systems SHALL ensure that data provided to consumer systems only includes data for which the GP practice acts as data controller.


## Patient demographic cross-checking ##

Consumer systems SHALL always perform a patient demographic check as part of the use of a GP Connect capability to ensure that the patient for whom the information has been provided is the same patient for whom the request was made, and make clear to the end user any discrepancies. 

## Cross organisation audit and provenance transport ##

### Bearer token ###

Consumer systems SHALL provide audit and provenance details in the HTTP authorisation header as an oAuth Bearer Token (as outlined in [RFC 6749](https://tools.ietf.org/html/rfc6749){:target="_blank"}) in the form of a JSON Web Token (JWT) as defined in [RFC 7519](https://tools.ietf.org/html/rfc7519){:target="_blank"}.

An example such an HTTP header is given below:

```
     Authorization: Bearer jwt_token_string
```

Provider systems SHALL respond to oAuth Bearer Token errors inline with [RFC 6750 - section 3.1](https://tools.ietf.org/html/rfc6750#section-3.1).

It is highly recommended that standard libraries are used for creating the JWT as constructing and encoding the token manually may lead to issues with parsing the token. A good source of information about JWT and libraries to use can be found on the [JWT.io site](https://jwt.io/).


### JWT generation ###

Consumer system SHALL generate a new JWT for each API request. The consumer generated JWT SHALL consist of three parts separated by dots `.`, which are:

- header
- payload
- signature

#### Header ####
Consumer systems SHALL generate an unsecured JWT using the 'none' algorithm parameter in the header to indicate that no digital signature or MAC has been performed (please refer to section 6 of [RFC 7519](https://tools.ietf.org/html/rfc7519){:target="_blank"} for details).

```json
{
  "alg": "none",
  "typ": "JWT"
}
```

#### Payload ####

Consumers systems SHALL generate a JWT payload conforming to the requirements set out in the [JWT Payload](#jwt-payload) section of this page.

#### Signature ####

Consumer systems SHALL generate an empty signature.

#### Complete JWT ####

The final output is three Base64url encoded strings separated by dots (note - there is some canonicalisation done to the JSON before it is Base64url encoded, which the JWT code libraries will do for you).

```shell
eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJpc3MiOiJodHRwOi8vZWMyLTU0LTE5NC0xMDktMTg0LmV1LXdlc3QtMS5jb21wdXRlLmFtYXpvbmF3cy5jb20vIy9zZWFyY2giLCJzdWIiOiIxIiwiYXVkIjoiaHR0cHM6Ly9hdXRob3JpemUuZmhpci5uaHMubmV0L3Rva2VuIiwiZXhwIjoxNDgxMjUyMjc1LCJpYXQiOjE0ODA5NTIyNzUsInJlYXNvbl9mb3JfcmVxdWVzdCI6ImRpcmVjdGNhcmUiLCJyZXF1ZXN0ZWRfcmVjb3JkIjp7InJlc291cmNlVHlwZSI6IlBhdGllbnQiLCJpZGVudGlmaWVyIjpbeyJzeXN0ZW0iOiJodHRwOi8vZmhpci5uaHMubmV0L0lkL25ocy1udW1iZXIiLCJ2YWx1ZSI6IjkwMDAwMDAwMzMifV19LCJyZXF1ZXN0ZWRfc2NvcGUiOiJwYXRpZW50LyoucmVhZCIsInJlcXVlc3RpbmdfZGV2aWNlIjp7InJlc291cmNlVHlwZSI6IkRldmljZSIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6IldlYiBJbnRlcmZhY2UiLCJ2YWx1ZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn1dLCJtb2RlbCI6IkRlbW9uc3RyYXRvciIsInZlcnNpb24iOiIxLjAifSwicmVxdWVzdGluZ19vcmdhbml6YXRpb24iOnsicmVzb3VyY2VUeXBlIjoiT3JnYW5pemF0aW9uIiwiaWQiOiIxIiwiaWRlbnRpZmllciI6W3sic3lzdGVtIjoiaHR0cDovL2ZoaXIubmhzLm5ldC9JZC9vZHMtb3JnYW5pemF0aW9uLWNvZGUiLCJ2YWx1ZSI6IltPRFNDb2RlXSJ9XSwibmFtZSI6IkdQIENvbm5lY3QgRGVtb25zdHJhdG9yIn0sInJlcXVlc3RpbmdfcHJhY3RpdGlvbmVyIjp7InJlc291cmNlVHlwZSI6IlByYWN0aXRpb25lciIsImlkIjoiMSIsImlkZW50aWZpZXIiOlt7InN5c3RlbSI6Imh0dHA6Ly9maGlyLm5ocy5uZXQvc2RzLXVzZXItaWQiLCJ2YWx1ZSI6IkcxMzU3OTEzNSJ9LHsic3lzdGVtIjoibG9jYWxTeXN0ZW0iLCJ2YWx1ZSI6IjEifV0sIm5hbWUiOnsiZmFtaWx5IjpbIkRlbW9uc3RyYXRvciJdLCJnaXZlbiI6WyJHUENvbm5lY3QiXSwicHJlZml4IjpbIk1yIl19fX0.
```

**Note:**

- the final section (the signature) is empty, so the JWT will end with a trailing `.` (this must not be omitted, otherwise it would be an invalid token)


### JWT payload ###

The payload section of the JWT shall be populated as follows:

| Claim | Priority | Description | Fixed Value | Dynamic Value |
|-------|----------|-------------|-------------|------------------|
| iss | R | Requesting systems issuer URI | No | Yes |
| sub | R | ID for the user on whose behalf this request is being made. Matches `requesting_practitioner.id` | No | Yes |
| aud | R | Requested resource URI<sup>1</sup> | No | Yes |
| exp | R | Expiration time integer after which this authorisation MUST be considered invalid. | No | (now + 5 minutes) UTC time in seconds |
| iat | R | The UTC time the JWT was created by the requesting system | No | now UTC time in seconds |
| reason_for_request | R | Purpose for which access is being requested | `directcare` | No |
| requested_record | R | A minimal FHIR resource which describes the resource being requested or searched for. | No | FHIR Patient<sup>2</sup> <br/>OR <br/>FHIR Organization<sup>2</sup> |
| requested_scope | R | Data being requested | `patient/*.[read|write]` <br/>OR <br/>`organization/*.[read|write]` | No |
| requesting_device | R | Device details and/or system url making the request | No | FHIR Device<sup>2</sup> |
| requesting_organization | R | FHIR organisation resource making the request | No | FHIR Organization<sup>2+3</sup> | 
| requesting_practitioner | R | FHIR practitioner resource making the request | No | FHIR Practitioner<sup>2+4</sup> |

<sup>1</sup> The URI for the requested resource, including the fully qualified endpoint address returned to the consumer by the [SDS endpoint lookup service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html#worked-example-of-the-endpoint-lookup-process){:target="_blank"} as the value of `nhsMhsEndPoint`.

<sup>2</sup> Minimal FHIR resource to include any relevant business identifier(s), conforming to the base STU3 FHIR resources definition (the resource does not need to conform to the GP Connect FHIR resource profile).

<sup>3</sup> The `requesting_organization` **SHALL** refer to the care organisation from where the request originates.

<sup>4</sup> To contain the practitioner's local system identifier(s) (for example, login details / username). Where the user has both a local system 'role' as well as a nationally-recognised role, then the latter SHALL be provided. Default usernames (for example, referring to systems or groups) SHALL NOT be used in this field.

{% include important.html content="In topologies where GP Connect consumer applications are provisioned via a portal or middleware hosted by another organisation (see [Topologies](integration_system_topologies.html)), it is important for audit purposes that the practitioner and organisation populated in the JWT reflect the originating organisation rather than the hosting organisation." %}

#### Population of requesting_organization ####

The `consumer` SHALL populate the `requesting_organization` claim with:

* A FHIR [Organization](https://www.hl7.org/fhir/STU3/organization.html) resource representing the organisation making the request and SHALL include the elements:

  | Element | Description |
  | --- | --- |
  | name | A textual representation of the name of the organisation. |
  | identifier | An identifier should be included contain a fixed `system` of `"https://fhir.nhs.uk/Id/ods-organization-code"` and a identifier `value` containing the ODS code of requesting organization. |


#### Population of requested_record ####

The `consumer` SHALL populate the `requested_record` claim with:

* Either a FHIR [Organization](https://www.hl7.org/fhir/STU3/organization.html) resource or a FHIR [Patient](https://www.hl7.org/fhir/STU3/patient.html) resource which describes the resource being requested or searched for, where possible, and will contain any relevant business identifiers for the request.

  The table below shows the GP Connect API calls and the expected content for the JWT requested_record claim:

  | Request | Known Business Identifiers | requested_record Resource Type | requested_record Content |
  | --- | --- | --- | --- |
  | Access Record HTML | NHS Number | Patient | SHALL contain an identifier element containing the NHS number being passed as a parameter to the `gpc.getcarerecord` operation. |
  | Find a patient | NHS Number | Patient | SHALL contain an identifier element containing the NHS Number being passed as the search parameter of the request. |
  | Register a patient | NHS Number | Patient | SHALL contain an identifier element containing the NHS Number of the patient to be registered. |
  | Read a patient | N/A | Patient | SHOULD contain the logical id of the patient resource being requested. |
  | Find an organisation | ODS Code | Organisation | SHALL contain an identifier element containing the organisation ODS Code which is being passed as the parameter to the search. |
  | Read an organisation | ODS Code | Organisation | SHOULD contain the logical id of the organization resource being requested. |
  | Find a practitioner | N/A | Organisation | SHOULD contain any relevant identifier for the organisation on which the FHIR endpoint resides. |
  | Read a practitioner | N/A | Organisation | SHOULD contain any relevant identifier for the organisation on which the FHIR endpoint resides. |
  | Read a location | N/A | Organisation | SHOULD contain any relevant identifier for the organisation on which the FHIR endpoint resides. |
  | Search for free slots | N/A | Organisation | SHOULD contain any relevant identifier for the organisation on which the FHIR endpoint resides. |
  | Book Appointment | NHS Number | Patient | The consumer will have previously used the patients NHS Number to find the patients logical id on the providers system, therefore the requested_record Patient SHOULD contain the NHS number identifier element. |
  | Read Appointment | NHS Number | Patient | The consumer will have previously used the patients NHS Number to find the patients logical id on the providers system, therefore the requested_record Patient SHOULD contain the NHS number identifier element. |  
  | Retrieve a patients appointments | NHS Number | Patient | The consumer will have previously used the patients NHS Number to find the patients logical id on the providers system, therefore the requested_record Patient SHOULD contain the NHS number identifier element. |
  | Amend an appointment | NHS Number | Patient | The consumer will have previously used the patients NHS Number to find the patients logical id on the providers system, therefore the requested_record Patient SHOULD contain the NHS number identifier element. |
  | Cancel an appointment | NHS Number | Patient | The consumer will have previously used the patients NHS Number to find the patients logical id on the providers system, therefore the requested_record Patient SHOULD contain the NHS number identifier element. |

 
  The following identifier systems SHALL be used when populating the relevant business identifiers:
  
  | Known business identifiers | Relevant business identifiers |
  | --- | --- |
  | NHS number | https://fhir.nhs.uk/Id/nhs-number |
  | ODS code | https://fhir.nhs.uk/Id/ods-organization-code |

  {% include note.html content="The provider SHALL validate that the requested_record claim details match the request parameters where possible, to ensure valid auditing of the requests end-to-end." %}
  

#### Population of requested_device ####

This claim is used to provide details of the originator of the request for auditing purposes, in the form of a FHIR device resource. 

Where the request originates from a device (for example a mobile device in a patient facing scenario), details of the device can be provided in manufacture, model and version elements.

Where the request originates from a system, the Spine endpoint URL of the originating system shall be specified using the URL element.

#### Population of ISS claim ####

As the consuming system is presently responsible for generating the access token, this SHALL contain the URL of the Spine endpoint of the consuming system.

In future OAuth2 implementation, the ISS claim will contain the URL of the OAuth2 authorisation server token endpoint.


### JWT payload example ###

```json
{
	"iss": "https://[ConsumerSystemURL]",
	"sub": "[PractitionerID]",
	"aud": "https://provider.thirdparty.nhs.uk/GP0001/STU3/1",
	"exp": 1469436987,
	"iat": 1469436687,
	"reason_for_request": "directcare",
	"requested_record": {
		"resourceType": "Patient",
		"identifier": [{
			"system": "https://fhir.nhs.uk/Id/nhs-number",
			"value": "[NHSNumber]"
		}]
	},
	"requested_scope": "patient/*.read",
	"requesting_device": {
		"resourceType": "Device",
		"identifier": [{
			"system": "[DeviceSystem]",
			"value": "[DeviceID]"
		}],
		"model": "[SoftwareName]",
		"version": "[SoftwareVersion]",
		"url": "https://[ConsumerSystemURL]"
	},
	"requesting_organization": {
		"resourceType": "Organization",
		"identifier": [{
			"system": "https://fhir.nhs.uk/Id/ods-organization-code",
			"value": "[ODSCode]"
		}],
		"name": "Requesting Organisation Name"
	"requesting_practitioner": {
		"resourceType": "Practitioner",
		"id": "[PractitionerID]",
		"identifier": [{
			"system": "https://fhir.nhs.uk/Id/sds-user-id",
			"value": "[SDSUserID]"
		},
		{
			"system": "https://fhir.nhs.uk/Id/sds-role-profile-id",
			"value": "[SDSRoleID]"
		},
		{
			"system": "[LocalUserSystem]",
			"value": "[LocalUserID]"
		}],
		"name": {
			"family": ["[Family]"],
			"given": ["[Given]"],
			"prefix": ["[Prefix]"]
		}
	}
}
```

{% include important.html content="Whilst the use of a JWT and the claims naming is inspired by the [SMART on FHIR](https://github.com/smart-on-fhir/smart-on-fhir.github.io/wiki/cross-organizational-auth) the GP Connect programme hasn't committed to using the SMART on FHIR specification." %}

Where the practitioner has both a local system role as well as a Spine RBAC role, then the Spine RBAC role SHALL be supplied.

## Example code ##

### C# ###

{% include tip.html content="The following code snippet utilises the [Microsoft Identity Model JWT Token NuGet Package](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/) for creating, serializing and validating JWT tokens." %}

```C#
var requesting_device = new Device {
	Id = "[DeviceID]",
	Model = "[SoftwareName]",
	Version = "[SoftwareVersion]",
	Identifier =
	{
		new Identifier("[DeviceSystem]", "[DeviceID]")
	}
};

var requesting_organization = new Organization {
	Id = "[OrganizationID]",
	Name = "Requesting Organisation Name",
	Identifier =
	{
		new Identifier("https://fhir.nhs.uk/Id/ods-organization-code", "[ODSCode]")
	}
};

var requesting_identity = new Practitioner {
	resourceType = "Practitioner",
	Id = "[PractitionerID]",
	PractitionerRole =
	{
		new role()
		{
			new coding("http://fhir.nhs.net/ValueSet/sds-job-role-name-1", "[SDSJobRoleName]")
		}
	},
	Name = new HumanName()
	{
			Prefix = new[] {"[Prefix]"},
			Given = new[] {"[Given]"},
			Family = new[] {"[Family]"}
	},
	Identifier =
	{
		new Identifier("http://fhir.nhs.net/sds-user-id", "[SDSUserID]"),
		new Identifier("[UserSystem]", "[UserID]")
	}
};

var subject_patient = new Patient {
	Identifier =
	{
		new Identifier("https://fhir.nhs.uk/Id/nhs-number","[NHSNumber]")
	}
};

var audit_event_id = "[AuditEventID]";
var requesting_system_url = "https://[ConsumerSystemURL]";
var requesting_system_token_url = "https://authorize.fhir.nhs.net/token";

// --this example getting local patient ID 1 at gp practice GP001
var target_request_url = "https://http://gpconnect.aprovider.nhs.net/GP0001/DSTU2/1/Patient/1";
var now = DateTime.UtcNow;
var expires = now.AddMinutes(5);

var claims = new List<System.Security.Claims.Claim>
{
    new System.Security.Claims.Claim("iss", requesting_system_url, ClaimValueTypes.String),
    new System.Security.Claims.Claim("sub", requesting_practitioner.Id, ClaimValueTypes.String),
    new System.Security.Claims.Claim("aud", target_request_url, ClaimValueTypes.String),
    new System.Security.Claims.Claim("exp", EpochTime.GetIntDate(expires).ToString(), ClaimValueTypes.Integer64),
    new System.Security.Claims.Claim("iat", EpochTime.GetIntDate(now).ToString(), ClaimValueTypes.Integer64),
    new System.Security.Claims.Claim("reason_for_request", "directcare", ClaimValueTypes.String),
    new System.Security.Claims.Claim("requested_scope", "patient/*.read", ClaimValueTypes.String),	
    new System.Security.Claims.Claim("requesting_device", FhirSerializer.SerializeToJson(requesting_device), JsonClaimValueTypes.Json),
    new System.Security.Claims.Claim("requesting_organization", FhirSerializer.SerializeToJson(requesting_organization), JsonClaimValueTypes.Json),
    new System.Security.Claims.Claim("requesting_identity", FhirSerializer.SerializeToJson(requesting_identity), JsonClaimValueTypes.Json)
};

// Serialize To Json
JwtPayload payload = new JwtPayload(claims);
var jsonPayload = payload.SerializeToJson();
jsonPayload.Dump();

```

## External documents / policy documents ##

| Name | Author | Version | Updated |
| GPSoC IG Requirements for GP Systems | NHS Digital | v4.0 | 19/09/2014 |
| GP Systems Interface Mechanism Requirements V 1| NHS Digital | v0.10|

