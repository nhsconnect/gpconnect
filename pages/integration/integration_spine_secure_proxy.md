---
title: Spine Secure Proxy
keywords: spine, proxy, ssp, security
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_secure_proxy.html
summary: "Overview of the role of the Spine Secure Proxy (SSP) within GP Connect"
---

## Spine Secure Proxy (SSP) - overview ##

The Spine Secure Proxy (SSP) is a forward HTTP proxy which will be used as a front-end to control and protect access to GP principal IT systems that will be exposing FHIR based RESTful APIs as defined by the GP Connect programme.  It provides a single security point for both authentication and authorisation for consuming systems. Additional responsibilities include auditing of all requests, throttling of requests and transaction logging for performance and commercial remuneration purposes. 

![Spine Security Proxy](images/integration/Spine Security Proxy Block Diagram.png)

### Proxied FHIR Requests ###

For First of Type (FoT) implementations FHIR endpoint location will be performed internally by the consumer system utilising the patient’s GP organisational identifier (i.e. ODSCode as returned from a separate PDS lookup process) with the provider's server endpoint being resolved via LDAP queries to the [Spine Directory Service (SDS)](integration_spine_directory_service.html).

{% include important.html content="All HTTP communications are expected to be secured using TLS MA. This includes both legs of the request, from consumer system to the proxy and then from the proxy to provider system." %}

{% include important.html content="All N3 connected systems are expected to synchronise their local system clocks to the N3 Network Time Protocol (NTP) reference source." %}

Once the provider server's endpoint is determined using the SDS a HTTP request to the proxy server will be constructed as follows:

```http
GET https://[proxy_server]/https://[provider_server]/[fhir_base]/[fhir_request]
```

A number of Spine specific HTTP headers also need to be populated with the intended spine interactionID and system ASIDs.

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | Spine's InteractionID |

Furthermore, the consumer's client certificate is validated to ensure it includes valid certificate `CN` and `DN` details and that the certificate has not been added to the certificate revocation list (CRL).

## Spine Secure Proxy (SSP) - implementation guide ##

The [Spine Core FHIR API Framework - SSP Implementation Guide](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html) describes the SSP in more depth and provides the following:

- [Architectural context](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html#system-architecture)
- GP Connect [Consuming system responsibilities](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html#consumer)
- GP Connect [Provider system responsibilities](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html#provider)

