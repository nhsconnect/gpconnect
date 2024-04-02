---
title: FHIR&reg; resources overview
keywords: getcarerecord
tags: [design,structured]
sidebar: access_documents_sidebar
permalink: access_documents_development_resources_overview.html
summary: "List of FHIR&reg; resource profiles used in the Access Document capability"
---

## Resources used in Access Document ##

* [Bundle](access_documents_development_bundle.html)
* [DocumentReference](access_documents_development_documentreference.html)
* [Binary](access_documents_development_binary.html)
* Patient
* Practitioner
* PractitionerRole
* OperationOutcome

## Definitions of mandatory, required and optional

Throughout the profile pages within the specification we have a label for each data item named "Optionality", which details whether or not it has to be included in the resource. This item has 3 possible values:

1. Mandatory - if the data item **MUST** be recorded in the resource every time it is produced.
2. Required - if the system that is providing the data item contains this piece of data then it **MUST** include it in the resource.
3. Optional - the system has the option to include this data if it is available.
