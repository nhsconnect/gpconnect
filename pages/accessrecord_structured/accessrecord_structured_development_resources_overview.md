---
title: FHIR&reg; resources overview
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_resources_overview.html
summary: "List of FHIR resource profiles used in the Access Record Structured capability pack"
---

## Resources ##

The following profiled <span class="stu3">STU3</span> FHIR&reg; resources are used in this capability pack:

### Clinical ###

* [AllergyIntolerance](accessrecord_structured_development_allergyintolerance.html)
* [Medication](accessrecord_structured_development_medication.html)
* [MedicationStatement](accessrecord_structured_development_medicationstatement.html)
* [MedicationRequest](accessrecord_structured_development_medicationrequest.html)

### Administrative ###

* Patient
* Organization
* PractitionerRole
* Practitioner
* Location

{% include tip.html content="Please see the [Foundations](foundations.html) section for details on population and consumption of the administrative resources." %}

### Structural ###

* [Bundle](accessrecord_structured_development_bundle.html)
* [List](accessrecord_structured_development_list.html)

## CodeableConcept and common code and identifier systems ##

### Population of CodeableConcept ###

The `CodeableConcept` data type is used throughout this capability and the following guidance **SHALL** be followed in order to ensure consistent representation of coded data:

{% include note.html content="Please see [Guidance on the population of CodeableConcept](pages/accessrecord_structured/GuidanceOnCodableConcept.pdf)." %}

### Common code systems ###

The following common code systems are used when populating `CodeableConcept.coding.system` in resources for this capability:

| Name | Code system |
| ----------- | ------ |
| SNOMED CT   | `http://snomed.info/sct` |
| Read codes V2     | `http://read.info/readv2` |
| Read codes CTV3   | `http://read.info/ctv3` |
| EMIS drug codes | `https://fhir.hl7.org.uk/Id/emis-drug-codes` |
| Egton codes | `https://fhir.hl7.org.uk/Id/egton-codes` |
| Multilex drug codes | `https://fhir.hl7.org.uk/Id/multilex-drug-codes` |
| Resip UK Gemscript drug codes | `https://fhir.hl7.org.uk/Id/resipuk-gemscript-drug-codes` |

### Common identifier systems ###

The following common identifier systems are used when populating `Identifier.system` in resources for this capability:

| Name | Identifier system |
| ---------- | -------- |
| NHS number | `https://fhir.nhs.uk/Id/nhs-number` |
| ODS organisation code | `https://fhir.nhs.uk/Id/ods-organization-code` |
| ODS site code | `https://fhir.nhs.uk/Id/ods-site-code` |
| SDS user ID | `https://fhir.nhs.uk/Id/sds-user-id` |
| SDS role profile ID | `https://fhir.nhs.uk/Id/sds-role-profile-id` |
| General Medical Council (GMC) number | `https://fhir.hl7.org.uk/Id/gmc-number` |
| General Practitioner (GMP) number | `https://fhir.hl7.org.uk/Id/gmp-number` |
| Cross care setting identifier | `https://fhir.nhs.uk/Id/cross-care-setting-identifier` |
