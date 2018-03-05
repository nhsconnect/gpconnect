---
title: Allergy Intolerance
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_allergies_introduction.html
summary: "Guidance for populating and reading the AllergyIntolerance resource"
---
## Guidance for providers and consumers of the AllergyIntolerance  FHIR&reg; profile

The recording of Allergy and Intolerance information in patient records is a major component of communicating the effects of external substances/compounds on patient health.

The Allergy and Intolerance concept is broad and multidimensional.
* the causation of Allergy and Intolerance may be linked to specific medications or pharmaceuticals or substances (biological or chemical) in the environment
* the weight and significance that may be attached to recorded Allergy and Intolerance is affected by a number of factors including the certainty of the allergy, the severity of the reaction and the likelihood of occurrence
* Allergies and Intolerances may be linked to other clinical events, such as diagnostic tests that confirm the presence of the allergy or linked to instances of illness caused by the allergy
* Allergies and Intolerances may be dynamic and evolving, increasing in severity over time, recurrent or perhaps only active and observed within defined periods

The recording and handling of Allergy and Intolerance information has an important role to play in patient safety, not only with regard to clinical decision making but also in the realm of prescribing decision support, where the presence of allergy information linked to causative agents can trigger automated alerts and restrictions when prescribing.

Given the complexity and depth of the Allergy and Intolerance domain there are significant differences and variations in the implementation of the Allergy and Intolerance concept across participating systems in terms of structure, terminology and the linkages between terminology and decision support. These differences limit the current interoperability of Allergies and Intolerances.

The GP Connect AllergyIntolerance FHIR resource aims to improve the interoperability of Allergies and Intolerances through convergence towards a standardised structure and common terminology.

The clinical importance of Allergy and Intolerance information coupled with the variability of implementations across participating systems means that there is a need for clear guidance on the utilisation of the GP Connect AllergyIntolerance resource by both providers and consumers.

This page provides the required guidance:
* usage of the FHIR resource elements to represent Allergy and Intolerance concepts from participating systems
* guidance for providers on the correct representation of Allergy/Intolerance concepts as FHIR resources
* guidance for consumers on the handling of the FHIR resources in terms of expectations for what can be present in the resource and the handling of variations between systems

# Roadmap and vision
The Allergy and Intolerance FHIR resource has been developed to address current Allergy and Intolerance interoperability limitations. As such it has been designed to enable a future state in which greater levels of Allergy and Intolerance interoperability are achieved by utilisation of SNOMED CT and DM+D concepts from the specified Allergy and Intolerance subset. 

The FHIR structure and standard is only an enabler for greater drug allergy interoperability. Drug allergy interoperability is only achieved when drug allergy concepts are understood by receiving systems i.e. trigger equivalent prescribing decision support. Therefore the benefits will not be achieved without participating systems being able to consistently process codes from the defined causative agent subset as concepts capable of triggering prescribing decision support in receiving systems. 

The system change to converge the coding of causative agents to the specified subset and also make the causative agent subset consistently processable by prescribing decision support modules across participating systems falls outside the current scope of this guidance document.

In the interim state it is expected that with the gradual adoption of the FHIR resource and associated terminologies, drug allergy interoperability will continue to be partial. 

The AllergyIntolerance resource adopts common approaches for expressing certainty and severity, increasing interoperability of qualifiers associated with Allergies and Intolerances. 

Greater expressivity around dates (end dates, onset, occurrence) is also supported.

It is recognised that current support for the full range of severity qualifiers is limited and variable across systems and existing support for the full range of date concepts will also be limited.

It is also recognised that there will be interim challenges in mapping existing Allergy and Intolerance record structures to the AllergyIntolerance resource. In some systems, Allergy and Intolerance information may be a post-coordinated triple of allergy code, reaction/manifestation code and causative agent code. In other systems, a single pre-coordinated code serves to describe the Allergy/Intolerance concept and the causative agent. In the former case, the AllergyIntolerance resource may not fully support the three coded concepts and in the latter case, there is currently no distinct identification of causative agent and reaction/manifestation.


