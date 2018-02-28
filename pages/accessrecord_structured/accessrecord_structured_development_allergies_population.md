---
title: Allergy Intolerance
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_allergies_population.html
summary: "Guidance for populating and reading the AllergyIntolerance resource"
---

# AllergyIntolerance resource definition
This guidance should be read in conjunction with the underlying resource definition. (TO DO: Check URL matches correct published StructureDef) [AllergyIntolerance](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1)

# Common and base element handling
Guidance for the general handling of common and base elements in GP Connect resources can be found [here - link required]()

# Element usage

| Element  |Usage |Datatype   |Optionality|Guidance 
|---|---|---|---|---
|Allergy End Date|TO DO: Confirm removal in latest StructureDefinition and remove|
|Probability of Recurrence|TO DO: Confirm removal in latest StructureDefinition and remove|
|Evidence|Reference to confirmatory diagnostic report e.g. pathology RAST test result|Extension (valueReference)|O||
|clinicalStatus|Fixed value 'active' if present|Code|O|||
|verificationStatus|Fixed value of 'unconfirmed' TO DO - ensure certainty extension in reaction element is not in published StructureDefinition|Code|M|||
|type|Set to 'allergy' for reactions which are allergenic in nature (immunological), a value of 'intolerance may be used to indicate Adverse Reactions (not immunologic in nature). Where the type is unknown the type element may be omitted. |Code|O|Some systems allow explicit identification of Adverse Reactions and Intolerances and the type should be used to make this distinction where it exists||
|category|Use 'medication' for all drug allergy types, 'environmental' for all non-drug allergies. The other values in the ValueSet (food and biologic) should not be used by convention.|Code|M|See note on 'AllergyIntolerance Category' TO DO - confirm restriction of vocabulary and optionality.
|criticality|Distinguishes between life threatening (high) and non-life-threatening (low) potential as well as unable-to-assess. May be used in addition to severity within the reaction element to express severity e.g. systems that support a severity of life threatening may set to high|Code|O|May be used in conjunction with reaction/severity by systems which support a severity of 'Life Threatening' or equivalent
|code|The causative agent such as food, drug or substances that has caused or may cause an allergy, intolerance or adverse reaction in this patient.|CodeableConcept|M|Systems will evolve to use the specified vocabulary of interoperable SNOMED CT concepts. In the interim this coded element will hold the primary code for the AllergyIntolerance which may in the case of drug allergies be a medication code or a pre-coordinated code which triggers decision support on the system. TO DO: confirm ValueSet will be referenced by published StructureDefinition. Where the AllergyIntolerance has no coded representation in the source system but is identified as such in the source record then the appropriate degrade code may be used and the text of the AllergyIntolerance placed in the text element of the CodeableConcept.
|onset[dateTime]|Date when allergy/intolerance first manifested. Restricted to values of dateTime. |dateTime|O|Is the user modifiable date or datetime associated with the Allergy/Intolerance entry on the original system. May be unknown on source system and if so omitted (TO DO: or make it mandatory and use nullFlavor UNK for date?)
|assertedDate|The 'Date Record was believed accurate'. Unless the system has an explicit user alterable datetime that represents the 'Date record was believed to be accurate' then this is the audit trail datetime of when the record entry was 1st made or modified|dateTime|M|Mandatory element as audit trail datetime will always be available
|lastOccurrence|Represents the date and/or time of the last known occurrence of a reaction event|dateTime|O|May not currently be available from participating systems and may be omitted. Ommission should not prejudice the ability of suppliers to include this element if and when it is available.
|note|All text associated with the AllergyIntolerance including user entered notes and qualifiers is grouped together and expressed in this field. Ensures mapped coded values are not lost|Annotation|O|
|reaction/note|NOT TO BE USED. AllergyIntolerance/note should contain all the consolidate text from the Allergy/Intolerance|Annotation|O||
|reaction/manifestation|Conveys the reaction resulting from the Allergy/Intolerance as a code. Where no code is available, but a textual description of the reaction is available then the nullFlavor UNC may be used and the textual description conveyed via reaction.description. If no reaction has explicitly been recorded but the reaction element is present to convey severity, then reaction/manifestation should be coded as the nullFlavor NI. If the patient has been asked but is unable to specify a reaction the nullFlavor 'ASKU' should be used |CodeableConcept|O|
|reaction/description|Conveys the textual description of the manifestation where no code is available|String|O|A receiving system may concatenate the contents (appropriately labelled) with text in AllergyIntolerance/note if a textual description of the manifestation is not supported in the receiving system record structure|
|reaction/severity|Severities of mild, moderate, severe are mapped directly to FHIR ValueSet. Map life threatening to severe and populate criticality with high. |Code|O|Unmapped severity codes in original system should be expressed in AllergyIntolerance/note|
|reaction/exposureRoute|The route by which exposure to the substance causing the reaction occurred. Utilise the DM+D route codes|CodeableConcept|O|
|reaction/onset[x]|NOT TO BE USED|Choice|O|Onset explicitly supplied via AllergyIntolerance/onset[dateTime]|
|reaction/substance|NOT TO BE USED|CodeableConcept|O|The causative is explicitly and specifically coded via AllergyIntolerance/code|
