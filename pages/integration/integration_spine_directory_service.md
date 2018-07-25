---
title: Spine Directory Service
keywords: spine, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_directory_service.html
summary: "Overview of the role of the Spine Directory Services (SDS) within GP Connect"
---

## Spine Directory Service (SDS) ##

In order to use the GP Connect API, consumer systems need to integrate with the Spine SDS service to resolve the following two pieces of information which are needed to make an API call:

1. The Accredited System Identifier (ASID) of the organisation which is the target of the request. The ASID will be specified in the `Ssp-To` HTTP header in their request to the [Spine Secure Proxy](integration_spine_secure_proxy.html).
2. The FHIR Endpoint Server Root URL of the organisation which is the target of the request. This is used when constructing the URL of the request to the [Spine Security Proxy](integration_spine_secure_proxy.html).

Full details of how to integrate with SDS to carry out these two steps are outlined at [Spine Core FHIR API Framework - Spine Endpoints](https://developer.nhs.uk/apis/spine-core-1-0/build_endpoints.html). Note that in order to resolve the ASID, Step 1a described there is not required.


{% include roadmap.html content="NHS Digital is considering the delivery of a simplified FHIR facade over the Spine Directory Service (SDS) to allow FHIR endpoint resolution to be achieved in a more streamlined (and FHIR compatible) way." %}


### Consuming system viewpoint ###

#### Worked example of the endpoint lookup process ####

The two step process which a consumer undertakes to integrate with SDS is illustrated using a worked example at [Spine Core FHIR API Framework - Endpoint Lookup Example - SSP](https://developer.nhs.uk/apis/spine-core-1-0/build_endpoints_example_ssp.html).

#### Sample SDS client code ####

Sample client code is provided to ease the process of integration with SDS for GP Connect API consumers. This code provides helper classes which hide the details of the LDAP calls which are needed, and provide a simpler interface for endpoint lookup.

| Language | Code repository |
| -------- | --------------- |
|C# | [gpconnect-dotnet-examples](https://github.com/nhsconnect/gpconnect-dotnet-examples) |
|Java | [gpconnect-java-examples](https://github.com/nhsconnect/gpconnect-java-examples) |

### Provider system viewpoint ###

The provider system is responsible for populating SDS with the necessary information to enable reliable endpoint lookup by consuming systems.

To ensure that endpoint lookup is reliable, the guidelines defined at [Spine Core FHIR API Framework - Endpoint lookup - provider system viewpoint](https://developer.nhs.uk/apis/spine-core-1-0/ssp_providers.html) **MUST** be followed for First of Type implementations.

