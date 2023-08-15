---
title: FHIR&reg; resources
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_resource_guidance.html
summary: "Where to find details of what resources and operations a FHIR server should expose to be a fully compliant GP Connect solution"
---

## Introduction

GP Connect versions 1.x use the [FHIR STU3](http://hl7.org/fhir/STU3/) standard to specify the API and profiles.

## Profiling principles

> Please see the [Data model principles](designprinciples_data_model_principles.html) page for further information.

## Profiles for each capability pack

The profiled FHIR resources required for each of the GP Connect capability packs are specified within the specific specification sections for each of the capabilities:

* [Foundations](datalibraryfoundation.html)
* [Access Record HTML](accessrecord.html)
* [Access Record Structured](accessrecord_structured_development_resources_overview.html)
* [Appointment Management](datalibraryappointment.html)
* [Access Document](access_documents_development_resources_overview.html)

## General FHIR resource population requirements

### Population of optional elements

The purpose of GP Connect is to make the patient data stored within the GP systems available externally so that it can be used to help improve the quality of patient care across the NHS. To give patients the best care possible the data made available through the GP Connect API should be as complete as possible. Therefore, it is expected that both provider and consumers:

* ***SHALL*** populate all the elements within FHIR resources subject to any Capability-specific variance, where data is available within their system irrespective of the cardinality of the elements within the FHIR resource profiles.

As GP Connect has made the FHIR resources open to aid in interoperability this means that there are some elements included in FHIR profiles which are not applicable to our deployment settings, for example 'specialism' in the appointment resource. For these elements if the provider or consumer does not have data stored within their system the element will not be populated.

### Use of Must-Support flag

Some resource profiles used in GP Connect make use of the [Must-Support](https://www.hl7.org/fhir/STU3/conformance-rules.html#mustSupport) flag.

Where a Must-Support flag is present on a resource element, a `consumer` system SHALL populate the field in the request body if data is available to do so, irrespective of the fact that field cardinality may be `0..1` or `0..*`.

Similarly, `provider` systems SHALL populate an element in responses where data is available to do so, irrespective of optional cardinality. When a `provider` system receives data from a consumer for a field marked with the Must-Support flag, the provider system SHALL store this data field in such a way that the data element is preserved and the element can be populated in future responses to consumer requests for the resource in question.

If an element within a FHIR profile is marked as must support then all sub elements of that element SHALL also be considered must support. For example, within the GP Connect Appointment profile the booking organization extension is flagged with must support on the extension. This means that the extension and all sub elements within the extension are must support and SHALL be stored in a way that the data is preserved and the booking organization can be populated in future responses to consumers requesting that resource.

For example, see the [Register a patient request body](foundations_use_case_register_a_patient.html#payload-request-body).

## Resources not to be disclosed to a patient

There are occasions when information within a patient's record is not suitable or desirable to be disclosed to them. This might be for a temporary period of time such as test results that either should or must be disclosed by their primary healthcare professional before they can be discussed with the patient, or it might be information that could cause the patient psychological harm and the healthcare professional has deemed a risk to patient's emotional well-being should it be discussed with them.

Alongside information not suitable for patient disclosure there is another category of information, classified as sensitive and confidential. This is information that the primary healthcare professional has deemed to not be suitable for disclosure to other healthcare professionals. Currently, this information is only returned in a call made to the [migrate a patient's record](accessrecord_structured_development_migrate_patient_record) API when the parameter `includeSensitiveInformation` is set to `true`.
The inclusion of security labels does not change this behaviour i.e. if information was not going to be output previously due to sensitivity or confidentiality reasons, this should still be the case. And for information that was previously output this should continue to be output, just now it should be output according to the guidance below and with a security label, if appropriate.

Any resource, with the exception of [List](accessrecord_structured_development_migrate_patient_record), [Bundle](accessrecord_structured_development_bundle) and [Binary](access_documents_development_binary) that contains information that is not to be disclosed to the patient **MUST** be marked with the `NOPAT` [security label](http://hl7.org/fhir/stu3/resource.html#security-labels) within the [Resource Metadata](http://hl7.org/fhir/stu3/resource.html#Meta).
[NOPAT](http://hl7.org/fhir/stu3/v3/ActCode/cs.html#v3-ActCode-NOPAT) is a code within the [ActCode Code System](https://hl7.org/fhir/stu3/v3/ActCode/cs.html) and signifies the information should not be disclosed to the patient, family or caregivers.

The label should be applied to the [Meta.security](http://hl7.org/fhir/stu3/resource-definitions.html#Meta.security) element as follows:

```json
{
  "meta":{
    "security":[
      {
        "system":"http://hl7.org/fhir/v3/ActCode",
        "code":"NOPAT",
        "display":"no disclosure to patient, family or caregivers without attending provider's authorization"
      }
    ]
  }
}
```

For any resource carrying information that has been deemed to not be suitable to be disclosed to the patient:

* in a response to [retrieve a patient's record](accessrecord_structured_development_retrieve_patient_record):

  * Providers **MUST** include the `NOPAT` security label for all applicable resources
  * Consumers **MAY** utilise the information to display a message to the healthcare professional that the information is not to be disclosed to the patient

* in a response to [migrate a patient's record](accessrecord_structured_development_migrate_patient_record):

  * Providers **MUST** include the `NOPAT` security label for all applicable resources
  * Consumers **MUST** record the `NOPAT` security label against any resources as returned within the response from the Provider

It is anticipated additional labels will be introduced in the future and as such the existence of the label is not enough to consider the information is not suitable for patient disclosure, the security label must be for `NOPAT`.

### Documents not to be disclosed to a patient

There are two APIs available to retrieve a patient's documents, [retrieve a document](access_documents_development_retrieve_patient_documents) and [migrate a document](access_documents_development_migrate_patient_documents). Both APIs return a [Binary](access_documents_development_binary) resource that can not have security labels applied.
However, prior to calling either API a search is performed for the patient's documents, retrieve a document uses [search for a patient's documents](access_documents_development_search_patient_documents) and migrate a document uses [migrate a patient's record](accessrecord_structured_development_migrate_patient_record). Within the responses to these calls is a list of [DocumentReference](access_documents_development_documentreference)s that are able to have security labels applied. It is the `DocumentReference` resources which **MUST** contain the security labels indicating if they are not suitable to be disclosed to the patient.

Where applicable, Providers **MUST** ensure `DocumentReference`s contain the `NOPAT` security label and Consumers **MUST** honour and store this information for the documents in the search list.

## FHIR resource element/data type specific population requirements

### id

The logical id of all FHIR resources SHALL be populated in accordance with the [FHIR specification requirements](https://www.hl7.org/fhir/STU3/resource.html#id), meaning that population of the element is expected.

### Address

The `Address` data type is used in many of the FHIR resources across the GP Connect API. Where an element using the `Address` data type is present in a FHIR resource the following population guidance SHALL be followed:

* The address SHALL be populated using the elements:
  * `line`
    * E.g. House name, flat number, house number and street & village or locality.  Multiple `line` elements SHALL be populated, where more than one line is present.
  * `city`
  * `district`
    * This element is to carry county, where present.
  * `postalCode`
  * `country`
* Where an element is not present, the element SHALL NOT be populated.

* The `text` element SHOULD NOT be populated within the address.

* `use` SHALL be populated for patient or patient contact addresses and SHOULD be populated in other contexts.

Example:

```json
{
  "use": "home",
  "line": [
    "Trevelyan Square",
    "Boar Ln"
  ],
  "city": "Leeds",
  "district": "West Yorkshire",
  "postalCode": "LS1 6AE"
}
```

### ContactPoint

The `ContactPoint` data type is used in many of the FHIR resources across the GP Connect API. Where an element using the `ContactPoint` data type is present in a FHIR resource the following population guidance SHALL be followed:

* The telecom number or address (telephone number, email address etc) SHALL be populated in the `value` element
* `system` SHALL be populated in all circumstances
* `use` SHALL be populated for patient or patient contact telecom details and SHOULD be populated in other contexts.

Example:

```
{
  "system": "phone",
  "value": "01454587554",
  "use": "home"
}
```

### Patient.contact

The Patient.contact element SHALL be populated where demographic information is available in the Patient record for those individuals who may need to be contacted in connection with the Patient’s appointment.  In accordance with the FHIR definition, it is "Not applicable to register pedigree and family ties beyond use of having contact".

* `relationship.text` SHALL be populated with the type of relationship, for example *Emergency context*, *Next of kin*, or *Carer*.  The element SHALL also be used where a family relationship is recorded, for example *Daughter*.  Multiple relationship entries are allowed.
* `relationship.coding` SHALL NOT be populated
* `name`, `telecom`, `address`, `gender`, `organization` and `period` SHALL be populated where data is available
* `address` and `telecom` SHALL follow the [Address](development_fhir_resource_guidance.html#address) and [ContactPoint](development_fhir_resource_guidance.html#contactpoint) rules above for population of these elements

Example:

```
{
  "relationship": [
    {
      "text": "Emergency contact"
    },
    {
      "text": "Next of kin"
    },
    {
      "text": "Daughter"
    }
  ],
  "name": {
    "use": "official",
    "text": "JACKSON Jane (Miss)",
    "family": "Jackson",
    "given": [
      "Jane"
    ],
    "prefix": [
      "Miss"
    ]
  },
  "telecom": [
    {
      "system": "phone",
      "value": "07777123123",
      "use": "mobile"
    }
  ],
  "address": {
    "use": "home",
    "type": "physical",
    "line": [
      "Trevelyan Square",
      "Boar Ln"
    ],
    "city": "Leeds",
    "district": "West Yorkshire",
    "postalCode": "LS1 6AE"
  },
  "gender": "female"
}
```

### Bundle.entry.fullUrl

Providers SHOULD NOT populate `Bundle.entry.fullUrl`.

Consumers MUST NOT use `Bundle.entry.fullUrl`.
