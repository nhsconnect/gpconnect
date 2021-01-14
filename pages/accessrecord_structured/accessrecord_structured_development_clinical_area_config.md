---
title: Configuration for supported clinical areas
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_clinical_area_config.html
summary: "Configuration for supported clinical areas"
---
## Introduction
The Access Record Structured capability requires the ability to configure the availability of clinical areas in a Provider system. In the event that a clinical area isn't available, information for other clinical areas that are configured to be available would still be retrievable.  This is required to support the following scenarios:

- to manage First of Type implementations - one or more clinical areas that still require development and/or assurance could be turned off to accelerate the deployment of clinical areas that have been developed and assured
- managing clinical safety incidents - when FRA has been awarded, one or more clinical areas could be turned off if there was a clinical safety incident relating to them

Also, in addition to the [enablement switch defined in the non-functional requirements](development_api_non_functional_requirements.html#enablement) for GP Connect APIs, the Access Record Structured capability requires that one or more clinical areas can be turned off at individual sites.

## Requirements

### Clinical areas
The configuration of the Provider system **MUST** allow for clinical areas to be switched on or off for all sites without requiring a release. This MUST be achieved using a single configuration iten or action. For example, in the case of a clinical safety incident with a clinical area where a provider would be required to turn off the clinical area across their entire estate. Where information for a clinical area isn't returned, provider systems **MUST** return an `OperationOutcome` for each clinical area that isn't supported according to the rules below. The following clinical areas can be configured to be on or off:
- Medications
- Allergies
- Consultations
- Problems
- Uncategorised data
- Immunisations
- Investigations
- Referrals
- Diary entries
- Documents

Documents MUST be switched off when the Access Documents capability isn't [enabled at a practice](development_api_non_functional_requirements.html#enablement).

### Site switch
In addition to the above, the configuration of the Provider system **MUST** allow for the availability of a clinical area to be switched on or off at one or more sites without requiring a release. For example, in the scenario where there was a data quality issue with a clinical area at a single site. Where information for a clinical area isn't returned, provider systems **MUST** return an `OperationOutcome` for each clinical area that isn't available according to the rules below.

### Consumer systems
Consumer systems **MUST** be able to handle the unavailability of clinical areas and warn users that information hasn't been returned.

### Populating a warning
In the above scenarios, providers **MUST** respond in the following way:
- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- Include FHIR&reg; resources for clinical areas that are switched on
- as part of the returned bundle, include a single [`OperationOutcome`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1/_history/1.2) with an `issue` for each clinical area that has been disabled where:
  - `issue.code` = `not-supported`
  - `issue.severity` = `warning`
  - `issue.details.coding.system` = `https://fhir.nhs.uk/STU3/CodeSystem/Spine-ErrorOrWarningCode-1`
  - `issue.details.coding.code` = `NOT_IMPLEMENTED`
  - `issue.details.coding.display` = `Not implemented`
- For each disabled clinical area the following **MUST** be supplied:
  - `issue.details.text` = `<parameter-name>` has been disabled`
  - `issue.diagnostics` = `<parameter-name>`
  - Where the documents capability has been switched off 'Documents' MUST be returned in place of <parameter-name>

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
### Populating references to clinical areas that aren't available
Where clinical areas are unavailable, references to them will need to be populated with a warning that the information is unavailable:

Where a clinical area has been turned off, it will create a section.section.entry (or section.entry) entry with the:

-   `List.entry.item.display` set to “[Clinical area] items are unavailable.”

       Where [Clinical area] identifies the type of the clinical item that isn't available.

The example below shows references to two items, one for an observation and another for referrals that have been disabled in the provider system:

```json
{
  "item": {
    "reference": "Observation/6734572634"
  }
},
{
  "item": {
    "display": "Referral items have been disabled"
  }
}
```
