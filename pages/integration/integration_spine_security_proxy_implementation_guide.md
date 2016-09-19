---
title: Spine Security Proxy Implementation Guide
keywords: spine, proxy, ssp, security
tags: [integration]
sidebar: overview_sidebar
permalink: integration_spine_security_proxy_implementation_guide.html
summary: "Technical specification for the Spine Security Proxy (SSP)."
---

## Spine Security Proxy (SSP) Implementation Guide ##

Technical overview of the operation of the Spine Security Proxy (SSP).

### Purpose ###

This document is intended for use by software developers looking to build a conformant GP Connect FoT API interfaces or consumer application utilising the Spine Security Proxy (SSP).

### Notational Conventions ###

The keywords "**MUST**", "**MUST NOT**", "**REQUIRED**", "**SHALL**", "**SHALL NOT**", "**SHOULD**", "**SHOULD NOT**", "**RECOMMENDED**", "**MAY**", and "**OPTIONAL**" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt).

## Introduction ##

The Spine Security Proxy (SSP) is a forward proxy which will be used as a front-end to control and protect access to GP principal IT systems that will be exposing FHIR based RESTful APIs as defined by the GP Connect programme.  It will provide a single security point for both authentication and authorisation for consumer and provider systems. Additional responsibilities include auditing of all requests and transaction logging for performance and commercial remuneration purposes. In the first instance the proxy will be made available on the N3 network but it is envisaged that in a later phase of the GP Connect programme access via the public internet will also be supported.

## Background ##

The design of the proxy SHALL support the following business goals:

 - The adoption of open APIs & standards (such as FHIR) driven by need.
 - Creation of a level playing field where access to data is governed by the patient & data controller and not the supplier.

## System Architecture ##

### Block Diagram ###

At a high-level the proxy operates as a content agnostic mediator allowing authorised consumer systems to retrieve HTTPS resources from selected downstream provider systems in a secure and auditable way.

![Spine Security Proxy Block Diagram](images/integration/Spine Security Proxy Block Diagram.png)

### System Roles ###

| Role | Description |
|------|-------------|
| Consumer | Any system which requires access to HTTPS resources of a third-party provider IT system. |
| Proxy | HTTPS/TLS Mutual Authentication (MA) enabled proxy with auditing. |
| Provider | Any system which is capable of servicing HTTPS requests from third-party consumer systems. |

In the First of Type (FoT) instantiation of this system architecture provider systems will be GP principal IT systems from vendors such as (EMIS, TPP, INPS and Microtest), consumer are expected to be a mix of GP principal IT systems and other IT systems. 

As a guiding design principle the Spine Security Proxy (SSP) SHALL NOT impose any interoperability barriers<sup>1</sup> which would impede FHIR compliant client libraries/applications from communicating with FHIR compliant back-end API services. However, it MAY block consumer communications on security grounds (i.e. a consumer attempting to access a provider for which it doesn’t have permission).

<sup>1</sup> consumer applications for FoT are currently expected to be able to populate a small number of additional Spine HTTP headers.

### Proxy Advantages ###

Introducing the Spine Security Proxy (SSP) has the following advantages:

- Removes the need for endpoints to open their firewalls to all potential clients; by allowing them to instead open a single channel to the proxy.
- Removes the need for distributed PKI infrastructure; by allowing endpoints to simply trust the spine PKI certificates.
- Will provide essential diagnostic information about the movement of data with-in the NHS.
- Will enable tracking of performance across the system.
- Will provide a level of protection to provider systems from numerous potential issues (i.e. Distributed Denial of Service attacks).
- Will provide a central point to enable transaction based payments to data providers to be calculated.

### Operating Principle ###

Servicing a consumer system’s request for a FHIR endpoint located on a provider system requires the following series of interactions:

![Proxy Operating Principle](images/integration/Proxy%20Operating%20Principle.png)

