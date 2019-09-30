---
title: API Version Compatibility
keywords: getstructuredrecord, view
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_version_compatibility.html
summary: "Retrieve a patient's record in structured format"
---

## Introduction ##

The GP Connect API requires that a solution for forwards and backwards compatibility is developed as there is the potential for multiple versions of the GP Connect API to be implemented by consumers and providers.

### Forwards and backwards compatibility ###

#### Forwards compatibility ####
Forwards compatibility is the scenario where a consumer requests a higher version of the API than the provider supports. This requires that a provider **MUST** be able to warn a consumer when they don't support a requested parameter or part parameter.

In this scenario, providers **MUST** respond in the following way:
- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- Include FHIR&reg; resources for supported parameters
- as part of the returned bundle, include a single [`OperationOutcome`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) with an `issue` for each unsupported parameter or part parameter where:
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

The example shows a fully populated [`OperationOutcome`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) for a request where the `includeConsultations` and `includeProblems` parameters weren't supported:

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
          "text": "includeConsultations is an unrecognised parameter"
        },
        "diagnostics": "includeConsultations"
      },
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
          "text": "includeProblems is an unrecognised parameter",
        },
        "diagnostics": "includeProblems"
      }
    ]
  }
}

```

<div markdown="span" class="alert alert-warning" role="alert">
	<i class="fa fa-warning"></i>
	<b>Note:</b> where no valid parameters are provided in a request, an OperationOutcome with a severity of error <b>MUST</b> to be returned as specified in the <a href="accessrecord_structured_development_retrieve_patient_record.html#error-handling">error handling section</a>
</div>

Providers **MUST** report unsupported parameters at the least granular level, that is, unsupported part parameters **MUST** only be reported when their top level parameter is supported.

Consumers **MUST** check for the presence of an [`OperationOutcome`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1) resource as specified above to check for incomplete data as a result of unsupported parameters. These warnings **MUST** be displayed to users to warn them that information is missing.

The following table gives an overview of which parameters are supported in each version of the GP Connect API:

|-------------------------|-------------------|
| Specification version | Parameters     |
| :------------------------- | :------------------- |
| 1.2.x       | includeMedication       |
|             | &nbsp;&nbsp;&#8627; includePrescriptionIssues|
|             | &nbsp;&nbsp;&#8627; medicationSearchFromDate|
|        | includeAllergies       |
|             | &nbsp;&nbsp;&#8627; includeResolvedAllergies|
 |||
 | 1.3.x       | includeMedication       |
 |             | &nbsp;&nbsp;&#8627; includePrescriptionIssues|
 |             | &nbsp;&nbsp;&#8627; medicationSearchFromDate|
 |        | includeAllergies       |
 |             | &nbsp;&nbsp;&#8627; includeResolvedAllergies|
 |        | includeConsultations       |
 |             | &nbsp;&nbsp;&#8627; consultationSearchPeriod|
 |             | &nbsp;&nbsp;&#8627; includeNumberOfMostRecent|
 |        | includeProblems       |
 |             | &nbsp;&nbsp;&#8627; includeStatus|
 |             | &nbsp;&nbsp;&#8627; includeSignificance|
 |        | includeImmunisations       |
 |        | includeUncategorisedData       |
 |             | &nbsp;&nbsp;&#8627; uncategorisedDataSearchPeriod|
 |||
 | 1.4.x       | includeMedication       |
 |             | &nbsp;&nbsp;&#8627; includePrescriptionIssues|
 |             | &nbsp;&nbsp;&#8627; medicationSearchFromDate|
 |        | includeAllergies       |
 |             | &nbsp;&nbsp;&#8627; includeResolvedAllergies|
 |        | includeConsultations       |
 |             | &nbsp;&nbsp;&#8627; consultationSearchPeriod|
 |             | &nbsp;&nbsp;&#8627; includeNumberOfMostRecent|
 |        | includeProblems       |
 |             | &nbsp;&nbsp;&#8627; includeStatus|
 |             | &nbsp;&nbsp;&#8627; includeSignificance|
 |        | includeImmunisations       |
 |        | includeUncategorisedData       |
 |             | &nbsp;&nbsp;&#8627; uncategorisedDataSearchPeriod|
 |        | includeInvestigations       |
 |             | &nbsp;&nbsp;&#8627; investigationSearchPeriod|
 |        | includeReferrals       |
 |             | &nbsp;&nbsp;&#8627; referralSearchPeriod|
 |-------------------------|-------------------|


Consumers **MAY** determine programmatically which parameters have been implemented by the provider using the following process:
- [retrieve the CapabilityStatement](foundations_use_case_get_the_fhir_capability_statement.html) from the provider
- Locate the value in CapabilityStatement.operation[name='gpc.getstructuredrecord'].definition.reference, this will be a reference to an OperationDefinition
- Perform a HTTP GET to the value that was retrieved in the previous step
- The parameters that are supported by the provider will be listed in OperationDefinition.parameters

To illustrate how forwards compatibility works, the following example has been included:
- [Retrieve consultations, problems, medications and allergies from a provider on version 1.2.4 of the GP Connect API](accessrecord_structured_development_fhir_examples_forwards_consultations.html)



#### Backwards compatibility ####
Backwards compatibility is the scenario where a consumer requests a lower version of the API than the provider supports. The GP Connect APIs have been developed to be backwards compatible by following the [rules for backwards compatibility](https://www.hl7.org/fhir/STU3/versions.html#b-compat) that are defined in the FHIR&reg; specification.

Consumers are required to ignore unexpected elements and process data that they understand. They **MUST** alert users to the fact that some information couldn't be displayed as it isn't supported.
