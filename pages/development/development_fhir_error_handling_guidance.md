---
title: Error handling
keywords: fhir, development, operation outcome, error
tags: [fhir,development,error]
sidebar: overview_sidebar
permalink: development_fhir_error_handling_guidance.html
summary: "Details of the common error handling pattern(s) across the GP Connect API"
---

As a nationally brokered FHIR&reg; API, the GP Connect error handling approach defined below closely follows the approach of the Spine Core FHIR API Framework.

However, the guidance given below is the definitive error handling definition for the GP Connect API and thus the [Spine Core error handling guidance](https://developer.nhs.uk/apis/spine-core-1-0/resources_error_handling.html) should be viewed for context only.

### Operation outcome usage ####

In the event of an error, provider systems **SHALL** respond by providing an OperationOutcome resource profiled to [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1). 

The `GPConnect-OperationOutcome-1`:
- **SHALL** contain a definition of severity in the `OperationOutcome.issue.severity` field providing a value from the [valueset-issue-severity](http://hl7.org/fhir/STU3/valueset-issue-severity.html) value set. In all cases described in this guidance, the value used will be `error`.
- **SHALL** contain a definition of the type of error in the `OperationOutcome.issue.code` element, providing a value from the [issue-type](http://hl7.org/fhir/STU3/valueset-issue-type.html) value set. 
- **SHALL** contain details of the `Spine error code` in the `OperationOutcome.issue.details.coding.code` and `OperationOutcome.issue.details.coding.display` fields. These shall be taken from the standard set of NHS Spine error codes as defined in the [spine-error-or-warning-code-1](https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1) value set. The Spine error and warning codes provide a greater degree of error handling granularity, and also ensure a standardised error handling approach across NHS APIs. 
- **SHOULD** provide additional diagnostic details of the error in the `OperationOutcome.diagnostics` property where such details securely provide additional error context for consumer applications.


The sections below provide guidance on the error details to be returned in a number of key scenarios.

### Identity validation errors ####

Provider systems **SHALL** respond by returning one of the following `OperationOutcome` error codes where FHIR resource identity error scenarios are encountered: 

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

If an invalid NHS number value is supplied to the `$gpc.getstructuredrecord` operation, the following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "value",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "INVALID_NHS_NUMBER",
            "display": "Invalid NHS number"
          }
        ]
      }
    }
  ]
}
```

#### Example: Patient not found #####

For example, if a valid NHS number value is supplied to the `$gpc.getstructuredrecord` operation but no active GP record exists for that patient, then the following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "not-found",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "PATIENT_NOT_FOUND",
            "display": "Patient not found"
          }
        ]
      }
    }
  ]
}
```

#### Example: Resource not found ####

This is a catch-all where a request for a resource instance cannot be found at the FHIR server, where more specific Spine error codes (such as PATIENT_NOT_FOUND) cannot be used.

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "not-found",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "NO_RECORD_FOUND",
            "display": "No record found"
          }
        ]
      }
    }
  ]
}
```

### Security validation errors ###

When responding to consumer API requests, provider systems **SHALL** return one of the following `OperationOutcome` details when enforcement of local consent rules result in an error condition: 

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
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "forbidden",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "NO_PATIENT_CONSENT",
            "display": "Patient has not provided consent to share data"
          }
        ]
      }
    }
  ]
}
```

### Duplicate errors ###

When responding to consumer API requests, provider systems **SHALL** return one of the following `OperationOutcome` details when a resource could not be created or updated because it would cause a duplicate in the provider system:

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | -----------|------------|-------------|
| `409` | duplicate | DUPLICATE_REJECTED | Create would lead to creation of a duplicate resource |

#### Example: Attempting to register a patient that already exists #####