| Step | Description | System | Phase 1. Deliverable |
|------|-------------|--------|----------------------|
| 1.   | Retrieve patient demographics and NHS number. | PDS or FHIR SMSP | The consumer system SHALL have performed a PDS or SMSP trace prior to interaction with the proxy.<sup>1</sup><br/><br/>OR (when available^) The consumer system SHALL perform a FHIR SMSP RESTful trace query prior to interaction with the proxy. |
| 2.   | Locate the organisation that holds the patient’s GP care record. | PDS or FHIR RLS | The consumer system SHALL use GP organisation details previously retrieved from PDS. <br/><br/>OR (when available^) The consumer system SHALL use GP organisation details retrieved from the FHIR RLS. |
| 3.   | Lookup what capabilities exist at that organisation to support access to the record. | | SDS or FHIR ELS | 3a) The consumer system SHALL resolve the endpoint of the provider system using an organisational identifier (i.e. ODS code) against SDS. <br/><br/>OR (when available^) 3b) The proxy system SHALL resolve the endpoint of the provider system using a consumer system supplied identifier (i.e. patient NHS number). <br/><br/>OR (when available^) The consumer system SHALL resolve the endpoint of the provider system using a FHIR ELS RESTful query. |
| 4.   | Consumer requests the record. | SSP | The consumer system SHALL build a request URL using the proxy endpoint and either the endpoint of the provider <br/><br/>OR (when available^) the NHS number of the patient<sup>2</sup>. <br/><br/>The consumer system SHALL issue the request to the proxy system over a secure channel. |
| 5.   | Lookup the patient’s sharing preferences. | PPR | Out of scope for GP Connect FoT. |
| 6.   | Lookup organisational data sharing agreements. | DSAR | Out of scope for GP Connect FoT. |
| 7.   | Proxy retrieves the record (throttling as required^) and returns to the consumer system. | SSP | The proxy system SHALL forward on the consumer systems request and return the provider systems response over a secure channel. |

<sup>^</sup> will be made available after the initial GP Connect FoT go-live.
<sup>1</sup> this look-up is to ensure the NHS Number is of good quality in the consumer system and is not required prior to each API operation.
<sup>2</sup> will be limited to the $gpc.getcarerecord interaction.

> Note: whilst composite routing services inside the proxy (i.e. Step 3b) is under consideration this is not in-scope for Connect FoT.

It is expected that for phase 1 delivery a number of supporting systems won’t be available, namely:

- The FHIR SMSP service (step 1).
- The Record Locator service (step 2).
- The Endpoint Locator service (step 3).
- The Patient Preferences Repository (step 5).
- The Data Sharing Agreement Repository (step 6).

As such it is planned that the following mitigations will be implemented as part of phase 1:

- Retrieving patient demographics and NHS number (step 1) will have been performed by the consumer system using a PDS or SMSP trace.
- The Record Location (step 2) and Endpoint Location (step 3a) will be performed internally by the consumer system using the patient’s GP organisational identifier as returned from a PDS lookup with the endpoint look-up being performed via a direct LDAP query to the Spine Director Service (SDS).
- The Patient Preferences Repository (step 5) will not be checked.
- The Data Sharing Agreement Repository (Step 6) will not be checked.

<sup>^</sup> will be made available after the initial GP Connect FoT go-live.

## System Responsibilities ##

### Consumer ###

- PDS trace/validation of NHS number.<sup>1</sup>
- Provides PKI client credentials to allow verification of consumer system.
- Validation of PKI server credentials to allow verification of proxy system.
- Addition of Spine HTTP headers to allow secure routing & system-level auditing.
	- `Ssp-TraceID`
		- `GUID/UUID` which identifies the sender's message/interaction (to be generated per request).
	- `Ssp-From`
		- `ASID` which identifies the sender's FHIR endpoint.
	- `Ssp-To`
		- `ASID` which identifies the recipient's FHIR endpoint.
	- `Ssp-InteractionID`
		- `InteractionID` of the operation being performed.<sup>2</sup>
