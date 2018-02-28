---
title: Allergy Intolerance
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_allergies_introduction.html
summary: "Guidance for populating and reading the AllergyIntolerance resource"
---

## Guidance for producers and consumers of the AllergyIntolerance  FHIR&reg; profile

The recording of Allergy and Intolerance information in patient records is a major component of communicating the effects of external substances/compounds on patient health.

The Allergy and Intolerance concept is broad and multidimensional.
* the causation of Allergy and Intolerance may be linked to specific medications or pharmaceuticals or substances (biological or chemical) in the environment
* the weight and significance that may be attached to recorded Allergy and Intolerance is affected by a number of factors including the certainty of the allergy, the severity of the reaction and the likelihood of occurrence
* Allergies and Intolerances may be linked to other clinical events, such as diagnostic tests that confirm the presence of the allergy or linked to instances of illness caused by the allergy
* Allergies and Intolerances may be dynamic and evolving, increasing in severity over time, recurrent or perhaps only active and observed within defined periods

The recording and handling of Allergy and Intolerance information has an important role to play in patient safety, not only with regard to clinical decision making but also in the realm of prescribing decision support, where the presence of allergy information linked to causative agents can trigger automated alerts and restrictions when prescribing.

Given the complexity and depth of the Allergy and Intolerance domain there are significant differences and variations in the implementation of the Allergy and Intolerance concept across GP Systems in terms of structure and terminology. These differences limit the current interoperability of Allergies and Intolerances.

The GP Connect AllergyIntolerance FHIR resource aims to improve the interoperability of Allergies and Intolerances through a standardised structure and common terminology.

The clinical importance of Allergy and Intolerance information coupled with the variability of implementations across participating systems means that there is a need for clear guidance on the utilisation of the GP Connect AllergyIntolerance resource by both producers and consumers.

This page provides the required guidance:
* usage of the FHIR resource elements to represent Allergy and Intolerance concepts from participating systems
* guidance for producers on the correct representation of Allergy/Intolerance concepts as FHIR resources
* guidance for consumers on the handling of the FHIR resources in terms of expectations for what can be present in the resource and the handling of variations between systems


# Roadmap and vision
The Allergy and Intolerance FHIR resource has been developed to address current Allergy and Intolerance interoperability limitations. As such it has been designed to enable a future state in which greater levels of Allergy and Intolerance interoperability are achieved by utilisation of SNOMED CT concepts from a curated Allergy and Intolerance list to describe causative agents in an interoperable manner. Interoperability of the codes describing causative agents coupled with linkage of the codes to prescribing decision support in receiving systems should improve the end to end interoperability of Allergy and Intolerance concepts. In the current state causative agents are described via a variety of mechanisms (DM+D, supplier specific terminologies), which limits interoperability.

In the interim state it is expected that with the gradual adoption of the FHIR resource and associated terminologies, interoperability will continue to be partial, improving over time as adoption of the common terminology for describing causative agents increases. In the early stages of adoption, causative agents may for example continue to be described with existing terminologies and approaches.

In addition to support for improved interoperability, the AllergyIntolerance resource adopts common approaches for expressing certainty and severity, increasing interoperability of qualifiers associated with Allergies and Intolerances. 

Greater expressivity around dates (end dates, onset, occurrence) is also supported.

It is recognised that current support for the full range of certainty/severity qualifiers is limited across systems and support for the full range of date concepts will also be limited.

It is also recognised that there will be interim challenges in mapping existing Allergy and Intolerance record structures to the AllergyIntolerance resource. In some systems, Allergy and Intolerance information may be a post-coordinated tuple of allergy code, reaction/manifestation code and causative agent code. In other systems, a single pre-coordinated code serves to describe the Allergy/Intolerance concept and the causative agent. In the former case, the AllergyIntolerance resource may not fully support the three coded concepts and in the latter case, there is currently no separate identification of causative agent and reaction/manifestation.

