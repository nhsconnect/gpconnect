---
title: Allergies guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_allergies_guidance.html
summary: "Guidance on the representation of allergies and intolerances in GP Connect"
---

## Introduction ##

The recording of allergy and intolerance information in patient records is a major component of communicating the effects of external substances and compounds on patient health.

The allergy and intolerance concept is broad and multidimensional:

* the causation of allergy and intolerance may be linked to specific medications or pharmaceuticals or substances (biological or chemical) in the environment
* the weight and significance that may be attached to recorded allergy and intolerance is affected by a number of factors including the certainty of the allergy, the severity of the reaction and the likelihood of occurrence
* allergies and intolerances may be linked to other clinical events, such as diagnostic tests that confirm the presence of the allergy or linked to instances of illness caused by the allergy
* allergies and intolerances may be dynamic and evolving, increasing in severity over time, recurrent or perhaps only active and observed within defined periods

The recording and handling of allergy and intolerance information has an important role to play in patient safety, not only with regard to clinical decision making, but also in the realm of prescribing decision support, where the presence of allergy information linked to causative agents can trigger automated alerts and restrictions when prescribing.

Given the complexity and depth of the allergy and intolerance domain there are significant differences and variations in the implementation of the allergy and intolerance concept across participating systems in terms of structure, terminology and the linkages between terminology and decision support. These differences limit the current interoperability of allergies and intolerances.

The GP Connect `AllergyIntolerance` FHIR&reg; resource aims to improve the interoperability of allergies and intolerances through convergence towards a standardised structure and common terminology.

The clinical importance of allergy and intolerance information coupled with the variability of implementations across participating systems means that there is a need for clear guidance on the utilisation of the GP Connect `AllergyIntolerance` resource by both providers and consumers.

These pages provide the required guidance:

* usage of the FHIR resource elements to represent allergy and intolerance concepts from participating systems
* guidance for providers on the correct representation of allergy/intolerance concepts as FHIR resources
* guidance for consumers on the handling of the FHIR resources in terms of expectations for what can be present in the resource and the handling of variations between systems

## Roadmap and vision ##

The `AllergyIntolerance` FHIR resource has been developed to address current allergy and intolerance interoperability limitations. As such, it has been designed to enable a future state in which greater levels of allergy and intolerance interoperability are achieved by utilisation of SNOMED CT and NHS dictionary of medicines and devices (dm+d) concepts from the specified allergy and intolerance subset. 

The FHIR structure and standard is only an enabler for greater drug allergy interoperability. Drug allergy interoperability is only achieved when drug allergy concepts are understood by receiving systems - that is, they trigger equivalent prescribing decision support. Therefore, the benefits will not be achieved without participating systems being able to consistently process codes from the defined causative agent subset as concepts capable of triggering prescribing decision support in receiving systems. 

The system change to converge the coding of causative agents to the specified subset and make the causative agent subset consistently processable (by prescribing decision support modules across participating systems) falls outside the scope of this guidance.

In the interim state it is expected that with the gradual adoption of the FHIR resource and associated terminologies, drug allergy interoperability will continue to be partial. 

The `AllergyIntolerance` resource adopts common approaches for expressing certainty and severity, increasing interoperability of qualifiers associated with allergies and intolerances. 

Greater expressivity around dates (end dates, onset, occurrence) is also supported.

It is recognised that current support for the full range of severity qualifiers is limited and variable across systems, and existing support for the full range of date concepts will also be limited.

It is also recognised that there will be interim challenges in mapping existing allergy and intolerance record structures to the `AllergyIntolerance` resource. In some systems, allergy and intolerance information may be a post-coordinated triple of allergy code, reaction/manifestation code and causative agent code. In other systems, a single pre-coordinated code serves to describe the allergy/intolerance concept and the causative agent. In the former case, the `AllergyIntolerance` resource may not fully support the three coded concepts and in the latter case, there is currently no distinct identification of causative agent and reaction/manifestation.

## Entries of allergy concepts as 'non-allergies' in source systems
Participating systems have a variety of record types/structures that explicitly represent allergy and intolerance structures within the patient record. These structures are explicitly selected by users to record allergy and intolerance information in the record or may be automatically triggered by attempts to enter allergy codes/concepts into the patient record. As these structures readily identify the presence of allergy/intolerance concepts in the record, they are readily identifiable and mappable to the `AllergyIntolerance` request when processing FHIR requests. 