- Construction of URL formatted for valid consumption by the proxy system.
	- `https://[proxy_server]/https://[provider_server]/[fhir_base]/[fhir_request]`
		- Fully qualified domain name of the proxy system.
		- Fully qualified domain name of the provider system.
		- FHIR URL base.
			- To include any path details.
			- To include major API version details.
			- FHIR URL request.
				- `[type]/[id] {?_format=[mime-type]}`
- Construction of a valid JSON Web Token (JWT) to include the consumer’s client and user claims in line with the audit trail record requirements.<sup>3</sup>
	- UserID, Name, Role and Organisation
	- Identity of authority (the person authorising the entry of, or access to data).
	- The date and time on which the event occurred.
	- Details of the nature of the event and the identity of the associated data (e.g. message / audit event ID) of the event.
- Addition of a HTTP authorization header of the type Bearer including the JWT.
- Issuing FHIR conformant API requests using HTTPS to the proxy system.
- Validation and consumption of FHIR resources returned from the provider system.
- Graceful handling of failed/rejected requests (i.e. `4xx` and `5xx` HTTP error codes).
- Graceful handling of transient error conditions.
	- e.g. incorporation of a back-off strategy and maximum number of 3 automated retries.

The inclusion of the consumer systems UserID, user name and date/time of the event is critical to ensuring a full audit trail can be stored by the provider system. Failure to provide sufficient audit trail information will result in the request being blocked by the spine security proxy^.

<sup>1</sup> this look-up is to ensure the NHS Number is of good quality in the consumer system and is not required prior to each API operation.

<sup>2</sup> a table of `InteractionIDs` for each RESTful API can be found in the [Development - FHIR API Guidance - Operation Guidance](development_fhir_operation_guidance.html) page.

<sup>3</sup> an example of a valid JSON Web Token (JWT) for the purposes of GP Connect can be found in the [Cross Organisation Audit & Provenance](integration_cross_organisation_audit_and_provenance.html) guidance.

### Proxy ###

- Provides PKI client and server credentials to allow verification of proxy system (by both consumer and provider systems).
- Validation of PKI client credentials to allow verification of the consumer system.
- Validation of PKI server credentials to allow verification of the provider system.
- Rejection of consumer requests for provider resources for which there isn’t a valid data sharing agreement in place.^
	- `403` Forbidden
- Rejection of consumer requests that trigger throttling limits put in place to protect downstream provider systems from DoS attacks.^
- Validation of additional HTTP headers for the purposes of security/auditing and debugging/profiling.
	- `Ssp-TraceID`: `GUID/UUID` which identifies the sender's message/interaction (to be generated per request).
	- `Ssp-From`: Sender of the message/request as an `ASID`.
	- `Ssp-To`: Recipient of the message/request as an `ASID`.
	- `Ssp-InteractionID`: The message type or `interactionID` of the message.
- Decoration of additional HTTP headers into the response for notifying consumer systems of throttling limits in-line with industry best practise.^
	- `X-Rate-Limit-Limit`:  The number of allowed requests in the current period.
	- `X-Rate-Limit-Remaining`: The number of remaining requests in the current period.
	- `X-Rate-Limit-Reset`: The number of seconds left in the current period.
- Validation of NHS Number by length and check digit only.^
- Forwarding of consumer requests (including all headers, query parameters and payload) onto the downstream provider systems, agnostic of content type and content encoding.
- Streaming of provider response data back to the consumer system, agnostic of transport type and encoding.
- Performant operation supporting `X concurrent client connections` and `Y requests per second`.
- Highly available with an uptime of `X.YZ %`.
- Low latency with a maximum lag of `X ms`.
- Supply of monitoring endpoints/data to allow regular observation and recording of the activities being performed by the proxy.
- Fail-safe error and fault handling mechanisms such that any detected error or failure doesn’t cause the system to halt or loose data.

{% include important.html content="Service Level Agreements (SLA) will be negotiated with principal system vendors prior to go-live to ensure non-functional aspects of system operation are finalised and guaranteed." %}

