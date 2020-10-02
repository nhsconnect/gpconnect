---
title: Configuration for supported clinical areas
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_clinical_area_config.html
summary: "Configuration for supported clinical areas"
---
## Introduction
The Access Record Structured capability requires the ability to configure the availability of clinical areas in a Provider system. This is required to support the following scenarios:

- to manage First of Type implementations - one or more clinical areas that still require development and/or assurance could be turned off to accelerate the deployment of clinical areas that have been developed and assured
- managing clinical safety incidents - when FRA has been awarded, one or more clinical areas could be turned off if there was a clinical safety incident relating to them

Also, in addition to the [enablement switch defined in the non-functional requirements](development_api_non_functional_requirements.html#enablement) for GP Connect APIs, the Access Record Structured capability requires that one or more clinical areas can be turned off at individual sites.

## Requirements

### Clinical areas
The configuration of the Provider system **MUST** allow for clinical areas to be switched on or off for all sites without requiring a release. For example, in the case of a clinical safety incident with a clinical area where a provider would be required to turn off the clinical area across their entire estate. Where information for a clinical area isn't returned, provider systems **MUST** return an `OperationOutcome` for each clinical area that isn't supported according to the rules below.

### Site switch
In addition to the above, the configuration of the Provider system **MUST** allow for a clinical area to be switched on or off at one or more sites without requiring a release. For example, in the scenario where there was a data quality issue with a clinical area at a single site. Where information for a clinical area isn't returned, provider systems **MUST** return an `OperationOutcome` for each clinical area that isn't supported according to the rules below.

### Consumer systems
Consumer systems **MUST** be able to handle the unavailability of clinical areas and warn users that information hasn't been returned.

### Populating a warning
In the above scenarios, providers **MUST** respond in the following way:
- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- Include FHIR&reg; resources for supported parameters
- as part of the returned bundle, include a single [`OperationOutcome`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1/_history/1.2) with an `issue` for each unsupported parameter or part parameter where:
  - `issue.code` = `not-supported`
  - `issue.severity` = `warning`
  - `issue.details.coding.system` = `https://fhir.nhs.uk/STU3/CodeSystem/Spine-ErrorOrWarningCode-1`
  - `issue.details.coding.code` = `NOT_IMPLEMENTED`
  - `issue.details.coding.display` = `Not implemented`
- Where it's an unsupported parameter the following **MUST** be supplied:
  - `issue.details.text` = `<parameter-name>` is an unrecognised parameter`
  - `issue.diagnostics` = `<parameter-name>`
- Where it's an unsupported part parameter the following **MUST** be supplied:
  - `issue.details.text` = `<parameter-name>.<part-parameter-name> is an unrecognised parameter`
  - `issue.diagnostics` = `<parameter-name>.<part-parameter-name>`

  The example shows a fully populated [`OperationOutcome`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1/_history/1.2) for a request where the `includeProblems` clinical area has been turned off:

  ```
  {
    "resource": {
      "resourceType": "OperationOutcome",
      "id": "8b679981-e9be-4e37-b103-799295a6aec8",
      "meta": {
        "profile": [
          "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1"
        ]
      },
      "issue": [
        {
          "severity": "warning",
          "code": "not-supported",
          "details": {
            "coding": [
              {
                "system": "https://fhir.nhs.uk/STU3/CodeSystem/Spine-ErrorOrWarningCode-1",
                "code": "NOT_IMPLEMENTED",
                "display": "Not implemented"
              }
            ],
            "text": "includeProblems has been disabled",
          },
          "diagnostics": "includeProblems"
        }
      ]
    }
  }

  ```
