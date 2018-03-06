---
title: Structure access record include groups
keywords: getstructuredrecord, view
tags: [use_case,getstructuredrecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_resource_groups.html
summary: "Structured access record include groups"
---

## Structured Operation Definition - GPConnect-GetStructuredRecord-Operation-1  ##

The following two include groups are available to be returned in the response bundle:

- `includeMedication`
- `includeAllergyAndIntolerances`

{% include important.html content="At least one include group must be supplied" %}

?patientNHSnumber - The NHS number of the patient whose record is being extracted, which must be traced or verified against the national demographics index

### includeMedication ###

Includes resources representing a patient's medication record in the response bundle.

The includeMedication resource consists of the following FHIR resources:

- [MedicationStatement](https://www.hl7.org/fhir/medicationstatement.html "MedicationStatement")
- [MedicationRequest](https://www.hl7.org/fhir/medicationrequest.html "MedicationRequest")
- [Medication](http://www.hl7.org/fhir/STU3/medication.html "Medication")
- [Patient](https://www.hl7.org/fhir/patient.html "Patient")
- [Practitioner](https://www.hl7.org/fhir/practitioner.html "Practitioner")
- [Organization](https://www.hl7.org/fhir/organization.html "Organization")

{: .center-image }
![Medication Resource Group diagram](images/access_structured/MedicationResourceGroup.png)


#### Part Parameters ####

The following describes the part parameters available for filtering in this include group:

| Name                  | Include Group | Type | Value | Comments |
| `timePeriod.start` | `Medication` | `date` | `yyyy-mm-dd` | Restrict the patient's medication record to a specific time period (start date) [Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `timePeriod.end` | `Medication` | `date` | `yyyy-mm-dd` | Restrict the patient's medication record to a specific time period (end date )[Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `includePrescriptionIssues.valueBoolean` | `Medication` | `boolean` | `true` or `false` | Include individual prescription issues in the response bundle |


### includeAllergyAndIntolerances ###

Includes resources representing a patient's allergies and intolerances in the response bundle. By default, resolved allergies and intolerances are not included.

The AllergyAndIntolerances include group consists of the following FHIR resources:

- [AllergyIntolerance](http://www.hl7.org/fhir/STU3/allergyintolerance.html "AllergyIntolerance")
- [Patient](https://www.hl7.org/fhir/patient.html "Patient")
- [Practitioner](https://www.hl7.org/fhir/practitioner.html "Practitioner")

{: .center-image }
![AlleryIntolerance Resource Group diagram](images/access_structured/AllergyIntoleranceResourceGroup.png)


#### Part Parameters ####

The following describes the part parameters available for filtering in this include group:

| Name                  | Include Group | Type | Value | Comments |
| `includeResolvedAllergies.valueBoolean` | `AllergyAndIntolerances` | `boolean` | `true` or `false` | Include ended allergies in response, or not |



<!--
## Operation Definition ##

The request payload is a set of [Parameters](https://www.hl7.org/fhir/parameters.html) conforming to the `gpconnect-structuredrecord-operation-1` profiled `OperationDefinition`, see below:


```xml
to be added
```
-->
