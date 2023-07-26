---
title: FHIR&reg; resource population fundamentals
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_resources_overview.html
summary: "List of FHIR&reg; resource profiles used in the Access Record Structured capability pack"
---

## Population of CodeableConcept ##

The `CodeableConcept` data type is used throughout this capability and the following guidance **SHALL** be followed in order to ensure consistent representation of coded data:

{% include note.html content="Please see [Guidance on the population of CodeableConcept](pages/accessrecord_structured/GuidanceOnCodeableConcept.pdf)." %}

## Definitions of mandatory, required and optional

Throughout the profile pages within the specification we have a label for each data item named "Optionality", which details whether or not it has to be included in the resource. This item has 3 possible values:

1. Mandatory - if the data item **MUST** be recorded in the resource every time it is produced.
2. Required - if the system that is providing the data item contains this piece of data then it **MUST** include it in the resource.
3. Optional - the system has the option to include this data if it is available.

An example of a 'required' data item is the extension to the MedicationRequest profile for StatusReason.

StatusReason is used in GP Connect to carry information about why the status of a medication has been changed to stopped. In GP systems when a medication is stopped the clinician has to enter a date when it was stopped and the reason why it was stopped.

Clearly not every medication will have a status of stopped but when it does this information is of a high clinical importance and **MUST** be included in the message.

## Definition of 'Must support' for use in the FHIR profiles

In FHIR, it allows the use of a flag titled 'Must support' to be attached to any give data item. The FHIR specification states, "The meaning of "support" is not defined by the base FHIR specification, but can be set to true in a profile. When a profile does this, it SHALL also make clear exactly what kind of "support" is required".

In the GP Connect FHIR profiles, we have used the 'Must support' flag to represent the required data items as described above.

This leads to our definition for use in GP Connect:

**Must support** = if a system is providing resources and one of the items is flagged as 'Must support' the system **MUST** include the data item if it is available to be sent.

## Using the List resource ##

The `List` resource in FHIR is used to manage collections of resources.

In GP Connect, it is used to organise data returned by a query into groups of resources that can then be processed more easily. For each clinical area query, GP Connect will return a list that identifies the data returned for that query.

- when an API call returns data for more than one clinical area, the list will identify which data has been returned for which clinical area
- where there are no items returned, the list will be empty
- where the return includes warning messages (for example, when clinical data is excluded), those messages will be in the list profile.manage negation where no resources are present in a system to be returned by a query - an attribution that is common to the resources it references will be returned, differentiating between items at different stages of a workflow, providing a mechanism to deal with warnings that can be applied to the group of resources

## Warning codes

Details on the warning codes available in the GP Connect message and how they are populated are on the page [Returning data in lists page](accessrecord_structured_development_lists_for_message_structure.html).

## Common code systems ##

The following common code systems are used when populating `CodeableConcept.coding.system` in resources for this capability:

| Name                          | Code system                                               |
| ----                          | -----------                                               |
| SNOMED CT                     | `http://snomed.info/sct`                                  |
| Read codes V2                 | `http://read.info/readv2`                                 |
| Read codes CTV3               | `http://read.info/ctv3`                                   |
| EMIS drug codes               | `https://fhir.hl7.org.uk/Id/emis-drug-codes`              |
| Egton codes                   | `https://fhir.hl7.org.uk/Id/egton-codes`                  |
| Multilex drug codes           | `https://fhir.hl7.org.uk/Id/multilex-drug-codes`          |
| Resip UK Gemscript drug codes | `https://fhir.hl7.org.uk/Id/resipuk-gemscript-drug-codes` |

## Common identifier systems ##

The following common identifier systems are used when populating `Identifier.system` in resources for this capability:

| Name                                                             | Identifier system                                       |
| ----                                                             | -----------------                                       |
| NHS number                                                       | `https://fhir.nhs.uk/Id/nhs-number`                     |
| ODS organisation code                                            | `https://fhir.nhs.uk/Id/ods-organization-code`          |
| ODS site code                                                    | `https://fhir.nhs.uk/Id/ods-site-code`                  |
| SDS user ID                                                      | `https://fhir.nhs.uk/Id/sds-user-id`                    |
| SDS role profile ID                                              | `https://fhir.nhs.uk/Id/sds-role-profile-id`            |
| General Medical Council (GMC) number                             | `https://fhir.hl7.org.uk/Id/gmc-number`                 |
| General Practitioner (GMP) number                                | `https://fhir.hl7.org.uk/Id/gmp-number`                 |
| EPS prescription order item identifier                           | `https://fhir.nhs.uk/Id/prescription-order-item-number` |
| EPS short form prescription identifier                           | `https://fhir.nhs.uk/Id/prescription-order-number`      |
| e-Referral Service (e-RS) Unique Booking Reference Number (UBRN) | `https://fhir.nhs.uk/Id/UBRN`                           |

The following profiled <span class="stu3">STU3</span> FHIR&reg; resources are used in this capability pack:

### Business identifiers for resources

Each clinical resource will have a unique business identifier that will be persisted to help consuming systems distinguish data they have integrated previously to data which is new to them. These identifiers will be scoped by a supplier specific namespace to ensure uniqueness.

### Clinical ###

- [AllergyIntolerance](accessrecord_structured_development_allergyintolerance.html)
- [Medication](accessrecord_structured_development_medication.html)
- [MedicationStatement](accessrecord_structured_development_medicationstatement.html)
- [MedicationRequest](accessrecord_structured_development_medicationrequest.html)
- [Immunization](accessrecord_structured_development_immunization.html)
- [Observation - uncategorised data](accessrecord_structured_development_observation_uncategorisedData.html)
- [Observation - blood pressure](accessrecord_structured_development_observation_bloodpressure.html)
- [Encounter](accessrecord_structured_development_encounter.html)
- [List - consultation structure](accessrecord_structured_development_list_consultation.html)
- [Observation - narrative data](accessrecord_structured_development_guidance_observation_narrative.html)
- [Condition - ProblemHeader](accessrecord_structured_problems.html)
- [Diagnostic Report](accessrecord_structured_development_diagnosticreport.html)
- [Specimen](accessrecord_structured_development_specimen.html)
- [Observation - Test Group Header](accessrecord_structured_development_observation_testgroup.html)
- [Observation - Test Result](accessrecord_structured_development_observation_testresult.html)
- [Observation - Filing Comments](accessrecord_structured_development_observation_filingcomments.html)
- [ProcedureRequest](accessrecord_structured_development_procedurerequest.html)
- [ReferralRequest](accessrecord_structured_development_referralrequest.html)
- [ProcedureRequest - Diary Entry](accessrecord_structured_development_diaryentry.html)
- DocumentReference - see note below

{% include note.html content="DocumentReference is defined as part of a seperate [Access Document](access_documents.html) capability. Access Document complements Access Record Structured by allowing the querying and retrieval of documents for a patient." %}

### Administrative ###

- Patient
- Organization
- PractitionerRole
- Practitioner
- Location

{% include tip.html content="Please see the [Foundations](foundations.html) section for details on population and consumption of the administrative resources." %}

### Structural ###

- [Bundle](accessrecord_structured_development_bundle.html)
- [List](accessrecord_structured_development_list.html)
