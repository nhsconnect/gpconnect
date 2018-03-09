---
title: Operation Definition Parameters
keywords: getstructuredrecord, view
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_operation_definition_parameters.html
summary: "Access record structured operation definition parameter details"
---

### includeAllergies ###

Including the `includeAllergies` parameter will request resources representing a patient's allergies and intolerances in the response bundle. By default, resolved allergies and intolerances are not included.

{: .center-image }
![AlleryIntolerance Resource Group diagram](images/access_structured/AllergyIntoleranceResourceGroup.png)


#### includeAllergies sub (part) parameters ####

The following describes the part parameters available for filtering on this parameter:

| Name                  | Include Parameter | Type | Value | Optionality | Comments |
|-----------------------|-------------------|------|-------|:-----------:|----------|
| `includeResolvedAllergies.valueBoolean` | `Allergies` | `boolean` | `true` or `false` | Optional | Include resolved allergies and intolerances in the response bundle |

#### Provider details  ####

The folowing list describes the expected provider system behaviours based on `includeResolvedAllergies` parameter:

> - Where the consumer system has requested `includeResolvedAllergies`, the provider systems **MUST** return all the allergy, adverse reaction, sensitivity and future propensity for an adverse reaction data that is recorded as resolved (ended)
> - The resolved allergy information **MUST** be explicitely segregated from the active allergy information


### includeMedication ###

Includes the 'includeMedication' parameter will request resources representing a patient's medication record in the response bundle.

{: .center-image }
![Medication Resource Group diagram](images/access_structured/MedicationResourceGroup.png)


#### Part Parameters ####

The following describes the part parameters available for filtering on this parameter:

| Name                  | Include Parameter | Type | Value | Optionality | Comments |
|-----------------------|-------------------|------|-------|:-----------:|----------|
| `timePeriod.start` | `Medication` | `date` | `yyyy-mm-dd` | Optional |Restrict the patient's medication record to a specific time period (start date) [Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `timePeriod.end` | `Medication` | `date` | `yyyy-mm-dd` | Optional | Restrict the patient's medication record to a specific time period (end date ) [Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `includePrescriptionIssues.valueBoolean` | `Medication` | `boolean` | `true` or `false` | Optional | Include individual prescription issues in the response bundle |

#### Provider details  ####


The folowing list describes the expected provider system behaviours based on `timePeriod` parameter:

> - The provider system **MUST** return the medication summary data items for all medications with a `lastIssueDate` which falls within the `timePeriod.start` and `timePeriod.end` date range (inclusive). 
> - Where a medication does not have a `lastIssueDate`, the provider system **MUST** return the medication summary data items for all medications whose `effective[x]` date range overlaps the `timePeriod.start` and `timePeriod.end` date range (inclusive).
> - Where a medication does not have a `lastIssueDate` or `effective[x]` date range, the provider system **MUST** return the medication summary data items for all medications whose `effective[x]` start date falls within the `timePeriod.start` and `timePeriod.end` date range (inclusive).
> - Where a medication does not have a `lastIssueDate`, `effective[x]` date range or `effective[x]` start date, the provider system **MUST** return the medication summary data items for all medications whose `dateAsserted` date falls within the `timePeriod.start` and `timePeriod.end` date range (inclusive).


The folowing list describes the expected provider system behaviours based on `includePrescriptionIssues` parameter:

> - Where the consumer system has requested `includePrescriptionIssues`, the provider **MUST** return all medication issue data items related to the medication summaries that are returned
> - Where the consumer system has not requested `includePrescriptionIssues`, the provider **MUST** **NOT** return medication issue data items

