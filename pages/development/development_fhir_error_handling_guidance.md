---
title: Error handling guidance
keywords: fhir, development, operation outcome, error
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_error_handling_guidance.html
summary: "Details of the common error handling pattern(s) across all GP Connect FHIR&reg; APIs"
---

{% include important.html content="Please ignore any GPC-XXX format error codes defined in the *gpconnect-error-or-warning-code-1* value set / DMS guidance as these have now been superseded and will be removed in a future release." %}

### Operation outcome usage ####

The FHIR standard allows for an `OperationOutcome` to be returned for any/all errors both for Operations and for RESTful CRUD API calls.

- operation APIs **MUST** return an `OperationOutcome` in the event of an error
- RESTful APIs **MUST** return an `OperationOutcome` when a specific error code has for a certain situation (i.e. no patient consent to share)
- RESTful APIs **MUST** return an `OperationOutcome` when any other unexpected error occurs containing debug details in the `Diagnostics` field

{% include download.html content="A spreadsheet of [Expected Error Codes](downloads/development/expected_error_codes.xlsx) is available which covers the most common error scenarios." %}

### Identity validation errors ####

Provider systems **MUST** respond by returning one of the following `OperationOutcome` error codes in the case of a custom operation error (for example,`$gpc.getcarerecord`, `$gpc.registerpatient`).

| HTTP Code | Error Code | Description |
| --------- |------------|-------------|
| `400`     | INVALID_IDENTIFIER_SYSTEM | Invalid identifier system |
| `400`     | INVALID_IDENTIFIER_VALUE | Invalid identifier value |
| `400`     | INVALID_PATIENT_DEMOGRAPHICS | Invalid patient demographics (i.e. PDS trace failed) |
| `404`     | PATIENT_NOT_FOUND   | Patient record not found |
| `400`     | INVALID_NHS_NUMBER   | NHS Number invalid |
| `404`     | ORGANISATION_NOT_FOUND   | Organisation record not found |
| `400`     | INVALID_ODS_CODE   | ODS code invalid |
| `404`     | PRACTITIONER_NOT_FOUND   | Practitioner record not found |

#### Example - Invalid NHS Number supplied #####

For example, if an invalid NHS Number value is supplied to the `$gpc.getcarerecord` Operation the following error details would be returned:

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

#### Example - Patient not found #####

For example, a valid NHS Number value is supplied to the `$gpc.getcarerecord` Operation but no GP record exists for that patient then the following error details would be returned:

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

### Security validation errors ###

Provider systems **MUST** returning one of the following `OperationOutcome` error codes in the case of enforcing their local patient consent rules when responding to consumer API requests.

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `403` | NO_PATIENT_CONSENT | No Patient Consent To Share |
| `403` | NON_AUTHORITATIVE | Non Authoritative |

#### Example - No patient consent to share #####

For example, the patient has requested that their record not be shared via the `$gpc.getcarerecord` Operation then the following error details would be returned:

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

### Resource validation errors ###

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `422`     | INVALID_RESOURCE | Submitted resource is not valid. |
| `422`     | INVALID_PARAMETER | Submitted parameter is not valid. |
| `422`     | REFERENCE_NOT_FOUND | Referenced resource not found. |

#### Example - Invalid reference #####

For example, if the RESTful API fails when an invalid organisational reference is supplied, then the following error details would be returned:

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

### Internal server errors ###

When the error is **unexpected** and the server can't be more specific on the exact nature of the problem then the following `INTERNAL_SERVER_ERROR` **MUST** be used to return debug details.

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `500`     | INTERNAL_SERVER_ERROR | Unexpected internal server error. |

When the FHIR server has received a request for an operation or FHIR resource which is not (yet) implemented, then the NOT_IMPLEMENTED **SHOULD** be used.

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `501`     | NOT_IMPLEMENTED | FHIR resource or operation not implemented at server |



#### Example - Unexpected exception #####

For example, an unexpected internal exception is thrown by either an Operation or RESTful API, then the following error details would be returned:

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



### Malformed request errors ###

When the server cannot or will not process a request due to an apparent client error (for example, malformed request syntax, too large size, and so on) then the following `BAD_REQUEST` error **MUST** be used to return debug details.

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `400`     | BAD_REQUEST | Submitted request is malformed / invalid. |

#### Example - Malformed request syntax #####

For example, if the request could not be understood by the server due to malformed syntax, then the following error details would be returned:

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

### Spine Secure Proxy (SSP) errors ###

When the Spine Secure Proxy cannot or will not process a request then one of the following errors are used to return debug details:

