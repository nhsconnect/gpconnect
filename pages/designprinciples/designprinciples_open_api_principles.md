---
title: API design principles
keywords: development
tags: [development,fhir]
sidebar: overview_sidebar
toc: false
permalink: designprinciples_open_api_principles.html
summary: "High-level design principles related to the API design"
---

## Open API

GP Connect has aligned with [NHS England's Open API Policy](open-api-policy.pdf) to support the ambition of moving to a position where significant business functionality, available within systems, is exposed through interfaces where the definition is open.

## Architectural design principles

GP Connect has a number of architectural design principles, some of which have developed based on interaction with the suppliers, others are based on an understanding of the technological maturity of the NHS at the present time and the other principles are based on good practice and a vision for the future of the NHS.


### GP Connect API implemented at an organization level

The GP Connect API has been designed and developed to expose data at an organization level with a single FHIR server per organization. The GP Connect definition of an organization is the legal entity of an organization represented by an ODS code. 

The decision was made to expose the API at an organization level and tie the organization ODS code to the FHIR server endpoint, as the ODS code is the only commonly used identifier across the different GP system providers. 
The organization ODS code of a patient's registered GP practice is stored with their demographics record on the Spine. 
This makes it available to a consumer of the GP Connect API and allows the consumer to perform the endpoint lookup process required to target their request at the GP practice system that holds the patient record.

As the GP Connect API and FHIR server is exposed at an organization level, this results in the following architectural requirements:
- [Branch surgeries](development_branch_surgeries.html) of the main organization will expose their patient data and appointment books through the main organization FHIR server and not their own GP Connect FHIR server
- Organization FHIR server URLs are registered on the SDS against the organization ODS code. Therefore, the consumer API calls are targeted at a single organization represented by an ODS code. If a consumer wishes to get data from a group of organization such as their federation they must make a separate GP Connect API call to each organization from which they want data.


### Distribution of complexity

GP Connect follows the basic principle of API design that 'APIs interfaces are designed always with consumers in mind'. The design goal is to present an interface which maximises ease of use for a consumer.

The expected GP Connect ecosystem sees few 'providers' and many 'consumers' and so it is sensible to place complexity on the provider rather than in the consumer. 
Therefore, where a design decision is required in which the question of where to place complexity is a key point, the default GP Connect position is that complexity should be hidden behind the API interface in provider's business logic. 
GP Connect may diverge from this principle where there is a demonstrated overriding need to have complexity within the consumer rather than in the provider.


## Core API design principles

### FHIR

GP Connect has adopted the [FHIR&reg; standard (STU3)](https://www.hl7.org/fhir/STU3/) and as such the FHIR API design principles will be followed unless a clear rationale exists to amend - in which case any deviation will be logged and the rationale clearly communicated.

Examples of FHIR principles that GP Connect follows are:
- [FHIR RESTful API](https://www.hl7.org/fhir/STU3/http.html){:target="_blank"} principles will be used by default as this is the preferred approach by NHS Digital.
  - synchronous endpoints using `GET`, `POST` and `PUT` HTTP verbs
- [FHIR operation](https://www.hl7.org/fhir/STU3/operations.html){:target="_blank"} APIs to be used in limited 'set piece' circumstances - for example, to pull bundles of resources without using the full generic querying syntax
- business identifiers (such as NHS Number) used to resolve a resource's [logical identity](https://www.hl7.org/fhir/STU3/resource.html#id){:target="_blank"}
- Resources represented as either [XML or JSON](https://www.hl7.org/fhir/STU3/formats.html#wire){:target="_blank"} as requested by the API consumer.  To ensure maximum accessibility, GP Connect is expecting producers to support both formats.  However, since XML is on average 30% larger on the wire there is a preference towards use of JSON. 
- HTML content to utilise XHTML in line with the [FHIR narrative](https://www.hl7.org/fhir/STU3/narrative.html){:target="_blank"} guidance
- ETags for [managing version-aware updates](https://www.hl7.org/fhir/STU3/http.html#concurrency){:target="_blank"}


### Care Connect

GP Connect has worked to align as closely as possible with the Care Connect API, with an aim to maintain a wider interoperability. 
