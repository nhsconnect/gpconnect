---
title: Allergy Intolerance
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_allergies_guidance.html
summary: "Guidance for populating and reading the AllergyIntolerance resource"
---

## Guidelines

### Entries of allergy concepts as 'non-allergies' in source systems
Participating systems have a variety of record types/structures that explicitly represent Allergy and Intolerance structures within the patient record. These structures are explicitly selected by users to record Allergy and Intolerance information in the record or may be automatically triggered by attempts to enter allergy codes/concepts into the patient record. As these structures readily identify the presence of Allergy/Intolerance concepts in the record they are readily identifiable and mappable to the GP Connect AllergyIntolerance request when processing FHIR requests. 

It is also possible in some cases to bypass these data entry features and enter allergy codes/concepts as ordinary coded record entries in the patient record. Such entries may appear in the source system as journal entries and may not appear as Allergies/Intolerances in patient summaries or allergy lists in source systems.

*Where a record entry in a source system is not recognised by the source system as an Allergy/Intolerance it should not be represented as such in FHIR interactions*

### Allergy/Intolerance interoperability and clinical safety
It is recognised that Allergy/Intolerance information may not be fully interoperable between participating systems. Where Allergy/Intolerance information is not fully understood by a receiving system then it is the responsibility of the receiver to mitigate any risks arising and make related workflows as safe as possible. In other contexts, techniques such as prescribing prevention in the presence of non-understood (degraded) drug allergies have been employed. 

*Suppliers should seek appropriate clinical safety guidance when considering the implementation of use cases that involve Allergy/Intolerance interoperability.*

### Orthogonality to problem orientation
On some participating systems it is possible to manage Allergy/Intolerance information via problem orientation. This means, for example, making an Allergy/Intolerance record entry a problem heading with associated episodicities, priorities, linkage (to other record entries) and even start and end dates for the problem, independent of the Allergy/Intolerance record entry.

*The dual representation of an Allergy/Intolerance as a problem should not affect the representation of the Allergy/Intolerance via the FHIR resource*

### Unsupported qualifiers
It is possible on some participating systems to attach system specific qualifiers to Allergy/Intolerance record entries, for example a priority for the Allergy/Intolerance record entry or an episodicity. Similarly, some systems support richer sets of values for severity than are catered for via the criticality and reaction/severity elements. The certainty qualifiers that exist in participating systems are not supported. In all cases, the full set of qualifiers and values that are associated with an Allergy/Intolerance in the source system should be rendered as text (suitable formatted name/value pairs) and placed in the note element.

### Adoption of single notes field
Rather than split notes across a number of notes fields the AllergyIntolerance/note element is used as the single notes field to convey all qualifiers and user-entered text associated with the Allergy/Intolerance in a single place. Qualifiers and values should be appropriately labelled and formatted and where user notes have been entered against explicit fields such as Certainty then appropriate labels should be used.

### 'Ended' allergies and intolerances
On some systems it is possible to explicitly 'end' an Allergy and Intolerance such that it still appears in the patient record but is no longer active. For example, in the case of drug allergies that no longer interact with prescribing decision support. This inactivation may be achieved by explicit entry of an end date or a user action that alters the status of the Allergy and Intolerance. Allergies and Intolerances which have been explicitly ended should not accessible as AllergyIntolerance resources. That is, they should not be visible via Allergy and Intolerance lists to external systems.
The corollary is that these record entries should still be accessible as other resource types.

### Relationship to yellow card 
Allergy and Intolerance information may co-exist alongside system support for the capture of medication adverse reactions via the MHRA Yellow Card scheme. Suppliers should ensure that only information directly associated with the Allergy and Intolerance entry in the system is included in the AllergyIntolerance resource.

### AllergyIntolerance category
It is expected that it will always be possible to assign a category of medication for drug allergies or environmental for all other types of Allergy/Intolerance. Generally, the choice in a given system is explicit. In some cases, the type of Allergy/Intolerance may be more general - for example, a system type of 'Other' or equivalent. In such cases, if the Allergy/Intolerance entry interacts with prescribing decision support it should be assigned a category of medication, otherwise the category of 'environmental' should be used.

### Date usage
Where there is a single user alterable date associated with the Allergy/Intolerance on the original system, this is the onsetDateTime.
The assertedDate is explicitly the 'Date Record was believed accurate' and unless there is a user alterable date field on the source system that explicitly attests to the 'Date Record was believed accurate', then assertedDate is considered to be the audit trail datetime for the AllergyIntolerance - that is, when the record entry was made or modified and should be populated as such.

### Unsupported codes
In some of the participating systems, an additional code may be entered that represents the Allergy/Intolerance in addition to coding of the causative agent and reaction. These additional codes are not explicitly supported by the AllergyIntolerance resource. The unsupported allergy code should be encoded as a textual qualifier in the note element.

*The reasoning being that as systems converge on interoperable coding of Allergies and Intolerances via AllergyIntolerance/code the need for another code to represent the Allergy/Intolerance concept diminishes*

### Handling 'no known allergies'
Where there is an explicit assertion of the 'No Known Allergies' concept in the record (equivalent to SNOMED CT concept 716186003 and children) and there are otherwise no Allergy/Intolerance entries in the patient record, then systems may respond to queries for all AllergyIntolerance resources for the patient with an empty List containing an emptyReason code of 'nilKnown' with the term of the 'No Known Allergies' present expressed as text.

Where there are no Allergy/Intolerance entries in the patient record, but no explicit recording of the 'No Known Allergies' concept and equivalents, then systems should return an empty list with an emptyReason code of 'notasked' – that is, no assertion that the patient has 'No Known Allergies' has been made.

### Degradation actions to be performed by consumers not producers
Producer systems should not in principle limit potential interoperability by pre-emptively degrading coded information in export. It is a consumer responsibility to determine the understandability/processability of received resources and degrade if appropriate. This differs from the approach taken to AllergyIntolerance interoperability in other contexts such as GP2GP, where in some cases producer systems pre-emptively degraded certain types of Allergy/Intolerance on the basis that the concepts would never be generally interoperable.

### Reaction cardinality
The AllergyIntolerance/reaction element is optional, but where a severity is available in the source system it will be included to convey severity even if no reaction is explicitly available. If this is the case the reaction/manifestation should be coded as the nullFlavor NI.

By convention, only one resource should be expressed per allergy with only one manifestation per reaction.