| HTTP code | Issue type | Description of error  |
| --------- | ------- | ----------- |
| `400`     | invalid |  Target URL varies from endpoint registered in SDS | 
| `403`     | forbidden |  Sender ASID is not authorised for this interaction | 
| `403`     | forbidden |  Sender ASID is not authorised to send the interaction to receiver ASID | 
| `405`     | not-supported | Method not allowed |
| `415`     | not-supported | Unsupported media type |
| `502`     | transient | Error communicating to target URL |

#### SSP error example: Target URL varies from endpoint registered in SDS #####

```json
{
    "resourceType": "OperationOutcome", 
    "id": "09a01679-2564-0fb4-5129-aecc81ea2706",
    "issue": [
        {
            "code": "invalid", 
            "severity": "error", 
            "details": {
                "coding": [
                    {
                        "code": "400", 
                        "display": "ENDPOINT_https://supplier.thirdparty.nhs.uk/v1/fhir/_CPAID_S000000000001_VARIES_FROM_TARGETURL_https://supplier.thirdparty.nhs.uk/v1/test", 
                        "system": "http://fhir.nhs.net/ValueSet/gpconnect-schedule-response-code-1-0"
                    }
                ]
            },
            "diagnostics": "ENDPOINT_https://supplier.thirdparty.nhs.uk/v1/fhir/_CPAID_S000000000001_VARIES_FROM_TARGETURL_https://supplier.thirdparty.nhs.uk/v1/test",
        }
    ] 
}
```

#### SSP error example: Sender ASID is not authorised for this interaction #####

```json
{
    "resourceType": "OperationOutcome",
    "id": "10960df2-29d1-4e71-823c-c0bb9d723012",
    "issue": [
        {
            "code": "forbidden",
            "severity": "error",
            "details": {
                "coding": [
                    {
                        "code": "403",
                        "display": "ASID_CHECK_FAILED_MESSAGESENDER_100000000001",
                        "system": "http://fhir.nhs.net/ValueSet/gpconnect-schedule-response-code-1-0"
                    }
                ]
            },
            "diagnostics": "ASID_CHECK_FAILED_MESSAGESENDER_100000000001"
        }
    ]
}
```

#### SSP error example: Sender ASID is not authorised to send the interaction to receiver ASID #####

```json
{
    "resourceType": "OperationOutcome",
    "id": "43A8BB0D-195E-4CF4-86F9-E8514F6EB585",
    "issue": [
        {
            "code": "forbidden",
            "severity": "error",
            "details": {
                "coding": [
                    {
                        "code": "403",
                        "display": "FOT_CHECK_FAILED_MESSAGESENDER_200000000001_MESSAGERECEIVER_200000000002",
                        "system": "http://fhir.nhs.net/ValueSet/gpconnect-schedule-response-code-1-0"
                    }
                ]
            },
            "diagnostics": "FOT_CHECK_FAILED_MESSAGESENDER_200000000001_MESSAGERECEIVER_200000000002"
        }
    ]
}
```

#### SSP error example: Method not allowed #####

```json
{
  "resourceType": "OperationOutcome",
  "issue": [
    {
      "code": "forbidden",
      "severity": "fatal",
      "details": {
        "coding": [
          {
            "code": "405",
            "system": "https://fhir.nhs.uk/StructureDefinition/spine-operationoutcome-1",
            "display": "405: Method Not Allowed"
          }
        ]
      }
    }
  ]
}
```

#### SSP error example: Unsupported media type #####

```json
{
  "resourceType": "OperationOutcome",
  "id": "09a01679-2564-0fb4-5129-aecc81ea2706",
  "issue": [
    {
      "code": "not-supported",
      "severity": "error",
      "details": {
        "coding": [
          {
            "code": "415",
            "display": "Unsupported_Media_Type",
            "system": "http://fhir.nhs.net/ValueSet/gpconnect-schedule-response-code-1-0"
          }
        ]
      },
      "diagnostics": "Unsupported_Media_Type"
    }
  ]
}
```

#### SSP error example: Error communicating to target URL #####

```json
{
  "resourceType": "OperationOutcome",
  "id": "78D536C0-44D6-11E9-BFCD-17C1B88243CD",
  "issue": [
    {
      "code": "transient",
      "severity": "error",
      "details": {
        "coding": [
          {
            "display": "ERROR_COMMUNICATING_TO_ENDPOINT_URL_https://supplier.thirdparty.nhs.uk/D11111/STU3/1/GPConnect/Patient",
            "code": "502",
            "system": "http://fhir.nhs.net/ValueSet/gpconnect-schedule-response-code-1-0"
          }
        ]
      },
      "diagnostics": "ERROR_COMMUNICATING_TO_ENDPOINT_URL_https://supplier.thirdparty.nhs.uk/D11111/STU3/1/GPConnect/Patient"
    }
  ]
}
```
