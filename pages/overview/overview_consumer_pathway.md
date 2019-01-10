---
title: Getting started for consumer suppliers
keywords: consumer
tags: [consumer]
sidebar: overview_sidebar
permalink: overview_consumer_pathway.html
summary: Step-by-step guide to developing consumer applications
---

**Under Construction**

Intro paragraph



## 1. Get started ##

- Read about the GP Connect [Priority capabilities](overview_priority_capabilities.html).
- Look through the design decisions made so far in relation to each capability pack ([Foundations](foundations_design.html), [Access Record HTML](accessrecord.html), [Access Record Structured](accessrecord_structured_design.html) and [Appointment Management](appointments_design.html) and get involved:
	- <span class="label label-success">SELECTED</span> / <span class="label label-info">DECISION</span> A decision has been made for first release.
	- <span class="label label-warning">ASSUMPTION</span> An assumption has been made which is under review/needs validated.

## 2. Explore ## 

- Try out the [GP Connect Demonstrator](system_demonstrator.html) system.
- Optionally download the [GP Connect Demonstrator Codebase](https://github.com/nhs-digital/gpconnect){:target="_blank"} to see how it works. 
- Download our [PostMan Collection](system_reference_postman.html) and explore the GP Connect interactions.

## 3. Develop ##

- Familiarise yourself with HL7&reg; FHIR&reg; ([developer introduction](http://www.hl7.org/implement/standards/fhir/overview-dev.html){:target="_blank"}, [executive summary](http://www.hl7.org/implement/standards/fhir/summary.html){:target="_blank"}, or [clinical intro](http://www.hl7.org/implement/standards/fhir/overview-clinical.html){:target="_blank"}).
- Grab an [open source FHIR development library](development_fhir_open_source_guidance.html) for your favourite programming language.
- If you are a consumer, decide which wire format to use (JSON or XML)
{% include important.html content="Consumers planning their development should read [the following information](support_faq.html#which-serialisation-format-should-i-choose-as-an-gp-connect-api-consumer---json-or-xml) before choosing whether to use JSON or XML in their implementation." %}
- Familiarise yourself with our GP Connect [FHIR API guidance](development_fhir_api_guidance.html) common to all APIs.
- Explore the GP Connect profiled FHIR resources, a variation of the international [FHIR resources](https://www.hl7.org/fhir/STU3/){:target="_blank"}, for [Foundations](datalibraryfoundation.html), [Access Record HTML](accessrecord.html), [Access Record Structured](accessrecord_structured_development_resources_overview.html), and [Appointment Management](datalibraryappointment.html).
- Dig in deep and explore one or more of the GP Connect capability packs and start building new or hitting existing APIs.
  - [Foundations](foundations.html) (e.g. resolve a patient to their logical identifier for further API calls).
  	- Note the foundation per-requisites are mandatory.
  - [Access Record HTML](accessrecord.html) (e.g. Access html views from the primary care record).
  - [Access Record Structured](accessrecord_structured.html) (e.g. Access structured data from the primary care record).
  - [Appointment Management](appointments.html) (e.g. Book an appointment for a patient).
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

GP Connect is working closely with [INTEROPen](http://www.interopen.org/){:target="_blank"}, a healthcare IT interoperability community of suppliers, NHS organisations and healthcare standards bodies in the UK.

## Timescales, benefits and more

The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/article/1275/GP-Connect){:target="_blank"}.


## Getting started ##

## Explore ##
Use the system demonstrator to explore GP Connect functionality and access the Personal Demographics Service (PDS) and the Spine Directory Service (SDS) without an HSCN connection.

## Develop ##
There a number of APIs (capabilities) that GP Connect is aiming to deliver with the 4 GP Principal Clinical Systems Supplier– these relate to accessing GP records, appointments and structured data.
These need to be built to NHS standards – we are currently using FHIR standards

## Test and assure ##
The Consumer APIs need to go through a set of testing and assurance processes to ensure they are robust enough to meet the demands of busy NHS organisations. You will need to provide evidence that all tests have been completed.

## Deploy ##
Once your Consumer product has been assured it will be added to the NHSD Service Catalogue and you will be able to work with an NHS organisation to deliver the GP Connect API

Our developer ecosystem takes you through each stage of a typical GP Connect API project:
  
{% include developer_journey.html %}
