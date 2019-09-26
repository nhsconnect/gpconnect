---
title: Getting started
keywords: engage, about
tags: [getting_started]
sidebar: overview_sidebar
toc: false
permalink: overview_engage.html
summary: "Getting started with GP Connect API"
---

## Background

### Capabilities

A capability is an area of focus for the GP Connect APIs, this specification covers the access record document capability.

### Become an API consumer

If you're planning on consuming data using GP Connect APIs then you're a consumer system.

### Become an API provider

If you're planning on providing data using GP Connect APIs then you're a provider system.



## 1. Get started ##

- Read about the GP Connect [Access Record Document capability](accessrecord_documents_development_documents_guidance.html).


## 2. Explore ##

- Try out the [GP Connect Demonstrator](system_demonstrator.html) system.
- Optionally download the [GP Connect Demonstrator Codebase](https://github.com/nhs-digital/gpconnect){:target="_blank"} to see how it works.
- Download our [PostMan Collection](system_reference_postman.html) and explore the GP Connect interactions.

## 3. Develop ##

- Familiarise yourself with HL7&reg; FHIR&reg; ([developer introduction](http://www.hl7.org/implement/standards/fhir/STU3/overview-dev.html){:target="_blank"}, [executive summary](http://www.hl7.org/implement/standards/fhir/STU3/summary.html){:target="_blank"}, or [clinical intro](http://www.hl7.org/implement/standards/fhir/STU3/overview-clinical.html){:target="_blank"}).
- Grab an [open source FHIR development library](development_fhir_open_source_guidance.html) for your favourite programming language.
- If you are a consumer, decide which wire format to use (JSON or XML)
{% include important.html content="Consumers planning their development should read [the following information](support_faq.html#which-serialisation-format-should-i-choose-as-an-gp-connect-api-consumer---json-or-xml) before choosing whether to use JSON or XML in their implementation." %}
- Familiarise yourself with our GP Connect [FHIR API guidance](development_fhir_api_guidance.html) common to all APIs.
- Read the [GP Connect Document API guidance](accessrecord_documents_development_documents_guidance.html) to learn more about the Access Record Documents capability.
- Finally take a look at cross-cutting areas:
  - JSON Web Token - Provides [Cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html) details.
  - Additional HTTP headers and proxy URL - This gives you access to the [Spine Secure Proxy](integration_spine_secure_proxy.html), the secure 'front door' of GP Connect APIs.
  - Configure HTTPS and TLS/MA - [Security guidance](development_api_security_guidance.html) allows you to secure and mutually authenticate your service with the Spine (which refers to two parties authenticating each other at the same time).

## 4. Assure ##

- Read about the [Provider testing](testing_api_provider_testing.html) and [Consumer testing](testing_api_consumer_testing.html) process.

## 5. Deploy ##

- Become a first of type deployment - see below to get in touch with the GP Connect programme.


## Provide feedback

To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

Some early feedback on the May 2016 release of the GP Connect draft specification can be found on the [OpenHealthHub forum](https://www.openhealthhub.org/c/fhir-implementation){:target="_blank"} under the category of "FHIR Implementation".

## Community engagement

### The Open API ecosystem

GP Connect is part of a wider initiative to expose standards based [Open APIs](designprinciples_open_api_principles.html#open-api){:target="_blank"} to promote innovation and improve care across the NHS.

### INTEROPen

GP Connect FHIR profiles specified within this site have been developed by NHS Digital and where available use CareConnect profiles created in collaboration with the INTEROPen community.

The INTEROPen vision is to create a library of nationally defined HL7® FHIR® resources and interaction patterns that implementers can adopt to simplify integration and interoperability within England’s health and social care systems. Find out more on the [INTEROPen website](https://www.interopen.org/)

## Timescales, benefits and more

The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/services/gp-connect){:target="_blank"}.
