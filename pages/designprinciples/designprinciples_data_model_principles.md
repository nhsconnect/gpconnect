---
title: Data model principles
keywords: development, fhir, logical models
tags: [development,fhir]
sidebar: overview_sidebar
toc: false
permalink: designprinciples_data_model_principles.html
summary: "High-level design principles related to the FHIR data modelling aspects of the system"
---

{% include important.html content="GP Connect has adopted the FHIR&reg; standard (STU3) and as such the standard FHIR resources will be used unless a clear rationale exists to amend. When an amendment is required this decision will be logged and the rationale clearly communicated." %}

## GP Connect Data Models ##

- data model assets to be held on [GitHub](https://github.com/nhsconnect/gpconnect-fhir){:target="_blank"}
- data models to be licensed under the [Apache 2 license](http://www.apache.org/licenses/LICENSE-2.0){:target="_blank"}
- code repositories will use the [GitFlow](http://nvie.com/posts/a-successful-git-branching-model/){:target="_blank"} branching model
- a [data library](https://github.com/nhsconnect/gpconnect-fhir){:target="_blank"} Git repository will hold shared/common resources
- FHIR resources will carry the major version in the name (for example, gpconnect-patient-1) and major/minor version within StructureDefinition/Conformance.
- profiling tools (for example, [Furore Forge](http://fhir.furore.com/Forge){:target="_blank"}) will be used to create FHIR StructureDefinitions and ValueSets.

## Profiling ##

It is common for the base FHIR&reg; standard to require further adaptation to a particular context of use.

[Profiling](https://www.hl7.org/fhir/STU3/profiling.html){:target="_blank"} is a general term that describes the process of adapting the base standard for use in a specific context. Typically, the profiling process both restricts and extends APIs, resources and terminologies.
 