It is also possible in some cases to bypass these data entry features and enter allergy codes/concepts as ordinary coded record entries in the patient record. Such entries may appear in the source system as ordinary journal entries and may not appear as allergies/intolerances in patient summaries or allergy/intolerance lists in provider systems. 

*If it is possible on the provider system to record allergy concepts as non-allergies in the patient record, then the system **MUST** express these record entries as FHIR AllergyIntolerance resources when queried.*

## Allergy/intolerance interoperability and clinical safety
It is recognised that allergy/intolerance information may not be fully interoperable between participating systems. Where allergy/intolerance information is not fully understood by a receiving system then it is the responsibility of the receiver to mitigate any risks arising and make related workflows as safe as possible. 

Where allergy/intolerance information is integrated into the consuming system patient record then allergy/intolerance information **MUST** be degraded where the coded allergy/intolerance information is not fully understood by the consumer. In the context of drug allergies, an allergy/intolerance is only understood if the coded causative agent triggers equivalent prescribing decision support to that triggered on the producing system.

Degradation can be handled by coding the record entries resulting from the processed allergy as (`196461000000101`, Transfer-degraded drug allergy) and preserving the original term for the received code as text.

Where the processing of drug allergy `AllergyIntolerance` resources results in degradation or the FHIR resource being processed is already coded as a degrade drug allergy code (`196461000000101`, Transfer-degraded drug allergy) then the consuming system **MUST** prevent prescribing while degraded drug allergies are present in the patient record and inform users attempting prescribing actions that prescribing is prevented due to the presence of degraded drug allergies.

In other contexts, task-based workflows have been utilised to assist users on consuming systems to process degraded drug allergies by re-coding them to concepts understood by the consuming system.

*When considering the implementation of use cases involving allergy/intolerance interoperability suppliers **MUST** perform an appropriate clinical safety assessment and obtain the necessary clinical safety approvals for the processing performed by their system.*

## Orthogonality to problem orientation
On some participating systems it is possible to manage allergy/intolerance information via problem orientation. This means, for example, making an allergy/intolerance record entry a problem heading with associated episodicities, priorities, linkage (to other record entries) and even start and end dates for the problem, independent of the allergy/intolerance record entry.

*The dual representation of an allergy/intolerance as a problem **MUST NOT** affect the representation of the allergy/intolerance via the FHIR resource.*

## Unsupported qualifiers
It is possible on some participating systems to attach system specific qualifiers to allergy or intolerance record entries, for example a priority for the allergy/intolerance record entry or an episodicity. Similarly, some systems support richer sets of values for severity than are catered for via the criticality and reaction/severity elements. The certainty qualifiers that exist in participating systems are not supported. In all cases, the full set of qualifiers and values that are associated with an allergy/intolerance in the source system **MUST** be rendered as text (suitable formatted name/value pairs) and placed in the `AllergyIntolerance.note` element.

## Adoption of single notes field
Rather than split descriptive and user entered text across a number of notes fields the `AllergyIntolerance.note` element is used as the single notes field to convey all qualifiers and user-entered text associated with the allergy or intolerance in a single place. Qualifiers and values expressed as text **MUST** be appropriately labelled and formatted and where user notes have been entered against explicit fields such as certainty then appropriate labels **MUST** be used.

## 'Resolved' allergies and intolerances
On some systems it is possible to explicitly mark an allergy or intolerance as resolved or ended, such that it still appears in the patient record but is no longer active and no longer interacts with prescribing decision support. This inactivation may be achieved by explicit entry of an end date or a user action that alters the status of the allergy or intolerance.

Allergies and intolerances which have been explicitly resolved **MUST** only be returned in response to resource queries which have the *includeResolvedAllergies* parameter set to true (see [Retrieve a patient’s structured record](accessrecord_structured_development_retrieve_patient_record.html)).

When the provider is sending resolved allergies, it **MUST** send them in a separate `List` to the active allergies as contained resources in that `List`. The `List` **MUST** have the title 'Ended allergies' and resolved allergy resources **MUST** be assigned a `clinicalStatus` of `resolved`. A title of 'Allergies and adverse reactions' **MUST** be used for the `List` containing the active `AllergyIntolerance` resources.

Consuming systems **MUST** ensure that resolved allergies are not treated as active - that is, they **MUST NOT** interact with prescribing decision support or be misinterpreted by users as being active.

