---
title: Development overview
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development.html
summary: "Development overview to the Access Record Structured capability"
---

## Introduction ##

The Access Record Structured capability provides the ability to retrieve a patient's GP record in a structured and coded format; currently this consists of the following clinical areas:

- Allergies
- Medications

The capability consists of a single API operation for retrieving a patient's structured record, plus a capability statement operation describing the capability API, both of which are listed below in [API definition](accessrecord_structured_development.html#api-definition).

## Allergies and medication guidance

The following pages describe how allergies and medications recorded in general practice are represented in GP Connect:

- [Allergies guidance](accessrecord_structured_development_allergies_guidance.html)
- [Medication resource relationships](accessrecord_structured_development_medication_resource_relationships.html)
- [Medication guidance](accessrecord_structured_development_medication_guidance.html)

## FHIR&reg; resources ##

The [FHIR resources](accessrecord_structured_development_resources_overview.html) pages provide a detailed reference on population and consumption of the FHIR profiled resources used in this capability.

## FHIR&reg; examples ##

The following pages provide example request and response messages:

- [Allergies](accessrecord_structured_development_fhir_examples_allergies.html)
- [Medication](accessrecord_structured_development_fhir_examples_medication.html)

## API definition

The following API definitions are included in this capability:

- [Retrieve a patient’s structured record](accessrecord_structured_development_retrieve_patient_record.html)
- [Get the FHIR&reg; capability statement](accessrecord_structured_get_the_fhir_capability_statement.html)

## Spine interactions ##

The Access Record Structured capability message set includes the following set of Spine interactions:

| Operation                 | Interaction ID            |
|---------------------------|---------------------------|
| [Get Structured Record](accessrecord_structured_development_retrieve_patient_record.html) | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getstructuredrecord-1` |
| [Read Metadata (Access Record Structured)](accessrecord_structured_get_the_fhir_capability_statement.html) | `urn:nhs:names:services:gpconnect:structured:fhir:rest:read:metadata-1` |
