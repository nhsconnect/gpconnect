---
title: Structure access record resource groups
keywords: getstructuredrecord, view
tags: [use_case,getstructuredrecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_resource_groups.html
summary: "Structured access record resource groups"
---

## Structured Resource Groups ##

The following two groups are available to be returned:

- `Medication`
- `AllergyIntolerance`


### Resource Group - Medication ###

The Medication resource group consists of the following FHIR resources:

- [MedicationStatement](https://www.hl7.org/fhir/medicationstatement.html "MedicationStatement")
- [MedicationRequest](https://www.hl7.org/fhir/medicationrequest.html "MedicationRequest")
- [Medication](http://www.hl7.org/fhir/STU3/medication.html "Medication")
- [Patient](https://www.hl7.org/fhir/patient.html "Patient")
- [Practitioner](https://www.hl7.org/fhir/practitioner.html "Practitioner")
- [Organization](https://www.hl7.org/fhir/organization.html "Organization")

{: .center-image }
![Medication Resource Group diagram](images/access_structured/MedicationResourceGroup.png)


#### Part Parameters ####

The following describes the part parameters available for filtering in this resource group:

| Name                  | Resource Group | Type | Value | Comments |
| `timePeriod.start` | `Medication` | `date` | `yyyy-mm-dd` | [Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `timePeriod.end` | `Medication` | `date` | `yyyy-mm-dd` | [Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `includeIssues.valueBoolean` | `Medication` | `boolean` | `true` or `false` | Include associated issues in response, or not |


### Resource Group - AllergyIntolerance ###

The AllergyIntolerance resource group consists of the following FHIR resources:

- [AllergyIntolerance](http://www.hl7.org/fhir/STU3/allergyintolerance.html "AllergyIntolerance")
- [Patient](https://www.hl7.org/fhir/patient.html "Patient")
- [Practitioner](https://www.hl7.org/fhir/practitioner.html "Practitioner")


{: .center-image }
![AlleryIntolerance Resource Group diagram](images/access_structured/AllergyIntoleranceResourceGroup.png)


#### Part Parameters ####

The following describes the part parameters available for filtering in this resource group:

| Name                  | Resource Group | Type | Value | Comments |
| `includeResolvedAllergies.valueBoolean` | `AllergyIntolerance` | `boolean` | `true` or `false` | Include ended allergies in response, or not |



<!--
## Operation Definition ##

The request payload is a set of [Parameters](https://www.hl7.org/fhir/parameters.html) conforming to the `gpconnect-structuredrecord-operation-1` profiled `OperationDefinition`, see below:


```xml
<Parameters xmlns="http://hl7.org/fhir">
	<id value="b28bbed9-55b1-46ea-b019-b984a156decc"/>
	<meta>
		<profile value="https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-AccessStructuredRecord-1"/>
	</meta>	
	<parameter>
		<name value="patientNHSnumber"/>
		<valueIdentifier id="4569871235"/>
	</parameter>
	<parameter>
		<name value="includeResourceGroup:Medication"/>
			<part>
				<name value="timePeriod"/>
				<valuePeriod>
					<start value="2017-01-01"/>
					<end value="2018-02-01"/>
				</valuePeriod>
			</part>
			<part>
				<name value="includeIssues"/>
				<valueBoolean value="true"/>
			</part>
	</parameter>
	<parameter>
		<name value="includeResourceGroup:AllergyIntolerance"/>
			<part>
				<name value="includeResolvedAllergies"/>
				<valueBoolean value="true"/>
			</part>
	</parameter>
</Parameters>
```
-->