For example, if the consumer attempted to register a patient that already has an active record on the provider system the error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "duplicate",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "DUPLICATE_REJECTED",
            "display": "Create would lead to creation of duplicate resource"
          }
        ]
      },
      "diagnostics": "Patient record already exists with that NHS number"
    }
  ]
}
```

### Resource validation errors ###

Where FHIR resource validation issues arise during processing of consumer requests, provider systems **SHALL** utilise one the following error details:

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | ---------- | ---------- | ----------- |
| `422`     | invalid | INVALID_RESOURCE | Submitted resource is not valid. |
| `422`     | invalid | INVALID_PARAMETER | Submitted parameter is not valid. |
| `422`     | invalid | REFERENCE_NOT_FOUND | Referenced resource not found. |

Detailed diagnostic information **MUST** be supplied when erroring on the codes above.

INVALID_PARAMETER would be used in the following, or similar, scenarios:
- Unexpected parameter value for a custom operation. For example, a lowercase value is supplied to the recordSection parameter of the $gpc.getcarerecord operation.
- An invalid date/time value specified in a custom operation parameter. For example, an invalid timePeriod defined in the timePeriod input parameter to the $gpc.getcarerecord operation.

INVALID_RESOURCE would be used in situations such as the following:
- Resource fails to validate against StructureDefinition (either in request body or in JSON Web Tokens (JWT) claim).
- A resource fails to be processed because of a FHIR constraint, or other rule application, where the error is not already covered by other error codes

REFERENCE_NOT_FOUND describes a scenario where a consumer POSTs a FHIR resource which contains a FHIR reference that cannot be found. 

#### Example: Reference not found #####

For example, when using the 'Book an appointment' API use case, a consumer includes a reference to a slot which does not exist at the server. The following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "invalid",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "REFERENCE_NOT_FOUND",
            "display": "FHIR reference not found"
          }
        ]
      },
      "diagnostics": "Reference to Slot/6 - no such slot exists at the server"
    }
  ]
}
```

### Malformed request errors ###

When the server cannot or will not process a request due to an apparent client error then the following `BAD_REQUEST` error **SHALL** be used to return debug details.

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | ---------- | ---------- | ----------- |
| `400`     | invalid | BAD_REQUEST | Submitted request is malformed/invalid. |

BAD_REQUEST Spine error codes should be used in the following types of scenario:
- JWT claims information is not valid JSON, is null, or has an invalid value 
- invalid FHIR resource in JWT claim (for example, patient resource when practitioner expected)
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
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "invalid",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "BAD_REQUEST",
            "display": "Bad request"
          }
        ]
      },
      "diagnostics": "Empty JWT aud claim"
    }
  ]
}
```



### Internal server errors ###

When the FHIR server has received a request for an operation or FHIR resource which is not (yet) implemented, then the NOT_IMPLEMENTED Spine error code **SHALL** be used.

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | ---------- | ---------- | ----------- |
| `501`     | not-supported | NOT_IMPLEMENTED | FHIR resource or operation not implemented at server |

When the error is **unexpected** and the server can't be more specific on the exact nature of the problem then the `INTERNAL_SERVER_ERROR` Spine error code **SHALL** be used, and diagnostics **SHALL** be included to provide detail of the error.

| HTTP code | Issue type |Spine error code - code | Spine error code - display |
| --------- | ------- | ---------- | ----------- |
| `500`     | processing | INTERNAL_SERVER_ERROR | Unexpected internal server error. |

#### Example: Unexpected exception #####

For example, if an unexpected internal exception is thrown by either an Operation or RESTful API, then the following error details would be returned:

```json
{
  "resourceType": "OperationOutcome",
  "meta": {
    "profile": [
      "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
    ]
  },
  "issue": [
    {
      "severity": "error",
      "code": "exception",
      "details": {
        "coding": [
          {
            "system": "https://fhir.nhs.uk/STU3/ValueSet/Spine-ErrorOrWarningCode-1",
            "code": "INTERNAL_SERVER_ERROR",
            "display": "Internal server error"
          }
        ]
      },
      "diagnostics": "Any further internal debug details i.e. stack trace details etc."
    }
  ]
}
```


### Spine Secure Proxy (SSP) errors ###

When the Spine Secure Proxy cannot or will not process a request then one of the following errors **SHALL** be used to return debug details:

| HTTP code | Issue type | Description of error  |
| --------- | ------- | ----------- |
| `400`     | invalid |  Target URL varies from endpoint registered in SDS | 
| `403`     | forbidden |  Sender ASID is not authorised for this interaction | 
| `403`     | forbidden |  Sender ASID is not authorised to send the interaction to receiver ASID | 
| `405`     | not-supported | Method not allowed |
| `415`     | not-supported | Unsupported media type |
| `502`     | transient | Error communicating to target URL |
| `504`     | transient| Server at target URL timed out |

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
            "severity": "error",
            "code": "forbidden",
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
TBC
```

#### SSP error example: Unsupported media type #####

```json
{
  "resourceType": "OperationOutcome",
  "id": "09a01679-2564-0fb4-5129-aecc81ea2706",
  "issue": [
    {
      "details": {
      "code": "not-supported",
      "severity": "error",
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
      "severity": "error",
      "code": "transient",
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

#### SSP error example: Server at target URL timed out #####

```json
TBC
```
