---
title: Cross Organisation Audit & Provenance
keywords: spine, ssp, integration, audit, provenance
tags: [integration]
sidebar: overview_sidebar
permalink: integration_cross_organisation_audit_and_provenance.html
summary: "Overview of how audit and provenance data is expected to be transported over the GP Connect FHIR interfaces."
---

## Cross Organisation Audit & Provenance ##

Consumer systems SHALL provided audit and provenance details in the HTTP authorization header as an oAuth bearer token (as outlined in [RFC 6749](https://tools.ietf.org/html/rfc6749){:target="_blank"}) in the form of a JSON Web Token (JWT) as defined in [RFC 7519](https://tools.ietf.org/html/rfc7519){:target="_blank"}.

### JSON Web Tokens (JWT) ###

Consumer system SHALL generate a new JWT for each API request.

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
| requesting_organization | R | FHIR organisation resource making the request | No | FHIR Organization<sup>1</sup> | 
| requesting_practitioner | R | FHIR practitioner resource making the request | No | FHIR Practitioner<sup>1+3</sup> |

<sup>1</sup> Minimal FHIR resource to include any relevant business identifier(s).

<sup>2</sup> Patient scope for patient centric APIs (i.e. Get Care Record and Patient's Appointments, Patient Task) or scope for organisation centric APIs (i.e. Get Organization Schedule)

<sup>3</sup> To contain the practitioners local system identifier(s) (i.e. login details / username).

## JWT Example ##

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

{% include important.html content="Whilst the use of a JWT and the claims naming is inspired by the [SMART on FHIR](https://github.com/smart-on-fhir/smart-on-fhir.github.io/wiki/cross-organizational-auth) the GP Connect programme hasn't commit to using the SMART on FHIR specification." %}

{% include todo.html content="Spine RBAC role support to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

### Example Code ###

#### C# ####

{% include tip.html content="The following code snippet utilise the [Microsoft Identity Model JWT Token Nuget Package](https://www.nuget.org/packages/System.IdentityModel.Tokens.Jwt/) for creating, serializing and validating JWT tokens." %}

{% gist michaelmeasures/d6a75e52acdbee93c4c30d23e639fb1a %}

{% include links.html %}