Where the consuming system does not natively support a resolved allergy concept, suppliers **MUST** seek appropriate clinical safety advice on the handling of the resolved allergy concept.

## Relationship to yellow card 
Allergy and intolerance information may co-exist alongside system support for the capture of medication adverse reactions via the MHRA Yellow Card scheme. Suppliers **MUST** ensure that only information directly associated with the allergy and intolerance entry in the system is included in the `AllergyIntolerance` resource and not data only associated with the MHRA yellow card dataset. 

## AllergyIntolerance category
It is expected that it will always be possible to assign a category of 'medication' for drug allergies or 'environment' for all other types of allergy/intolerance. Generally, the choice in a given system is explicit. In some cases, the type of allergy or intolerance may be more general - for example, a system designated type of 'Other' or equivalent. In such cases, if the allergy or intolerance entry interacts with prescribing decision support it **MUST** be assigned a `category` of `medication`. Otherwise, the category of `environment` **MUST** be used.

## Date usage
The `AllergyIntolerance` resource supports a rich set of date concepts. However, there is currently limited support for additional date concepts via the allergy record structures in producing systems. 

The asserted date is when the allergy related to the patient was asserted. In many cases, this will be when the allergy is entered on to the system, although systems may allow this date to be modified by the user.

If a producing system, currently or at a future point supports allergy date concepts that explicitly capture onset dates and last occurrence dates, then the `onsetDateTime` and `lastOccurrence` elements of `AllergyIntolerance` may be populated.

## Unsupported codes
In some of the participating systems, an additional coded concept may be entered that represents the allergy or intolerance in addition to coding of the causative agent and reaction. These additional codes are not explicitly supported by the `AllergyIntolerance` resource. The unsupported allergy code **MUST** be encoded as a textual qualifier in the note element.

*The reasoning being that as systems converge on interoperable coding of allergies and intolerances via AllergyIntolerance/code the need for another code to represent the allergy/intolerance concept diminishes.*

## Negation - handling 'no known allergies'
Where there is an explicit assertion of the 'No Known Allergies' concept in the record, equivalent to SNOMED CT concept `716186003` and children, and there are otherwise no allergy or intolerance entries in the patient record, then systems may respond to queries for all allergy or intolerance resources using and `AllergyIntolerance` resource containing the appropriate code. 

Where there are no allergy or intolerance entries in the patient record, but no explicit recording of the ‘No Known Allergies’ concept and equivalents, then systems **MUST** return an empty `List` with an emptyReason FHIR code: "No content recorded" and a `List.note` with the text: 

> Information not available.

Because resolved allergies are queried via the `includeResolvedAllergies` query parameter and resolved allergies are conveyed via a separate `List`, assertions of 'No known allergies' are true only in the context of a given list. Therefore, an empty 'Active Allergies' `List` only asserts that there are no active allergies and "No content recorded" in the context of the active allergies `List` asserts that there are no active allergies to contradict the recorded 'No Known Allergies' code. Similarly, where the `includeResolvedAllergies` flag is present an empty 'Resolved Allergies' `List` asserts the absence of resolved allergies and "No content recorded" asserts that the coding of 'No Known Allergies' is not contradicted by the presence of resolved allergies. Only the inclusion of the `includedResolvedAllergies` flag and emptiness of both lists can fully assert that there are no allergies (active or resolved) in the source record.

In most use cases consuming systems are only interested in active allergies, but the solution supports the retrieval of resolved allergies where this is required.

## Degradation actions to be performed by consumers not providers
Provider systems **MUST NOT** in principle limit potential interoperability by pre-emptively degrading coded information in export. It is a consumer responsibility to determine the understandability/processability of received resources and degrade if appropriate. In the case of drug allergies, understandability is determined by the consuming system being able to trigger equivalent prescribing decision support as the source system in response to the causative agent code.

It is expected that initial GP Connect provider implementations will reflect the current state of provider systems prior to full convergence on the specified causative agent subset and at this point causative agents may be coded using legacy terminologies/code systems or contain codes in supported terminologies that lie outside the hierarchies specified by the causative agent subset.

## Reaction cardinality
The `AllergyIntolerance.reaction` is optional, but where a severity is available in the source system it will be included to convey severity even if no other reaction details are explicitly available. If this is the case the `AllergyIntolerance.reaction.manifestation` **MUST** be coded as the `nullFlavor` NI.

By convention, only one reaction **MUST** be expressed per allergy with only one manifestation per reaction.



