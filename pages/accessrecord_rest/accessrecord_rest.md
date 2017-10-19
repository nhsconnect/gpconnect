---
title: Access Record Structured Data
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_rest_sidebar
permalink: accessrecord_rest.html
summary: "Introduction to the GP Connect Access Record Structured Data capability"
---

{% include todo.html content="This capability pack is published as a **work in progress** version and as such is subject to change. It has been published to show the direction of travel and to serve as a discussion document for parties involved with the implementation and consumption of GP Connect FHIR based APIs." %}

FHIR resources in scope for RESTful care record access ([Maturity Model Stage 3.](designprinciples_maturity_model.html#stage-3-q4-2016-into-q1-2017)) are:

## Tranche 1. Structured ##

1. [AllergyIntolerance](accessrecord_rest_structured_data_allergyintolerance.html)
2. [Immunization](accessrecord_rest_structured_data_immunization.html)
3. [MedicationOrder](accessrecord_rest_structured_data_medicationorder.html)
4. [MedicationStatement](accessrecord_rest_structured_data_medicationstatement.html)
5. [Condition](accessrecord_rest_structured_data_condition.html)

## Tranche 2. Structured ##

6. DiagnosticOrder
7. DiagnosticReport
8. Encounter
9. Flag
10. MedicationDispense
11. MedicationAdministration
12. Observation
13. Problem
14. Procedure
15. Referral

### Purpose ###

This capability delivers the ability to access structured primary care record data for a given patient in order to provide new interoperability opportunities between primary care and other sectors. Access to the structured and coded record will allow much tighter interoperability than the basic HTML Views described above.

### Use Cases ###

- A health professional is able to view and import allergies into their local patient record system.
- Information is rendered natively in a system rather than embedded in a HTML view to provide a more seamless experience, e.g. mobile device.
- Information offered in a structured and coded form by the API for the purposes of reconciling medications, problems and allergies e.g. as part of an inpatient spell.

### Domain Message Specification ###

Please refer to the Domain Message Specification (DMS) bundle for details of the FHIR profiles utilised:

{% include dms.html link="http://data.developer.nhs.uk/fhir/candidaterelease-240117-getrecordstructured" content="Get Care Record Structured." %}
