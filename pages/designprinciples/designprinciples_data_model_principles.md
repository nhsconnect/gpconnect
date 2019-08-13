---
title: Data model principles
keywords: development, fhir, logical models
tags: [development,fhir]
sidebar: overview_sidebar
toc: false
permalink: designprinciples_data_model_principles.html
summary: "High-level design principles related to the FHIR&reg; profiles"
---

## Introduction

GP Connect versions 1.x use the [FHIR STU3](http://hl7.org/fhir/STU3/) standard to specify the API and data models (known as profiles).

## INTEROPen

GP Connect FHIR profiles specified within this site have been developed by NHS Digital and where available use CareConnect profiles created in collaboration with the INTEROPen community.

> The INTEROPen vision is to create a library of nationally defined HL7® FHIR® resources and interaction patterns that implementers can adopt to simplify integration and interoperability within England’s health and social care systems.
> 
> Find out more on the [INTEROPen website](https://www.interopen.org/)

## Profiling principles

When creating the profiled FHIR resources GP Connect have aimed to improve interoperability by:

* aligning, where available, to the CareConnect profiles produced by INTEOPen
* storing profiles on [GitHub](https://github.com/nhsconnect/gpconnect-fhir){:target="_blank"}
* publishing profiles to [fhir.nhs.uk](https://fhir.nhs.uk)
* carrying the major version in the name of a profile (for example, gpconnect-patient-1) and major/minor version within StructureDefinition/Conformance.
* not mandating profile elements unless this cardinality will apply for all existing and future use cases
* applying must support flags to elements which hold key information within the resources

## GP Connect FHIR profiles

> Please see the [FHIR resource guidance page](development_fhir_resource_guidance.html) for further information.
