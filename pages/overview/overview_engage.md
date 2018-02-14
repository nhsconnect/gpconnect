---
title: Getting Involved with GP Connect
keywords: engage, about
tags: [getting_started]
sidebar: overview_sidebar
toc: false
permalink: overview_engage.html
summary: "Getting involved with GP Connect."
---

## The Open API Ecosystem

GP Connect is part of the a wider initiative to expose standards based [Open APIs](https://www.england.nhs.uk/digitaltechnology/info-revolution/interoperability/open-api/){:target="_blank"} to promote innovation and improve care across the NHS.

To make use of the ecosystem and GP Connect APIs we're asking all involved to sign-up to an [Open API Licence](designprinciples_open_api_licence_principles.html) which enshrines concepts such as fair-use and expectations around reciprocity of access to data to improve interoperability beyond just primary care.


### Capabilities

A capability is an area of focus for the GP Connect APIs. There are several [initial capabilities defined](overview_priority_capabilities.html).

### Become an API Consumer

If you're planning on consuming data using GP Connect APIs then you're a Consumer system (e.g. access record).

### Become an API Provider

If you're planning on providing data using GP Connect APIs then you're a Provider system. 



## 1. Get Started ##

- Read about the GP Connect [Priority Capabilities](overview_priority_capabilities.html).
- Look through the Design Decisions made so far in relation to each capability packs ([Foundations](foundations_design.html), [Access Record HTML](accessrecord_design.html), [Access Record Structured](accessrecord_design.html), [Appointment Management](appointments.html) and [Task Management](tasks.html)) and get involved:
	- <span class="label label-success">SELECTED</span> / <span class="label label-info">DECISION</span> A decision has been made for first release.
	- <span class="label label-warning">ASSUMPTION</span> An assumption has been made which is under review/needs validated.

## 2. Explore ## 

- Try out the [GP Connect Demonstrator](system_demonstrator.html) system.
- Optionally download the [GP Connect Demonstrator Codebase](https://github.com/nhs-digital/gpconnect){:target="_blank"} to see how it works. 
- Download our [Swagger API](downloads/swagger/swagger.json) definitions to be used with a tool like the [PostMan Chrome App](https://www.getpostman.com/).

## 3. Develop ##

- Familiarise yourself with HL7&reg; FHIR&reg; (Fast Health Interoperability Resources) ([developer intro](http://www.hl7.org/implement/standards/fhir/overview-dev.html){:target="_blank"}, [exec summary](http://www.hl7.org/implement/standards/fhir/summary.html){:target="_blank"}, or [clinical intro](http://www.hl7.org/implement/standards/fhir/overview-clinical.html){:target="_blank"}).
- Grab an [open source FHIR development library](development_fhir_open_source_guidance.html) for your favourite programming language.
- Familiarise yourself with our GP Connect [FHIR API Guidance](development_fhir_api_guidance.html) common to all APIs.
- Explore the GP Connect Profiled Fhir Resources, a variation of the international [FHIR Resources](https://www.hl7.org/fhir/DSTU2/){:target="_blank"}, for [Foundations](datalibraryfoundation.html), [AccessRecord HTML](datalibraryaccessRecord.html) and [Appointment Management](appointments.html).
- Dig in deep and explore one or more of the GP Connect Capability Packs and start building new or hitting existing APIs.
  - [Foundations capability pack](foundations.html) (e.g. resolve a patient to their logical identifier for further API calls).
  	- Note the foundation per-requisites are mandatory and may restrict your ability to utilise the GP Connect APIs.
  - [Access Record HTML capability pack](accessrecord.html) (e.g. Access html views from the primary care record).
  - [Access Record Structured capability pack](accessrecord_rest.html) (e.g. Access structured data from the primary care record).
  - [Appointment Management capability pack](appointments.html) (e.g. Book an appointment for a patient).
  - [Task Management Capability Pack](tasks.html) (e.g. Send a notification task to a general practice organisation).
- Finally take a look at cross-cutting areas:
  - JSON Web Token - Provides [Cross Organisation Audit and Provenance](integration_cross_organisation_audit_and_provenance.html) details.
  - Additional HTTP headers and Proxy URL - This gives you access to the [Spine Security Proxy](integration_spine_security_proxy.html), the secure 'front door' of GP Connect APIs.
  - Configure HTTPS and TLS MA - [Security Guidance](development_api_security_guidance.html) allows you to secure and mutually authenticate your service with the Spine (which refers to two parties authenticating each other at the same time). 

## 4. Assure ##

- Read about the [Provider Testing](testing_api_provider_testing.html) and [Consumer Testing](testing_api_consumer_testing.html) process.

## 5. Deploy ##

- Become a [First of Type](overview_first_of_type.html) deployment!




## Provide Feedback

To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

Some early feedback on the May 2016 release of the GP Connect draft specification can be found on the [Openhealthhub Forum](https://www.openhealthhub.org/c/fhir-implementation){:target="_blank"} under the category of "FHIR Implementation".

## Community Engagement

GP Connect is working closely with a number of interoperability communities:

- [Code4Health Interoperability Community](https://code4health.org/communities/interoperability){:target="_blank"}
- [INTEROPen Supplier-led Healthcare IT Interoperability Community](http://www.interopen.org/){:target="_blank"}

## Timescales, benefits and more

The content here is designed for a technical audience (i.e. developers, architects and data scientists) for other details (i.e. the vision, timescales, business benefits and case studies) then please see the [NHS Digital GP Connect Homepage](https://digital.nhs.uk/article/1275/GP-Connect){:target="_blank"}.

