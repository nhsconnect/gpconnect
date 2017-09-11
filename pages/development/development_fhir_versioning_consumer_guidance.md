---
title: Consumer Versioning Guidance
keywords: fhir development
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_versioning_consumer_guidance.html
summary: "Details of the common versioning requirements for GP Connect consumers."
---

In order for a consumer to find the provider endpoint which supports an interaction version, they SHALL perform a sequence of query operations against existing Spine services:

1. The Clients SHALL perform (or have previously performed) a PDS lookup for a patient. From the result of the PDS lookup the consumer can determine the patient's primary GP organisation ODS Code.
2. The Clients SHALL perform (or have previously performed) a pair of queries against the SDS, as specified on the [Spine Directory Service](/integration_spine_directory_service.html) page, using the patients primary GP organisation ODS code and the InteractionID for the capability which they wish to perform in order to find the correct endpoint on the Principal GP system responsible for hosting the capability.
3. The Clients SHALL construct a [FHIR Service Root URL](#ServiceRootURL) suitable for access to a GP providers FHIR server, using the response from the SDS queries. For GP Connect access to the Principal GP systems, requests will go via the [Spine Security Proxy](#SpineSecurityProxy) and as such the URL will need to be pre-pended with a Proxy Service Root URL as per the [Spine Security Proxy](integration_spine_security_proxy.html#proxied-fhir-requests) part of the specification.

