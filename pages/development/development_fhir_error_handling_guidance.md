---
title: Error Handling
keywords: fhir, development, operation outcome, error
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_error_handling_guidance.html
summary: "Details of the common error handling pattern(s) across all GP Connect FHIR APIs."
---

{% include todo.html content="This page is published as a **work in progress** version and as such is subject to change. Once finalised all error codes presented here will be defined as part of the *gpconnect-error-or-warning-code-1* value set." %}

{% include important.html content="Please ignore any GPC-XXX format error codes defined in the *gpconnect-error-or-warning-code-1* value set / DMS guidance as these have now been superseded and will be removed in a future release." %}

### Operation Outcome Usage ####

The FHIR standard allows for an `OperationOutcome` to be returned for any/all errors both for Operations and for RESTful CRUD API calls.

- Operation APIs SHALL return an `OperationOutcome` in the event of an error.
- RESTful APIs SHALL return an `OperationOutcome` when a specific error code has for a certain situation (i.e. no patient consent to share).
- RESTful APIs SHALL return an `OperationOutcome` when any other unexpected error occurs containing debug details in the `Diagnostics` field.

{% include download.html content="A spreadsheet of [Expected Error Codes](downloads/development/expected_error_codes.xlsx) is available which covers the most common error scenarios." %}

### Identity Validation Errors ####

Provider systems SHALL respond by returning one of the following `OperationOutcome` error codes in the case of a custom operation error (i.e. `$gpc.getcarerecord`, `$gpc.getschedule`, `$gpc.registerpatient`).

| HTTP Code | Error Code | Description |
| --------- |------------|-------------|
| `400`     | INVALID_IDENTIFIER_SYSTEM | Invalid Identifier System |
| `400`     | INVALID_IDENTIFIER_VALUE | Invalid Identifier Value |
| `400`     | INVALID_PATIENT_DEMOGRAPHICS | Invalid Patient Demographics (i.e. PDS Trace Failed) |
| `404`     | PATIENT_NOT_FOUND   | Patient Record Not Found |
| `400`     | INVALID_NHS_NUMBER   | NHS Number Invalid |
| `404`     | ORGANISATION_NOT_FOUND   | Organisation Record Not Found |
| `400`     | INVALID_ODS_CODE   | ODS Code Invalid |
| `404`     | PRACTITIONER_NOT_FOUND   | Practitioner Record Not Found |
| `400`     | INVALID_SDS_USERID   | SDS UserID Invalid |

#### Example 1. Invalid NHS Number Supplied #####

For example if an invalid NHS Number value is supplied to the `$gpc.getcarerecord` Operation the following error details would be returned:

```json
{
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "value",
		"details": {
			"coding": [{
				"system": "http://fhir.nhs.net/ValueSet/gpconnect-error-or-warning-code-1",
				"code": "INVALID_NHS_NUMBER"
			}]
		},
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

#### Example 2. Patient Not Found #####

For example a valid NHS Number value is supplied to the `$gpc.getcarerecord` Operation but no GP record exists for that patient then the following error details would be returned:

```json
{
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "not-found",
		"details": {
			"coding": [{
				"system": "http://fhir.nhs.net/ValueSet/gpconnect-error-or-warning-code-1",
				"code": "PATIENT_NOT_FOUND"
			}]
		},
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

### Security Validation Errors ###

Provider systems SHALL returning one of the following `OperationOutcome` error codes in the case of enforcing their local patient consent rules when responding to consumer API requests.

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `403` | NO_PATIENT_CONSENT | No Patient Consent To Share |
| `403` | NON_AUTHORITATIVE | Non Authoritative |

#### Example 3. No Patient Consent To Share #####

For example the patient has requested that their record not be shared via the `$gpc.getcarerecord` Operation then the following error details would be returned:

```json
{
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "forbidden",
		"details": {
			"coding": [{
				"system": "http://fhir.nhs.net/ValueSet/gpconnect-error-or-warning-code-1",
				"code": "NO_PATIENT_CONSENT"
			}]
		},
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

### Resource Validation Errors ###

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `422`     | INVALID_RESOURCE | Submitted resource is not valid. |
| `422`     | INVALID_PARAMETER | Submitted parameter is not valid. |
| `422`     | REFERENCE_NOT_FOUND | Referenced resource not found. |

#### Example 4. Invalid Reference #####

For example sending/creating a new Task using the RESTful API fails as an invalid organisational reference is supplied, then the following error details would be returned:

```json
{
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "invalid",
		"details": {
			"coding": [{
				"system": "http://fhir.nhs.net/ValueSet/gpconnect-error-or-warning-code-1",
				"code": "REFERENCE_NOT_FOUND"
			}]
		},
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

### Unexpected Internal Server Errors ###

When the error is unexpected and the server can't be more specific on the exact nature of the problem then the following `INTERNAL_SERVER_ERROR` SHALL be used to return debug details.

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `500`     | INTERNAL_SERVER_ERROR | Unexpected internal server error. |

#### Example 5. Unexpected Exception #####

For example an unexpected internal exception is thrown by either an Operation or RESTful API, then the following error details would be returned:

```json
 {
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "exception",
		"details": {
			"coding": [{
				"system": "http://fhir.nhs.net/ValueSet/gpconnect-error-or-warning-code-1",
				"code": "INTERNAL_SERVER_ERROR"
			}]
		},
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

### Malformed Request ###

When the server cannot or will not process a request due to an apparent client error (e.g., malformed request syntax, too large size etc.) then the following `BAD_REQUEST` error SHALL be used to return debug details.

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `400`     | BAD_REQUEST | Submitted request is malformed / invalid. |

#### Example 6. Malformed Request Syntax #####

For example if the request could not be understood by the server due to malformed syntax, then the following error details would be returned:

```json
 {
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["http://fhir.nhs.net/StructureDefinition/gpconnect-operationoutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "invalid",
		"details": {
			"coding": [{
				"system": "http://fhir.nhs.net/ValueSet/gpconnect-error-or-warning-code-1",
				"code": "BAD_REQUEST"
			}]
		},
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```