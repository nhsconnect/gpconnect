---
title: Spine Secure Proxy
keywords: spine, proxy, ssp, security
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_secure_proxy.html
summary: "Overview of the role of the Spine Secure Proxy (SSP) within GP Connect"
---

## Overview ##

The Spine Secure Proxy (SSP) is a forward HTTP proxy which is used as a broker to control and protect access to GP principal IT systems that expose FHIR based GP Connect APIs.  

It provides a single security point for both authentication and authorisation for consuming systems. Additional responsibilities include auditing of requests, checking data sharing agreements and transaction logging. 

All HTTP communications are secured using TLS MA. This includes both legs of the request, from consumer system to the proxy and then from the proxy to provider system.

![Spine Security Proxy](images/integration/ssp-diagram.png)

## Constructing a request ##

A consumer system queries [Spine Directory Service](integration_spine_directory_service.html#querying-sds) using the provider's ODS code to determine:

- the provider's [service root URL](development_general_api_guidance.html#service-root-url) (their "base endpoint")
- the provider's ASID, used in headers below

Once these are retrieved, a GP Connect HTTP request is constructed to send to the SSP in the following format:

```http
GET https://[ssp_fqdn]/[provider_service_root_url]/[fhir_request]
```

Where:

  - `[ssp_fqdn]` is the fully qualified domain name of the SSP
  - `[provider_service_root_url]` is the provider's service root URL as returned from SDS in the `nhsMhsEndPoint` attribute. This element is normally in the format `https://[provider_fqdn]/[path_to_fhir_base]`
  - `[fhir_request]` is the local portion of the request relating to the FHIR API call being made, including query parameters

Please note `GET` is used as an example; the actual HTTP method will vary based on API call.

{% include sds_ssp_warning.html %}

As an example, to request a patient's structured record, the following URL would be constructured (HTTP headers and payload are not included):

```http
POST https://testspineproxy.nhs.uk/https://pcs.thirdparty.nhs.uk/T99999/STU3/1/Patient/$gpc.getstructuredrecord
```

Please see a [worked example of the endpoint lookup process](integration_spine_directory_service.html#worked-example-of-the-endpoint-lookup-process) for more information.

## HTTP headers ##

The SSP requires a number of Spine specific HTTP headers to be populated when sending a request:

| Header               | Value | Notes |
|----------------------|-------|-------|
| `Ssp-TraceID`        | Consumer Trace ID | GUID/UUID generated per request |
| `Ssp-From`           | Consumer ASID | Consumer system ASID; see note below |
| `Ssp-To`             | Provider ASID | See [SDS queries](integration_spine_directory_service.html#worked-example-of-the-endpoint-lookup-process) to lookup the provider's ASID |
| `Ssp-InteractionID` &nbsp; &nbsp; &nbsp; | Spine Interaction ID  &nbsp; &nbsp; &nbsp; &nbsp; | See GP Connect [Interaction IDs](integration_interaction_ids.html#list-of-interaction-ids) |

{% include important.html content="Where GP Connect consumer applications are provisioned via a portal or middleware hosted by another organisation, it is vital that the ASID sent in the `Ssp-From` header reflects the organisation from where the request originates, rather than the hosting organisation." %}

## Further details ##

The [Spine Core FHIR API Framework - SSP Implementation Guide](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html) describes the SSP in more depth and provides the following:

- [Architectural context](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html#system-architecture)
- GP Connect [Consuming system responsibilities](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html#consumer)
- GP Connect [Provider system responsibilities](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html#provider)

