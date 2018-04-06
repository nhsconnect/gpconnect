---
title: Operation definition
keywords: getstructuredrecord, view
tags: [structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_operation_definition.html
summary: "Operation definition for retrieving a patient's structured record"
---

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
      <documentation value="The NHS Number of the patient whose record is being extracted, which must be traced or verified against the national demographics index." />
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
         <name value="medicationDatePeriod" />
         <use value="in" />
         <min value="0" />
         <max value="1" />
         <documentation value="Restrict the patient's medication record to a specific date period. Only date values (and not time) may be provided." />
         <type value="Period" />
      </part>
      <part>
         <name value="includePrescriptionIssues" />
         <use value="in" />
         <min value="0" />
         <max value="1" />
         <documentation value="Include each prescription issue in the response. By default, prescription issues are not included." />
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
         <reference value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1" />
      </profile>
   </parameter>
</OperationDefinition>
```