{% include tip.html content="Non functional testing by the Spine team has indicated a fairly constant 15ms average latency traversing the Spine Security Proxy (SSP) regardless of payload size." %}

### Provider ###
 
- PDS trace/validation of NHS number.<sup>1</sup>
	- Exposed patient records are expected to contain only curated NHS numbers.
- Provides PKI server credentials to allow verification of provider system.
- Validation of PKI credentials to allow verification of proxy system.
- Processing of FHIR conformant API requests and generation of FHIR conformant responses.
- Error response generation in line with FHIR and HTTP conventions including the return of transient HTTP error codes when appropriate (i.e. due to the provider being down or busy).
	- `503` Service Unavailable

<sup>1</sup> this look-up is to ensure the NHS Number is of good quality in the provider system and is not required prior to each API operation.

## Proxy Requirements ##

### In Scope for FoT ###

- Authentication of consumer/provider systems.
- End-to-End encryption of all traffic between systems.
- Transparent retrieval of HTTPS resources from provider systems.
- Performant retrieval of HTTPS resources.
- Audit & transaction logging to existing Spine centralised audit logging infrastructure (i.e. Splunk). 
- Reporting of volumetric and performance statistics to allow activity based remuneration back to the supplying vendor of the provider system(s).

### Out of Scope for FoT ###

- Authorisation of consumer requests against a Data Sharing Repository.
- Distributed Denial of Service (DDoS) protection / throttling to protect provider systems from being swamped (either intentionally or unintentionally) by consumer systems.
- Patient Index search/trace functionality.
	- Consumer systems are expected to be integrated with the existing PDS (or equivalent) system.
- User Authentication.
- Authorisation of the consumer’s client credentials through verification of a security token.
- Endpoint Location Service functionality.
	- In a future phase consumer systems will be expected to integrate with the National Endpoint Locator Service.
- Record Location Service functionality.
	- In a future phase consumer systems will be expected to integrate with the National Record Locator Service.
- Patient Preference (Consent) Service functionality.
	- Provider systems will be expected to respect record access protections at source when the patient’s sharing preferences (as recorded in the provider system) indicate that the patient’s record isn’t to be shared.

### Constraints ###

- As NHS smartcards will not be available for use by many consumer systems the systems should not depend on them for operation.

{% include roadmap.html content="The roadmap for handling of user level credentials is being explored under the NHS Digital Interoperability Platform (DIP) workstream." %}

### Functional Requirements ###

