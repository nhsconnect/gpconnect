---
title: Access Record Structured - Operation Definition
keywords: getstructuredrecord, view
tags: [use_case,getstructuredrecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_resource_groups.html
summary: "Access record structured operation definition include group details"
---

## Operation Definition - GPConnect-GetStructuredRecord-Operation-1  ##

The following parameters are available to be returned in the response bundle:

- `patientNHSnumber`
- `includeAllergies`
- `includeMedication`


{% include important.html content="At least one of the include groups listed above must be supplied" %}

### patientNHSnumber ###

The NHS number of the patient whose record is being extracted, which must be traced or verified against the national demographics index

### includeAllergies ###

Includes resources representing a patient's allergies and intolerances in the response bundle. By default, resolved allergies and intolerances are not included.

The Allergies include group consists of the following FHIR resources:

- [AllergyIntolerance](http://www.hl7.org/fhir/STU3/allergyintolerance.html "AllergyIntolerance")
- [Patient](https://www.hl7.org/fhir/patient.html "Patient")
- [Practitioner](https://www.hl7.org/fhir/practitioner.html "Practitioner")

{: .center-image }
![AlleryIntolerance Resource Group diagram](images/access_structured/AllergyIntoleranceResourceGroup.png)


#### Part Parameters ####

The following describes the part parameters available for filtering in this include group:

| Name                  | Include Group | Type | Value | Comments |
| `includeResolvedAllergies.valueBoolean` | `Allergies` | `boolean` | `true` or `false` | Include resolved allergies and intolerances in the response bundle |




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
| `timePeriod.end` | `Medication` | `date` | `yyyy-mm-dd` | Restrict the patient's medication record to a specific time period (end date ) [Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `includePrescriptionIssues.valueBoolean` | `Medication` | `boolean` | `true` or `false` | Include individual prescription issues in the response bundle |



## Operation Definition ##

The request payload is a set of [Parameters](https://www.hl7.org/fhir/parameters.html) conforming to the `gpconnect-getstructuredrecord-operation-1` profiled `OperationDefinition`, see below:


```xml
<?xml version="1.0" encoding="UTF-8"?>
<OperationDefinition xmlns="http://hl7.org/fhir">
   <id value="GPConnect-GetStructuredRecord-Operation-1" />
   <meta>
      <lastUpdated value="2018-03-07T00:00:00+00:00" />
   </meta>
   <url value="https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1" />
   <version value="1.0.0" />
   <name value="GP Connect Get Structured Record" />
   <status value="draft" />
   <kind value="operation" />
   <date value="2018-03-07" />
   <publisher value="NHS Digital" />
   <contact>
      <name value="Interoperability Team" />
      <telecom>
         <system value="email" />
         <value value="interoperabilityteam@nhs.net" />
      </telecom>
   </contact>
   <description value="Get a patient's clinical record in a structured coded format." />
   <code value="gpc.getstructuredrecord" />
   <resource value="Patient" />
   <system value="false" />
   <type value="true" />
   <instance value="false" />
   <parameter>
      <name value="patientNHSnumber" />
      <use value="in" />
      <min value="1" />
      <max value="1" />
      <documentation value="The NHS number of the patient whose record is being extracted, which must be traced or verified against the national demographics index." />
      <type value="Identifier" />
   </parameter>
   <parameter>
      <name value="includeAllergies" />
      <use value="in" />
      <min value="0" />
      <max value="1" />
      <documentation value="Include resources representing a patient's allergies and intolerances in the response bundle. By default, resolved allergies and intolerances are not included." />
      <part>
         <name value="includeResolvedAllergies" />
         <use value="in" />
         <min value="0" />
         <max value="1" />
         <documentation value="Include resolved allergies and intolerances in the response bundle." />
         <type value="boolean" />
      </part>
   </parameter>
   <parameter>
      <name value="includeMedication" />
      <use value="in" />
      <min value="0" />
      <max value="1" />
      <documentation value="Include resources representing a patient's medication record in the response bundle." />
      <part>
         <name value="timePeriod" />
         <use value="in" />
         <min value="0" />
         <max value="1" />
         <documentation value="Restrict the patient's medication record to a specific time period." />
         <type value="Period" />
      </part>
      <part>
         <name value="includePrescriptionIssues" />
         <use value="in" />
         <min value="0" />
         <max value="1" />
         <documentation value="Include resources representing a patient's allergies and intolerances in the response bundle. By default, resolved allergies and intolerances are not included." />
         <type value="boolean" />
      </part>
   </parameter>
   <parameter>
      <name value="response" />
      <use value="out" />
      <min value="1" />
      <max value="1" />
      <documentation value="The patient structured coded record. This is returned as a bundle containing resources representing the record as requested by the given input parameters." />
      <type value="Bundle" />
      <profile>
         <reference value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-GetStructuredRecord-Bundle-1" />
      </profile>
   </parameter>
</OperationDefinition>
```
