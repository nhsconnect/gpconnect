---
title: Open API design principles
keywords: development
tags: [development,fhir]
sidebar: overview_sidebar
permalink: designprinciples_open_api_principles.html
summary: "High-level design principles related to the Open API design"
---

{% include tip.html content="GP Connect has aligned with [NHS England's Open API Policy](https://www.england.nhs.uk/digitaltechnology/info-revolution/interoperability/open-api/) to support the ambition of moving to a position where significant business functionality available within systems is exposed through interfaces where the definition is open." %}

{% include important.html content="GP Connect has adopted the [FHIR&reg; standard (DSTU2)](https://www.hl7.org/fhir/DSTU2/) and as such the FHIR API design principles will be followed unless a clear rationale exists to amend. When an amendment is required this decision will be logged and the rationale clearly communicated." %}

- FHIR API providers to provide a [Conformance](https://www.hl7.org/fhir/DSTU2/conformance.html){:target="_blank"} resource for the server
- [FHIR RESTful API](https://www.hl7.org/fhir/DSTU2/http.html){:target="_blank"} principles to be used by default
  - synchronous endpoints using `GET`, `POST`, `PUT` and `DELETE` HTTP verbs
- [FHIR Operation](https://www.hl7.org/fhir/DSTU2/operations.html){:target="_blank"} APIs to be used in limited "set piece" circumstances
  - for example, to pull bundles of resources without using the full generic querying syntax
- Uniform Resource Identification (URI) as the resource's [Logical Identity](https://www.hl7.org/fhir/DSTU2/resource.html#id){:target="_blank"}
- business identifiers (such as NHS Number) used to resolve a resource's [Logical Identity](https://www.hl7.org/fhir/DSTU2/resource.html#id){:target="_blank"}
- resources represented as either [XML or JSON](https://www.hl7.org/fhir/DSTU2/formats.html#wire){:target="_blank"} as requested by the API consumer.  To ensure maximum accessibility, GP Connect is expecting producers to support both formats.  However since XML is on average 30% larger on the wire there is a preference towards use of JSON. 
- HTML content to utilise XHTML in line with the [FHIR Narrative](https://www.hl7.org/fhir/DSTU2/narrative.html){:target="_blank"} guidance
- eTags for [managing version aware updates](https://www.hl7.org/fhir/DSTU2/http.html#concurrency){:target="_blank"}
