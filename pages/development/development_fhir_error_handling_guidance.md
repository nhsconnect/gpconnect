---
title: Error Handling
keywords: fhir, development, operation outcome, error
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_error_handling_guidance.html
summary: "Details of the common error handling pattern(s) across all GP Connect FHIR APIs."
---

Provider systems SHALL respond by returning one of the following `OperationOutcome` error codes in the case of a custom operation error (i.e. `$gpc.getcarerecord`, `$gpc.getschedule`, `$gpc.registerpatient`).

### Identity Validation Errors ####

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

### Security Validation Errors ###

Provider systems SHALL returning one of the following `OperationOutcome` error codes in the case of enforcing their local patient consent/data sharing rules when responding to consumer API requests.

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `403` | NO_PATIENT_CONSENT | No Patient Consent To Share |
| `403` | NO_ORGANISATIONAL_CONSENT | No Organisational Consent To Share |
| `403` | NON_AUTHORITATIVE | Non Authoritative |

### Resource Validation Errors ###

| HTTP Code | Error Code | Description |
| --------- | ---------- | ----------- |
| `422`     | INVALID_RESOURCE | Submitted resource is not valid. |
| `422`     | INVALID_PARAMETER | Submitted parameter is not valid. |
| `422`     | REFERENCE_NOT_FOUND | Referenced resource not found. |

