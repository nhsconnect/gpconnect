---
title: Resource guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_resource_guidance.html
summary: "Where to find details of what resources and operations a FHIR server should expose to be a fully compliant GP Connect solution"
---

GP Connect has specified profiled versions of the international [FHIR Resources](https://www.hl7.org/fhir/STU3/){:target="_blank"}, tailoring them to meet the requirements of the GP Connect use cases and to aid in interoperability between systems.

The profiled FHIR resources required for each of the GP Connect capability packs are specified within the specific specification sections for each of the capabilities:

* [Foundations](datalibraryfoundation.html)
* [Access Record HTML](accessrecord.html)
* [Access Record Structured](accessrecord_structured_development_resources_overview.html)
* [Appointment Management](datalibraryappointment.html)
* [Task Management](tasks.html)


## General FHIR resource element guidance

### Address

The `address` element exists in many of the FHIR resources used in the GP Connect API. Where an address element is present in a FHIR resource the following population guidance SHALL be followed:

* Where the individual address sub elements are availabe within the suppliers system, the address SHALL be populated using the elements:
  * line
  * city
  * district
  * postalCode
  * country
  
  The `text` element SHOULD not be populated within the address.
  
* Where the address is not store as the individual elements within the suppliers system, the address SHALL be populated using the `text` element. The `line`, `city`, `district`, `postalCode` and `country` SHALL not be populated.
