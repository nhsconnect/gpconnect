---
title: Security Guidance
keywords: development
tags: [development]
sidebar: overview_sidebar
permalink: development_api_security_guidance.html
summary: "Details of the API security model and supported protocols."
---

## Secure Connection Negotiation ##

Provider systems SHALL only accept connections from the [Spine Security Proxy](integration_spine_security_proxy_implementation_guide.html) (SSP).

Provider systems SHALL authenticate the SSP prior to responding to any requests using it's [client certificate](development_api_security_guidance.html#client-certificates-tlsma).

Provider systems SHALL only permit approved [supported ciphers](development_api_security_guidance.html#supported-ciphers) to be utilised.

Provider systems SHALL only accept encrypted connections and drop connection attempts presented over insecure protocols.

## Security Testing ##

Provider systems SHALL as a minimum be tested against the [OWASP top 10 web application vulnerabilities](https://www.owasp.org/index.php/Top_10_2013-Top_10).

Provider systems SHOULD be tested for vulnerability to Denial of Service (DoS) and hardened against such attacks.

## Secure Socket Layer (SSL), and Transport Layer Security (TLS) Protocols ##

After consultation with the Infrastructure Security, Operational Security and Spine DDC teams the following SSL protocols SHALL be supported.

{% include important.html content="The list of supported ciphers is ordered in order of preference (i.e. the first item being the most preferred)." %}

- `TLSv1.2`
- `TLSv1.1`
- `TLSv1`

{% include note.html content="SSLv2 and SSLv3 are deprecated and SHALL NOT be used. All consumer and provider systems SHALL be configured to implement TLSv1 and SHOULD be configured to implement TLSv1.1 and above." %}

## Supported Ciphers ##

After consultation with the Infrastructure Security, Operational Security and Spine DDC teams the following SSL protocols SHALL be supported.

{% include important.html content="The list of supported ciphers is ordered in order of preference (i.e. the first item being the most preferred)." %}

- `AESGCM+EECDH`
- `AESGCM+EDH`
- `AES256+EECDH`
- `AES256+EDH`

{% include note.html content="GCM (Galois Counter Mode) suites are prefered as these are resistant to timing attacks<sup>1</sup>." %}

{% include important.html content="A Java 8 (or above) Runtime Environment and/or an upto date version of OpenSSL is required to support the GCM cipher suites." %}

<sup>1</sup>[Digitcert - SSL Support Enabling Perfect Forward Secrecy](https://www.digicert.com/ssl-support/ssl-enabling-perfect-forward-secrecy.htm)

## Tomcat OpenSSL Support Using The APR/Native Provider ##

- SSLCipherSuite = `AESGCM+EECDH,AESGCM+EDH,AES256+EECDH,AES256+EDH`
- SSLHonorCipherOrder = `true`
- SSLProtocol = `TLSv1+TLSv1.1+TLSv1.2`
- SSLVerifyClient = `require`

Please see the [Tomcat Config HTTP SSL Support](https://tomcat.apache.org/tomcat-8.0-doc/config/http.html#SSL_Support) webpage for more details.

## Client Certificates (TLSMA) ##

Provider and Consumer systems SHALL only accept client certificates issued by the NHS Digital Deployment Issue and Resolution (DIR) team.

Provider and Consumer systems SHALL only accept client certificates with a valid Spine 'chain of trust' (i.e. linked to the Spine SubCA and RootCA).

Provider and Consumer systems SHALL only accept client certificates which have not expired or been revoked.

Provider and Consumer systems SHALL check the `FQDN` presented in the client certificate is that of the [Spine Security Proxy](integration_spine_security_proxy_implementation_guide.html) (SSP).

## Response Headers ##

Provider systems SHALL ensure no sensitive data leaks into a browser cache by setting the following cache headers on all responses:

```http
Cache-Control: no-cache, no-store
Expires: 0
Pragma: no-cache
```

## External Documents / Policy Documents ##

| Name | Author | Version | Updated |
| Approved Cryptographic Algorithms Good Practice Guidelines | NHS Digital | v4.0 | 13/07/2016 |
| Warranted Environment Specification (WES) | NHS Digital | v1.0 | June 2015 |