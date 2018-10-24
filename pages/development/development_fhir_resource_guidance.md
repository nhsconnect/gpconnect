---
title: FHIR resource guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_resource_guidance.html
summary: "Where to find details of what resources and operations a FHIR server should expose to be a fully compliant GP Connect solution"
---

GP Connect has specified profiled versions of the international [FHIR Resources](https://www.hl7.org/fhir/STU3/){:target="_blank"}, tailoring them to meet the requirements of the GP Connect use cases and to aid in interoperability between systems.

When creating the profiled FHIR resources GP Connect have aimed to improve interoperability by:

* aligning, where possible, to the base FHIR profiles. GP Connect has also aligned, where possible, to the FHIR resource profiles produced by CareConnect and InterOpen
* not making FHIR profile elements mandatory unless absolute certainty that this cardinality will apply for all existing and future use cases
* applying must support flags to elements which hold key information within the resources

The profiled FHIR resources required for each of the GP Connect capability packs are specified within the specific specification sections for each of the capabilities:

* [Foundations](datalibraryfoundation.html)
* [Access Record HTML](accessrecord.html)
* [Access Record Structured](accessrecord_structured_development_resources_overview.html)
* [Appointment Management](datalibraryappointment.html)

## General FHIR resource population requirements

### Population of optional elements

The purpose of GP Connect is to make the patient data stored within the GP systems available externally so that it can be used to help improve the quality of patient care across the NHS. To give patients the best care possible the data made available through the GP Connect API should be as complete as possible. Therefore, it is expected that both provider and consumers:

* ***SHALL*** populate all the elements within FHIR resources subject to any Capability-specific variance, where data is available within their system irrespective of the cardinality of the elements within the FHIR resource profiles.

As GP Connect has made the FHIR resources open to aid in interoperability this means that there are some elements included in FHIR profiles which are not applicable to our deployment settings, for example 'specialism' in the appointment resource. For these elements if the provider or consumer does not have data stored within their system the element will not be populated.

### Use of Must-Support flag

Some resource profiles used in GP Connect make use of the [Must-Support](https://www.hl7.org/fhir/STU3/conformance-rules.html#mustSupport) flag. 

Where a Must-Support flag is present on a resource element, a `consumer` system SHALL populate the field in the request body if data is available to do so, irrespective of the fact that field cardinality may be `0..1` or `0..*`. 

Similarly, `provider` systems SHALL populate an element in responses where data is available to do so, irrespective of optional cardinality. When a `provider` system receives data from a consumer for a field marked with the Must-Support flag, the provider system SHALL store this data field in such a way that the data element is preserved and the element can be populated in future responses to consumer requests for the resource in question.

If an element within a fhir profile is marked as must support then all sub elements of that element SHALL also be considered must support. For example, within the GP Connect Appointment profile the booking organization extension is flagged with must support on the extension, this means that the extension and all sub elements within the extension are must support and SHALL be stored in a way that the data is preserved and the booking organization can be populated in future responses to consumers requesting that resource.

For example, see the [Register a patient request body](foundations_use_case_register_a_patient.html#payload-request-body).


## FHIR resource element/data type specific population requirements

### id

The logical id of all FHIR resources SHALL be populated in accordance with the [FHIR specification requirements](https://www.hl7.org/fhir/STU3/resource.html#id), meaning that population of the element is expected.


### Address

The `Address` data type is used in many of the FHIR resources across the GP Connect API. Where an element using the `Address` data type is present in a FHIR resource the following population guidance SHALL be followed:

- The address SHALL be populated using the elements:
  - `line`
  - `city`
  - `district`
  - `postalCode`
  - `country`
  
- The `text` element SHOULD NOT be populated within the address.

- `use` SHALL be populated for patient addresses


### ContactPoint

The `ContactPoint` data type is used in many of the FHIR resources across the GP Connect API. Where an element using the `ContactPoint` data type is present in a FHIR resource the following population guidance SHALL be followed:

- The telecom detail (telephone number, email address etc) SHALL be populated using the element:
	- `value`

- `system` SHALL be populated in all circumstances

- `use` SHALL be populated for patient or patient contact telecom details
