---
title: Data model principles
keywords: development, fhir, logical models
tags: [development,fhir]
sidebar: overview_sidebar
permalink: designprinciples_data_model_principles.html
summary: "High-level design principles related to the FHIR data modelling aspects of the system."
---

{% include important.html content="GP Connect has adopted the FHIR&reg; standard (DSTU2) and as such the standard FHIR resources will be used unless a clear rationale exists to amend. When an amendment is required this decision will be logged and the rationale clearly communicated (as a resource delta)." %}

- Data model assets to be held on [Github](https://github.com/nhsconnect/gpconnect-fhir){:target="_blank"}.
- Data models to be licensed under the [Apache 2 License](http://www.apache.org/licenses/LICENSE-2.0){:target="_blank"}.
- Code repositories will use the [Gitflow](http://nvie.com/posts/a-successful-git-branching-model/){:target="_blank"} branching model.
- A [Data Library](https://github.com/nhsconnect/gpconnect-fhir){:target="_blank"} Git repository will hold shared/common resources.
- FHIR resources will carry the major version in the name (e.g. gpconnect-patient-1) and major/minor version within StructureDefinition/Conformance.
- Profiling tools (i.e. [Furore Forge](http://fhir.furore.com/Forge){:target="_blank"}) will be used to create FHIR StructureDefinitions and ValueSets.

## Profiling ##

It is common for the base FHIR&reg; standard to require further adaptation to a particular context of use.

[Profiling](https://www.hl7.org/fhir/DSTU2/profiling.html){:target="_blank"} is a general term which describes the process of adapting the base standard for use in a specific context. 
<br/>Typically, the profiling process both restricts and extends APIs, resources and terminologies.
 