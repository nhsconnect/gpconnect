---
title: Security guidance
keywords: development
tags: [development]
sidebar: overview_sidebar
permalink: development_api_security_guidance.html
summary: "Details of the API security model and supported protocols"
---

## Secure connection negotiation ##

Provider Systems:

- **MUST** only accept connections from the [Spine Security Proxy](integration_spine_security_proxy_implementation_guide.html) (SSP)

- **MUST** authenticate the SSP prior to responding to any requests using its [client certificate](development_api_security_guidance.html#client-certificates-tlsma)

- **MUST** only permit approved [supported ciphers](development_api_security_guidance.html#supported-ciphers) to be utilised

- **MUST** only accept encrypted connections and drop connection attempts presented over insecure protocols

- **MUST** only accept requests for its allocated ASID, as specified by the `Ssp-To` header, on its matching endpoint URL

- **MUST** check that the `Ssp-InteractionID` value is consistent with the endpoint being requested

- **MUST** check for the presence of all [SSP headers](integration_spine_security_proxy_implementation_guide.html#consumer)

- **MUST** check that an [authorization bearer token](integration_cross_organisation_audit_and_provenance.html#cross-organisation-audit-and-provenance-transport) in present and correctly formed

- **MAY** authorise access to API endpoints through examining acceptable values in the JWT requested_scope claim

## Security testing ##

Provider systems **MUST** as a minimum be tested against the [OWASP top 10 web application vulnerabilities](https://www.owasp.org/index.php/Top_10_2013-Top_10).

Provider systems **SHOULD** be tested for vulnerability to Denial of Service (DoS) and hardened against such attacks.

## Secure Socket Layer (SSL), and Transport Layer Security (TLS) protocols ##

After consultation with the Infrastructure Security, Operational Security and Spine DDC teams the following SSL protocols **MUST** be supported.

- `TLSv1.2`

{% include note.html content="SSLv2, SSLv3, TLSv1.0 and TLSv1.1 are deprecated and **MUST NOT** be used. All consumer and provider systems **MUST** be configured to implement TLSv1.2." %}

## Supported ciphers ##

After consultation with the Infrastructure Security, Operational Security and Spine DDC teams the following SSL protocols **MUST** be supported.

{% include important.html content="The list of supported ciphers is ordered in order of preference (i.e. the first item being the most preferred)." %}

- `AESGCM+EECDH`
- `AESGCM+EDH`
- `AES256+EECDH`
- `AES256+EDH`

{% include note.html content="GCM (Galois Counter Mode) suites are preferred as these are resistant to timing attacks<sup>1</sup>." %}

{% include important.html content="A Java 8 (or above) Runtime Environment and/or an up-to-date version of OpenSSL is required to support the GCM cipher suites." %}

<sup>1</sup>[Digitcert - SSL Support Enabling Perfect Forward Secrecy](https://www.digicert.com/ssl-support/ssl-enabling-perfect-forward-secrecy.htm)

## Tomcat OpenSSL support using the APR/native provider ##

- SSLCipherSuite = `AESGCM+EECDH,AESGCM+EDH,AES256+EECDH,AES256+EDH`
- SSLHonorCipherOrder = `true`
- SSLProtocol = `TLSv1.2`
- SSLVerifyClient = `require`

Please see the [Tomcat Config HTTP SSL Support](https://tomcat.apache.org/tomcat-8.0-doc/config/http.html#SSL_Support) webpage for more details.

## Client certificates (TLSMA) ##

Provider and Consumer systems **MUST** only accept client certificates issued by the NHS Digital Deployment Issue and Resolution (DIR) team.

Provider and Consumer systems **MUST** only accept client certificates with a valid Spine 'chain of trust' (i.e. linked to the Spine SubCA and RootCA).

Provider and Consumer systems **MUST** only accept client certificates which have not expired or been revoked.

Provider and Consumer systems **MUST** check the `FQDN` presented in the client certificate is that of the [Spine Security Proxy](integration_spine_security_proxy_implementation_guide.html) (SSP).

## Response headers ##

Provider systems **MUST** ensure no sensitive data leaks into a browser cache by setting the following cache headers on all responses:

```http
Cache-Control: no-store
```


## Authorisation of access to endpoints ##

The primary purpose of the JWT claims is to [enable cross organisation provenance](integration_cross_organisation_audit_and_provenance.html#cross-organisation-audit-provenance-transport) information to be transmitted for auditing purposes.

Provider systems **MAY** choose to use the value of the requested_scope claim to authorise access to APIs. In this case, provider systems **MUST** apply authorisation logic to endpoints as follows:

| Endpoint | Acceptable values of requested_scope JWT claim |
|-------- | -----------------------------------|
| /Patient | patient/*.[read/write] |
| /Organization | organization/*.[read/write] |
| /Appointment |patient/*.[read/write] |
| /Task | organization/*.[read/write] |
| /Practitioner | organization/*.[read/write] |
| /Location | organization/*.[read/write] |
| /Slot | organization/*.[read/write] |


## External Documents / Policy Documents ##

| Name | Author | Version | Updated |
| [Approved Cryptographic Algorithms Good Practice Guidelines](http://webarchive.nationalarchives.gov.uk/20161021125701/http:/systems.digital.nhs.uk/infogov/security/infrasec/gpg/acs.pdf) | NHS Digital | v4.0 | July 2016 |
| [Warranted Environment Specification (WES)](https://digital.nhs.uk/spine/technical-information-warranted-environment-specification) | NHS Digital | v3.2018 | 2018 |
