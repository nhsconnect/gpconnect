---
title: Open API design principles
keywords: development
tags: [development,fhir]
sidebar: overview_sidebar
toc: false
permalink: designprinciples_open_api_principles.html
summary: "High-level design principles related to the open API design"
---

GP Connect has aligned with [NHS England's Open API Policy](https://www.england.nhs.uk/digitaltechnology/info-revolution/interoperability/open-api/) to support the ambition of moving to a position where significant business functionality available within systems is exposed through interfaces where the definition is open. [Download a PDF copy](https://www.england.nhs.uk/wp-content/uploads/2014/05/open-api-policy.pdf).

{% include important.html content="GP Connect has adopted the [FHIR&reg; standard (STU3)](https://www.hl7.org/fhir/STU3/) and as such the FHIR API design principles will be followed unless a clear rationale exists to amend. When an amendment is required this decision will be logged and the rationale clearly communicated." %}

## Core API design principles for GP Connect ##

- FHIR API providers to provide a [capability statement](https://www.hl7.org/fhir/STU3/capabilitystatement.html){:target="_blank"} resource for the server
- [FHIR RESTful API](https://www.hl7.org/fhir/STU3/http.html){:target="_blank"} principles to be used by default
  - Synchronous endpoints using `GET`, `POST`, `PUT` and `DELETE` HTTP verbs
- [FHIR operation](https://www.hl7.org/fhir/STU3/operations.html){:target="_blank"} APIs to be used in limited 'set piece' circumstances - for example, to pull bundles of resources without using the full generic querying syntax
- Uniform resource identification (URI) as the resource's [logical identity](https://www.hl7.org/fhir/STU3/resource.html#id){:target="_blank"}
- Business identifiers (such as NHS number) used to resolve a resource's [logical identity](https://www.hl7.org/fhir/STU3/resource.html#id){:target="_blank"}
- Resources represented as either [XML or JSON](https://www.hl7.org/fhir/STU3/formats.html#wire){:target="_blank"} as requested by the API consumer.  To ensure maximum accessibility, GP Connect is expecting producers to support both formats.  However, since XML is on average 30% larger on the wire there is a preference towards use of JSON. 
- HTML content to utilise XHTML in line with the [FHIR narrative](https://www.hl7.org/fhir/STU3/narrative.html){:target="_blank"} guidance
- ETags for [managing version-aware updates](https://www.hl7.org/fhir/STU3/http.html#concurrency){:target="_blank"}
