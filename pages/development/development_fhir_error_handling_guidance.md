---
title: Error handling guidance
keywords: fhir, development, operation outcome, error
tags: [fhir,development,error]
sidebar: overview_sidebar
permalink: development_fhir_error_handling_guidance.html
summary: "Details of the common error handling pattern(s) across the GP Connect API"
---

### Operation outcome usage ####

In the event of an error, provider systems SHALL respond by providing an OperationOutcome resource profiled to [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) 

The `GPConnect-OperationOutcome-1`:
- SHALL contain a definition of severity in the `OperationOutcome.issue.severity` field providing a value from the [valueset-issue-severity](http://hl7.org/fhir/STU3/valueset-issue-severity.html) value set. In all cases described in this guidance, the value used will be `error`.
- SHALL contain a definition of the type of error in the `OperationOutcome.issue.code` element, providing a value from the [issue-type](http://hl7.org/fhir/STU3/valueset-issue-type.html) value set. 
- SHALL contain details of the `Spine error code` in the `OperationOutcome.issue.details.coding.code` and `OperationOutcome.issue.details.coding.display` fields. These shall be taken from the standard set of NHS Spine error codes as defined in the [spine-error-or-warning-code-1](https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1) value set. The Spine error and warning codes provide a greater degree of error handling granularity, and also ensure a standardised error handling approach across NHS APIs. 
- SHOULD provide additional diagnostic details of the error in `OperationOutcome.diagnostics` property where such securely provides additional error context for consumer applications.


The sections below provide guidance on the error details to be returned in a number of key scenarios.

### Identity validation errors ####

Provider systems SHALL respond by returning one of the following `OperationOutcome` error codes where FHIR resource identity error scenarios are encountered: 

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | -----------|------------|-------------|
| `400`     | value | INVALID_IDENTIFIER_SYSTEM | Invalid identifier system |
| `400`     | value | INVALID_IDENTIFIER_VALUE | Invalid identifier value |
| `400`     | value | INVALID_NHS_NUMBER   | NHS number invalid |
| `400`     | business-rule | INVALID_PATIENT_DEMOGRAPHICS | Invalid patient demographics (that is, PDS trace failed) |
| `404`     | not-found | ORGANISATION_NOT_FOUND   | Organisation record not found |
| `404`     | not-found | PATIENT_NOT_FOUND   | Patient record not found |
| `404`     | not-found | PRACTITIONER_NOT_FOUND   | Practitioner record not found |
| `404`     | not-found | NO_RECORD_FOUND | No record found |

#### Example: Invalid NHS number supplied #####

If an invalid NHS number value is supplied to the `$gpc.getcarerecord` operation, the following error details would be returned:

```json
{
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "value",
		"details": {
			"coding": [{
				"system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
				"code": "INVALID_NHS_NUMBER",
				"dispay": "Invalid NHS number"
			}]
		}
	}]
}
```

#### Example: Patient not found #####

For example, if a valid NHS number value is supplied to the `$gpc.getcarerecord` Operation but no GP record exists for that patient, then the following error details would be returned:

```json
{
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "not-found",
		"details": {
			"coding": [{
				"system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
				"code": "PATIENT_NOT_FOUND",
				"display": "Patient not found"
			}]
		}
	}]
}
```

#### Example: Resource not found ####

This is a catch-all where a request for a resource instance cannot be found at the FHIR server, where more specific Spine error codes (such as PATIENT_NOT_FOUND) cannot be used.

```json
{
	"resourceType": "OperationOutcome",
	"issue": [{
		"severity": "error",
		"code": "not-found",
		"details": {
			"coding": [{
				"system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
				"code": "NO_RECORD_FOUND",
				"display": "No record found"
			}]
		}
	}]
}
```

### Security validation errors ###

When responding to consumer API requests, provider systems SHALL return one of the following `OperationOutcome` details when enforcment of local consent rules result in an error condition: 

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | -----------|------------|-------------|
| `403` | forbidden | NO_PATIENT_CONSENT | Patient has not provided consent to share data |
| `403` | forbidden | NO_ORGANISATION_CONSENT | Organisation has not provided consent to share data |
| `403` | forbidden | ACCESS_DENIED | Access denied |

#### Example: No patient consent to share #####

For example, if the patient has requested that their record should not be shared then the following error details would be returned:

```json
{
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "forbidden",
		"details": {
			"coding": [{
				"system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
				"code": "NO_PATIENT_CONSENT",
				"display": "Patient has not provided consent to share data" 
			}]
		}
	}]
}
```

### Resource validation errors ###

Where FHIR resource validation issues arise during processing of consumer requests, provider systems SHALL utilise one the following error details:

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | ---------- | ---------- | ----------- |
| `422`     | invalid | INVALID_RESOURCE | Submitted resource is not valid. |
| `422`     | invalid | INVALID_PARAMETER | Submitted parameter is not valid. |
| `422`     | invalid | REFERENCE_NOT_FOUND | Referenced resource not found. |

INVALID_PARAMETER would be used in the following, or similar, scenarios:
- Unexpected parameter value for an custom operation. For example, a lowercase value is supplied to the recordSection parameter of the $gpc.getcarerecord operation.
- An invalid date/time value specified in a custom operaion parameter. For example, a invalid timePeriod defined in the timePeriod input parameter to the $gpc.getcarerecord operation.

INVALID_RESOURCE would be used in situations such as the following:
- Resource does to validate against StructureDefinition (either in request body, of in JWT claim)

REFERENCE_NOT_FOUND describes a scenario where a consumer POSTs a FHIR resource which contains a FHIR reference which are cannot be found. 

#### Example: Reference not found #####

For example, when using the 'Book an appointment' API use case, a consumer includes a reference to a slot which does not exist at the server. The following error details would be returned:

```json
{
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "invalid",
		"details": {
			"coding": [{
				"system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
				"code": "REFERENCE_NOT_FOUND",
				"display": "FHIR reference not found"
			}]
		},
	    "diagnostics": "Reference to Slot/6 - no such slot exists at the server"
		"location": "/f:Slot/f:6"
	}]
}
```

### Malformed request errors ###

When the server cannot or will not process a request due to an apparent client error then the following `BAD_REQUEST` error SHALL be used to return debug details.

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | ---------- | ---------- | ----------- |
| `400`     | invalid | BAD_REQUEST | Submitted request is malformed / invalid. |

BAD_REQUEST Spine error codes should be used in the following types of scenario:
- JSON Web Tokens (JWT) claims information is not valid JSON, is null, or has an invalid value 
- invalid FHIR resource in JWT claim (for example, patient resource when practitioner expected)
- JWT requested_record claim does not match request
- malformed JSON or XML content in request body
- an expected header (for example, `interaction ID header`) is missing or invalid
- invalid HTTP verb used (for example, using POST to read a patient)
- InteractionID header does not match request

#### Example: Malformed JSON claim in request #####

For example, if the request contained a null `aud` claim in the JWT, then the following error details would be returned:

```json
 {
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "invalid",
		"details": {
			"coding": [{
				"system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
				"code": "BAD_REQUEST",
				"display": "Bad request"
			}]
		},
		"diagnostics": "Empty JWT aud claim"
	}]
}
```



### Internal server errors ###

When the FHIR server has received an request for an operation or FHIR resource which is not (yet) implemented, then the NOT_IMPLEMENTED Spine error code SHALL be used.

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | ---------- | ---------- | ----------- |
| `501`     | not-supported | NOT_IMPLEMENTED | FHIR resource or operation not implemented at server |

When the error is **unexpected** and the server can't be more specific on the exact nature of the problem then the `INTERNAL_SERVER_ERROR` Spine error code SHALL be used, and diagnostics SHALL be included to provide detail of the error.

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | ------- | ---------- | ----------- |
| `500`     | processing | INTERNAL_SERVER_ERROR | Unexpected internal server error. |

#### Example: Unexpected exception #####

For example, an unexpected internal exception is thrown by either an Operation or RESTful API, then the following error details would be returned:

```json
 {
	"resourceType": "OperationOutcome",
	"meta": {
		"profile": ["https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"]
	},
	"issue": [{
		"severity": "error",
		"code": "exception",
		"details": {
			"coding": [{
				"system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
				"code": "INTERNAL_SERVER_ERROR",
				"display": "Internal server error"
			}]
		},
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```


### Spine Security Proxy (SSP) errors ###

When the Spine security proxy cannot or will not process a request then one of the following errors SHALL be used to return debug details:

| HTTP code | Issue type | Description of error  |
| --------- | ------- | ----------- |
| `403`     | forbidden |   The sender or receiver's ASID is not authorised for this interaction. | 
| `405`     | not-supported | Bad request for an unsupported HTTP verb such as TRACE. |
| `415`     | not-supported | A consumer application asked for an unsupported media type. |
| `502`     | transient | A downstream server is offline. |
| `504`     | transient| A downstream server timed out. |

#### SSP error example: ASID check failed #####

```json
{
	"resourceType": "OperationOutcome",
	"issue": [{
		"severity": "error",
		"code": "forbidden",
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

#### SSP error example: method not allowed #####

```json
{
	"resourceType": "OperationOutcome",
	"issue": [{
		"severity": "error",
		"code": "not-supported",
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

#### SSP error example: unsupported media type #####

```json
{
	"resourceType": "OperationOutcome",
	"issue": [{
		"severity": "error",
		"code": "not-supported",
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

#### SSP error example: bad gateway #####


```json
{
	"resourceType": "OperationOutcome",
	"issue": [{
		"severity": "error",
		"code": "transient",
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```

#### SSP error example: gateway timeout #####

```json
{
	"resourceType": "OperationOutcome",
	"issue": [{
		"severity": "error",
		"code": "transient",
		"diagnostics": "Any further internal debug details i.e. stack trace details etc."
	}]
}
```
