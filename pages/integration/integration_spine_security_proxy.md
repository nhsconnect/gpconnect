---
title: Spine Security Proxy
keywords: spine, proxy, ssp, security
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_security_proxy.html
summary: "Overview of the role of the Spine Security Proxy (SSP) within GP Connect."
---

## Spine Security Proxy (SSP) ##

The Spine Security Proxy (SSP) is a forward HTTP proxy which will be used as a front-end to control and protect access to GP principal IT systems that will be exposing FHIR based RESTful APIs as defined by the GP Connect programme.  It provides a single security point for both authentication and authorisation for consuming systems. Additional responsibilities include auditing of all requests, throttling of requests and transaction logging for performance and commercial remuneration purposes. 

![Spine Security Proxy](images/integration/Spine Security Proxy Block Diagram.png)

### Proxied FHIR Requests ###

For First of Type (FoT) implementations FHIR endpoint location will be performed internally by the consumer system utilising the patient’s GP organisational identifier (i.e. ODSCode as returned from a separate PDS lookup process) with the provider's server endpoint being resolved via LDAP queries to the [Spine Director Service (SDS)](integration_spine_directory_service.html).

{% include important.html content="All HTTP communications are expected to be secured using TLS MA. This includes both legs of the request, from consumer system to the proxy and then from the proxy to provider system." %}

{% include important.html content="All N3 connected systems are expected to synchronise their local system clocks to the N3 Network Time Protocol (NTP) reference source." %}

Once the provider server's endpoint is determined using the SDS a HTTP request to the proxy server will be constructed as follows:

```http
GET https:/[proxy_server]/https://[provider_server]/[fhir_base]/[fhir_request]
```

A numder of Spine specific HTTP headers also need to be populated with the intended spine interactionID and system ASIDs.

| Header               | Value |
|----------------------|-------|
| `SSP-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `SSP-From`           | Consumer's ASID |
| `SSP-To`             | Provider's ASID |
| `SSP-InteractionID`  | Spine's InteractionID |

Please refer to the [Spine Security Proxy Implementation Guide](integration_spine_security_proxy_implementation_guide.html) for full technical details.