- Transport level integration SHALL be via HTTP as defined in [RFC 2616](https://tools.ietf.org/html/rfc2616).
- Transport level security SHALL be via TLS/HTTPS as defined in [RFC 5246](https://tools.ietf.org/html/rfc5246) and [RFC 6176](https://tools.ietf.org/html/rfc6176).
- HTTP Strict Transport Security (HSTS) as defined in [RFC 6797](https://tools.ietf.org/html/rfc6797) SHALL be employed to protect against protocol downgrade attacks and cookie hijacking.
- Authentication of systems connecting to the proxy SHALL be via PKI certificates with TLS Mutual Authentication (MA) providing two-way authentication.
	- The `FQDN` presented in the client certificate SHALL be checked against the `FQDN` registered against the `ASID`.
- To support web and mobile application development in which consumer requests will come from a domain outside the domain from which the resource originated the Cross-Origin Resource Sharing (CORS) mechanisms as defined in [Cross-Origin Resource Sharing W3C Recommendation](http://www.w3.org/TR/cors/) SHALL be supported^.
- To minimise the HTTPS handshake overhead and improve performance the proxy SHALL respect and support the HTTP `keep-alive` connection header allowing a connection between client and server to be used for multiple requests.
- Request-response between consumer and provider (via the proxy) systems SHALL be synchronous in nature with the consumer system waiting for the response payload.
- Request-response between consumer and provider (via the proxy) systems SHALL utilise any of the following HTTP verbs to support RESTful API interactions.
	- `GET`
	- `POST`
	- `PUT`
	- `DELETE`^
	- `PATCH`^ (which is expected in a future FHIR release)
	- `OPTION`^ (which is used in FHIR to retrieve the servers conformance statement)
 **^** HTTP verbs will be made available after the initial GP Connect FoT go-live.
- Request and response HTTP payloads SHALL NOT be modified, as this would require the proxy to have detained knowledge of payload structure and transport encoding. Furthermore, payload modification may introduce problems with asserting digital signatures/payload provenance in the future.
- Request and response HTTP headers SHALL NOT be modified.
- The proxy SHOULD validate and SHALL log for audit purposes user and system claims provided in the HTTP authorization header as an oAuth bearer token (as outlined in [RFC 6749](https://tools.ietf.org/html/rfc6749)) in the form of a JSON Web Token (JWT) as defined in [RFC 7519](https://tools.ietf.org/html/rfc7519).
	- Refer to the [Cross Organisation Audit & Provenance](integration_cross_organisation_audit_and_provenance.html) implementation guidance for full details.
- Additional request and response HTTP Headers SHOULD be added into the HTTP request/response for the purposes of security/auditing and debugging/profiling purposes.
- Additional HTTP response headers SHALL be added into the HTTP response for the purpose of throttling/rate limiting API access.
- As outlined in [RFC 6585](http://tools.ietf.org/html/rfc6585) HTTP status code 429 SHALL be used to notify consumer systems that their throttling limit has been reached or that the server is experiencing a DoS attack.
	- `429`	Too Many Requests
- HTTP status code `503` SHALL be returned if the cumulative load on the provider system exceeds a global throttling limit or the server is experiencing a DDoS attack.
- [FHIR DSTU2](http://hl7.org/fhir/index.html) standard will be the first API standard that will be mediated via the proxy.
- As a variety of payload types (both binary and textual) will be requested via the proxy the proxy SHALL NOT restrict the content types or payload size that can be transported.
- Additional HTTP headers SHALL be added into the HTTP request/response for the purpose of allowing the proxy system to disclose information lost in the proxying process (e.g. the originating IP address of a request). Typically, this information is added to proxy forwarding headers as defined in [RFC 7239](https://tools.ietf.org/html/rfc7239).
- To enable interoperability with existing implementations of FHIR the proxy SHALL support the return of chunked transfers (utilising the `Transfer-Encoding: chunked` HTTP header) to stream data back to the client without specifying explicitly a payload content length.
- Common HTTP status codes related to FHIR operations (in addition to normal HTTP errors related to security, header and content negotiation issues) SHALL be logged by the proxy and passed through to the consumer system.
	- `400`	Bad Request
	- `403`	Forbidden
	- `404`	Not Found
	- `405`	Method Not Allowed
	- `409`	Version Conflict
	- `422`	Unprocessed Entity
	- `429`	Too Many Requests
- If a downstream provider system is unreachable or fails to fulfil a valid request with a valid response then a gateway error SHALL be returned to the consumer system.
	- `502` Bad Gateway
- If a downstream provider system fails to fulfil a request within a configured timeout period then the connection should be closed and a HTTP timeout response SHALL be returned to the consumer system.
	- `504` Gateway Timeout
- If the following specific error conditions occur then the proxy SHALL return the corresponding HTTP status codes to the consumer system.
	- `403`	Forbidden
	- `444`	No Response
		- Used to indicate that the server has returned no information to the client and closed the connection.
	- `495`	SSL Certificate Error
		- Used when the client has provided an invalid client certificate.
	- `496`	SSL Certificate Required
		- Used when a client certificate is required but not provided.
	- `497`	HTTP Request Sent to HTTPS Port
		- Used when the client has made a HTTP request to a port listening for HTTPS requests.
	- `499`	Client Closed Request
		- Used when the client has closed the request before the server could send a response.
			- To be logged by the proxy as it can’t be sent to client/consumer.

