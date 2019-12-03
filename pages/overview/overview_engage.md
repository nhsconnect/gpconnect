---
title: Getting involved with GP Connect API
keywords: engage, about
tags: [getting_started]
sidebar: overview_sidebar
toc: false
permalink: overview_engage.html
summary: "Getting involved with GP Connect"
---

## The Open API ecosystem

GP Connect is part of a wider initiative to expose standards based [Open APIs](designprinciples_open_api_principles.html) to promote innovation and improve care across the NHS.

### Capabilities

A capability is an area of focus for the GP Connect APIs. There are several [initial capabilities defined](overview_priority_capabilities.html).

### Become an API consumer

If you're planning on consuming data using GP Connect APIs then you're a consumer system.

### Become an API provider

If you're planning on providing data using GP Connect APIs then you're a provider system. 



## 1. Get started ##

- read about the GP Connect [Priority capabilities](overview_priority_capabilities.html)
- look through the design decisions made so far in relation to each capability pack ([Foundations](foundations_design.html) and [Access Record HTML](accessrecord.html)), and get involved:
	- <span class="label label-success">SELECTED</span> / <span class="label label-info">DECISION</span> A decision has been made for first release
	- <span class="label label-warning">ASSUMPTION</span> An assumption has been made which is under review/needs validation

## 2. Explore ## 

- try out the [GP Connect Demonstrator](system_demonstrator.html) system
- optionally download the [GP Connect Demonstrator Codebase](https://github.com/nhs-digital/gpconnect){:target="_blank"} to see how it works
- download our [PostMan Collection](system_reference_postman.html) and explore the GP Connect interactions

## 3. Develop ##

- familiarise yourself with HL7&reg; FHIR&reg; ([developer introduction](http://www.hl7.org/implement/standards/fhir/overview-dev.html){:target="_blank"}, [executive summary](http://www.hl7.org/implement/standards/fhir/summary.html){:target="_blank"}, or [clinical intro](http://www.hl7.org/implement/standards/fhir/overview-clinical.html){:target="_blank"})
- grab an [open source FHIR development library](development_fhir_open_source_guidance.html) for your favourite programming language
- if you are a consumer, decide which wire format to use (JSON or XML)
{% include important.html content="Consumers planning their development should read [the following information](support_faq.html#which-serialisation-format-should-i-choose-as-an-gp-connect-api-consumer---json-or-xml) before choosing whether to use JSON or XML in their implementation." %}
- familiarise yourself with our GP Connect [FHIR API guidance](development_fhir_api_guidance.html) common to all APIs
- explore the GP Connect profiled FHIR resources, a variation of the international [FHIR resources](https://www.hl7.org/fhir/STU3/){:target="_blank"}, for [Foundations](datalibraryfoundation.html) and [Access Record HTML](accessrecord.html)
- dig in deep and explore one or more of the GP Connect capability packs and start building new or hitting existing APIs:
  - [Foundations](foundations.html) (e.g. resolve a patient to their logical identifier for further API calls)
  	- Note the foundation per-requisites are mandatory
  - [Access Record HTML](accessrecord.html) (e.g. Access html views from the primary care record)
  - [Access Record Structured](accessrecord_structured.html) (e.g. Access structured data from the primary care record)
  - [Appointment Management](appointments.html) (e.g. Book an appointment for a patient)
- finally take a look at cross-cutting areas:
  - JSON Web Token - Provides [Cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html) details
  - additional HTTP headers and proxy URL - This gives you access to the [Spine Secure Proxy](integration_spine_secure_proxy.html), the secure 'front door' of GP Connect APIs
  - configure HTTPS and TLS/MA - [Security guidance](development_api_security_guidance.html) allows you to secure and mutually authenticate your service with the Spine (which refers to two parties authenticating each other at the same time)

## 4. Assure ##

- read about the [Provider testing](testing_api_provider_testing.html) and [Consumer testing](testing_api_consumer_testing.html) process

## 5. Deploy ##

- become a first of type deployment - see below to get in touch with the GP Connect programme


## Provide feedback

To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

Some early feedback on the May 2016 release of the GP Connect draft specification can be found on the [OpenHealthHub forum](https://www.openhealthhub.org/c/fhir-implementation){:target="_blank"} under the category of "FHIR Implementation".

## Community engagement

GP Connect is working closely with [INTEROPen](http://www.interopen.org/){:target="_blank"}, a healthcare IT interoperability community of suppliers, NHS organisations and healthcare standards bodies in the UK.

## Timescales, benefits and more

The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/services/gp-connect){:target="_blank"}.

