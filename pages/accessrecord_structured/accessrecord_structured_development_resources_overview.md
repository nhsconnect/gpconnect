---
title: FHIR&reg; resource population fundamentals
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_resources_overview.html
summary: "List of FHIR resource profiles used in the Access Record Structured capability pack"
---

## Population of CodeableConcept ##

The `CodeableConcept` data type is used throughout this capability and the following guidance **SHALL** be followed in order to ensure consistent representation of coded data:

{% include note.html content="Please see [Guidance on the population of CodeableConcept](pages/accessrecord_structured/guidance-on-the-population-of-codeableconcept.pdf)." %}

## Using the List resource ##

The `List` resource in FHIR is used to help manage a collection of resources. In GP Connect it is used to identify the data returns for each query. For each clinical area query, GP Connect will return one or more predefined list that identifies the data returned for that query.

- When multiple queries in the same API call return data in the same profile, the list will identify which data in the profile has been returned for which query.
- Where there are no items returned, the list will be empty.
- Where the return includes warning messages (for example, when clinical data is excluded), those messages will be in the list profile.manage negation where no resources are present in a system to be returned by a query. An attribution that is common to the resources it references will be returned, differentiating between items at different stages of a workflow, providing a mechanism to deal with warnings that can be applied to the group of resources.

### Warning codes

The following table provides details of the warning codes that are to be used in the warningCode extension in GP Connect. More guidance for each code follows in the subsequent sections.

<table class='resource-attributes' border='1'>
  <tr>
    <td>Display</td>
    <td>Code</td>
    <td>Associated text</td>
  </tr>
  <tr>
    <td>Confidential Items</td>
    <td>confidential-items</td>
    <td>Items excluded due to confidentiality and/or patient preferences.</td>
  </tr>
  <tr>
    <td>Data in Transit</td>
    <td>data-in-transit</td>
    <td>Patient record transfer from previous GP practice not yet complete; information recorded before dd-Mmm-yyyy may be missing.</td>
  </tr>
  <tr>
    <td>Data Awaiting Filing</td>
    <td>data-awaiting-filing</td>
    <td>Patient data may be incomplete as there is data supplied by a third party awaiting review before becoming available.</td>
  </tr>
</table>

### Confidential items

Where items have been excluded from the returned resources due to patient consent preferences or as they are part of the exclusion dataset this **MUST** be indicated at the list level. If an item that would have been an entry in a list is excluded the warningCode field **MUST** be populated using the confidential items warning code from the above table. The associated text **MUST** also be added into the note field when the code is used.

### Data in transit

This only refers to data transmitted from GP to GP when a patient moves GP practice. This is where a patient is registered at their new GP practice but their medical records from their previous GP practice have not yet been received and/or incorporated into their new GP practice system. When this takes place all the lists returned **MUST** be populated using the data in transit warning code from the above table. The associated text **MUST** also be added into the note field when the code is used. Set dd-mmm-yyyy to the date the patient registered at their new GP practice.

### Data awaiting filing

Where data exists in a provider system workflow that has not yet been integrated into the patient record, then it **MUST** not be sent.

## Common code systems ##

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

## Common identifier systems ##

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
| EPS Line item identifier | 'https://fhir.nhs.uk/Id/eps-line-item-identifier' |


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
