---
title: Consumer Versioning Guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_versioning_consumer_guidance.html
summary: "Details of the common versioning requirements for GP Connect consumers."
---

In order for a consumer to find the correct provider endpoint for the capability version which they wish to make a request using, they SHALL perform a sequence of query operations against existing Spine services to enable FHIR endpoint resolution.

1. Clients SHALL perform (or have previously performed) a PDS lookup for a patient. From the result of the PDS lookup the consumer can determine the patient's primary GP organisation ODS Code. 
2. Clients SHALL perform (or have previously performed) a pair of queries against the SDS, as specified on the [Spine Directory Service](/integration_spine_directory_service.html) page, using the patients primary GP organisation ODS code and the InteractionID for the capability which they wish to perform in order to find the correct endpoint on the Principal GP system responsible for hosting the capability.
3. Clients SHALL construct a [FHIR Service Root URL](#ServiceRootURL) suitable for access to a GP providers FHIR server, using the response from the SDS queries. For GP Connect access to the Principal GP systems will be via the [Spine Security Proxy](#SpineSecurityProxy) and as such the URL will need to be pre-pended with a Proxy Service Root URL.

Consumer systems are required to construct a [Service Root URL containing the SSP URL followed by the FHIR Server Root URL of the logical practice FHIR server](integration_spine_security_proxy.html#proxied-fhir-requests) that is suitable for interacting with the SSP service. API provider systems will be unaware of the SSP URL prefix as this will be removed prior to calling the provider API endpoint.
