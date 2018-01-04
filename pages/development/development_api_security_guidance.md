---
title: Security guidance
keywords: development
tags: [development]
sidebar: overview_sidebar
permalink: development_api_security_guidance.html
summary: "Details of the API security model and supported protocols"
---

## Secure connection negotiation ##

Provider systems:

- SHALL only accept connections from the [Spine Security Proxy](integration_spine_security_proxy_implementation_guide.html) (SSP)

- SHALL authenticate the SSP prior to responding to any requests using its [client certificate](development_api_security_guidance.html#client-certificates-tlsma)

- SHALL only permit approved [supported ciphers](development_api_security_guidance.html#supported-ciphers) to be utilised

- SHALL only accept encrypted connections and drop connection attempts presented over insecure protocols

- SHALL only accept requests for its allocated address space identifier (ASID), as specified by the `Ssp-To` header  on its matching endpoint URL

- SHALL check that the `Ssp-InteractionID` value is consistent with the endpoint being requested

- SHALL check for the presence of all [SSP headers](integration_spine_security_proxy_implementation_guide.html#consumer)

- SHALL check that an [authorization bearer token](integration_cross_organisation_audit_and_provenance.html#json-web-tokens-jwt) is present and correctly formed

- MAY authorise access to API endpoints through examining acceptable values in the JSON Web Tokens (JWT) requested_scope claim

- SHALL risk-manage the security of the endpoints of the Transport Layer Security (TLS) communications, so as to prevent inappropriate risks (for example, audit logging of the GET parameters into an unprotected audit log)


## Security testing ##

Provider systems SHALL as a minimum be tested against the [OWASP top 10 web application vulnerabilities](https://www.owasp.org/index.php/Top_10_2013-Top_10).

Provider systems SHOULD be tested for vulnerability to Denial of Service (DoS) and hardened against such attacks.

## Secure Socket Layer (SSL), and Transport Layer Security (TLS) protocols ##

After consultation with the Infrastructure Security, Operational Security and Spine DDC teams, the following SSL protocol guidance have been agreed:

- suppliers SHALL use `TLS1.2` with mutual authentication enabled for all message interactions
- at the current time suppliers may use `TLS1.0` or `TLS1.1`, however these protocols will soon become unsupported and suppliers should move to support `TLS1.2` as soon as possible
- suppliers SHALL NOT use `SSLv2` and `SSLv3` as they are deprecated

## Supported ciphers ##

After consultation with the Infrastructure Security, Operational Security and Spine DDC teams the following SSL protocols SHALL be supported.

{% include important.html content="The list of supported ciphers is ordered by preference (that is, the first item being the most preferred)." %}

- `AESGCM+EECDH`
- `AESGCM+EDH`
- `AES256+EECDH`
- `AES256+EDH`
- `AES256+SHA` (temporary support for limited roll-out/FoT only)
- `AES128+SHA` (temporary support for limited roll-out/FoT only)

{% include note.html content="Galois/Counter Mode (GCM) suites are prefered as these are resistant to timing attacks<sup>1</sup>." %}

{% include warning.html content="Support for AES265-SHA and AES128-SHA ciphers is temporary in nature and will be withdrawn." %}

{% include important.html content="A Java Runtime Environment 8 (or above) and/or an up to date version of OpenSSL is required to support the GCM cipher suites." %}

<sup>1</sup>[Digitcert - SSL Support Enabling Perfect Forward Secrecy](https://www.digicert.com/ssl-support/ssl-enabling-perfect-forward-secrecy.htm)

## Tomcat OpenSSL support using the Apache Portable Runtime (APR)/native provider ##

- SSLCipherSuite = `AESGCM+EECDH,AESGCM+EDH,AES256+EECDH,AES256+EDH`
- SSLHonorCipherOrder = `true`
- SSLProtocol = `TLSv1+TLSv1.1+TLSv1.2`
- SSLVerifyClient = `require`

Please see the [Tomcat Config HTTP SSL Support](https://tomcat.apache.org/tomcat-8.0-doc/config/http.html#SSL_Support) web page for more details.

## Client certificates (TLS/mutual authentication (MA)) ##

Provider and consumer systems SHALL only accept client certificates issued by the NHS Digital Deployment Issue and Resolution (DIR) team.

Provider and consumer systems SHALL only accept client certificates with a valid Spine 'chain of trust' (that is, linked to the Spine SubCA and RootCA).

Provider and consumer systems SHALL only accept client certificates which have not expired or been revoked.

Provider and consumer systems SHALL check the `FQDN` presented in the client certificate is that of the [Spine Security Proxy](integration_spine_security_proxy_implementation_guide.html) (SSP).

## Response headers ##

Provider systems SHALL ensure no sensitive data leaks into a browser cache by setting the following cache headers on all responses:

```http
Cache-Control: no-store
```


## Authorisation of access to endpoints ##

The primary purpose of the JWT claims is to [enable cross organisation provenance](integration_cross_organisation_audit_and_provenance.html#cross-organisation-audit--provenance-transport) information to be transmitted for auditing purposes.

Provider systems MAY choose to use the value of the requested_scope claim to authorise access to APIs. In this case, provider systems SHALL apply authorisation logic to endpoints as follows:

| Endpoint | Acceptable values of requested_scope JWT claim |
|-------- | -----------------------------------|
| /Patient | patient/*.[read/write] |
| /Organization | organization/*.[read/write] |
| /Appointment |patient/*.[read/write] |
| /Task | organization/*.[read/write] |
| /Practitioner | organization/*.[read/write] |
| /Location | organization/*.[read/write] |
| /Slot | organization/*.[read/write] |


## External policy documents ##

| Name | Author | Version | Updated |
| Approved Cryptographic Algorithms Good Practice Guidelines | NHS Digital | v4.0 | 13/07/2016 |
| Warranted Environment Specification (WES) | NHS Digital | v1.0 | June 2015 |
