---
title: Getting started for consumer suppliers
keywords: consumer
tags: [consumer]
sidebar: overview_sidebar
permalink: overview_consumer_supplier.html
toc: false
summary: Step-by-step guide to developing consumer applications
---

**Under construction**

As a {% include tooltip.html type="Consumer supplier" %}, you want to use GP Connect to develop an API to consume GP data. You intend to work with a suitable end-user organisation, which you may or may not have already identified.

{% include tooltip.html type="Consumer supplier" %}

<p> {% include tooltip.html type="Consumer supplier" %}

This page guides you through the development process, 


- Read about the GP Connect [priority capabilities](overview_priority_capabilities.html).
- Look through the design decisions made so far in relation to each capability pack ([Foundations](foundations_design.html), [Access Record HTML](accessrecord.html), [Access Record Structured](accessrecord_structured_design.html) and [Appointment Management](appointments_design.html) and get involved:
	- <span class="label label-success">SELECTED</span> / <span class="label label-info">DECISION</span> A decision has been made for first release.
	- <span class="label label-warning">ASSUMPTION</span> An assumption has been made which is under review/needs validated.

## Explore ## 

- Use the [GP Connect system demonstrator](system_demonstrator.html) to explore GP Connect functionality, and access the Personal Demographics Service (PDS) and the Spine Directory Service (SDS) without an HSCN connection..
- Optionally download the [GP Connect demonstrator codebase](https://github.com/nhs-digital/gpconnect){:target="_blank"} to see how it works. 
- Download our [PostMan collection](system_reference_postman.html) and explore the GP Connect interactions.

## Develop ##

- Familiarise yourself with HL7&reg; FHIR&reg; ([developer introduction](http://www.hl7.org/implement/standards/fhir/overview-dev.html){:target="_blank"}, [executive summary](http://www.hl7.org/implement/standards/fhir/summary.html){:target="_blank"}, or [clinical intro](http://www.hl7.org/implement/standards/fhir/overview-clinical.html){:target="_blank"}).
- Grab an [open source FHIR development library](development_fhir_open_source_guidance.html) for your favourite programming language.
- Decide which wire format to use (JSON or XML)
{% include important.html content="Consumers planning their development should read [the following information](support_faq.html#which-serialisation-format-should-i-choose-as-an-gp-connect-api-consumer---json-or-xml) before choosing whether to use JSON or XML in their implementation." %}
- Familiarise yourself with our GP Connect [FHIR API guidance](development_fhir_api_guidance.html) common to all APIs.
- Explore the GP Connect profiled FHIR resources, a variation of the international [FHIR resources](https://www.hl7.org/fhir/STU3/){:target="_blank"}, for [Foundations](datalibraryfoundation.html), [Access Record HTML](accessrecord.html), [Access Record Structured](accessrecord_structured_development_resources_overview.html), and [Appointment Management](datalibraryappointment.html).
- Explore one or more of the GP Connect capability packs and start building new or hitting existing APIs.
  - [Access Record HTML](accessrecord.html) (e.g. Access html views from the primary care record).
  - [Access Record Structured](accessrecord_structured.html) (e.g. Access structured data from the primary care record).
  - [Appointment Management](appointments.html) (e.g. Book an appointment for a patient).
- Take a look at cross-cutting areas:
  - JSON Web Token - provides [cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html) details
  - additional HTTP headers and proxy URL - this gives you access to the [Spine Secure Proxy](integration_spine_secure_proxy.html), the secure 'front door' of GP Connect APIs.
  - configure HTTPS and TLS/MA - [security guidance](development_api_security_guidance.html) allows you to secure and mutually authenticate your service with the Spine (which refers to two parties authenticating each other at the same time). 

## Assure ##

Consumer APIs need to go through a set of testing and assurance processes to ensure they are robust enough to meet the demands of busy NHS organisations. You will need to provide evidence that all tests have been completed.

- Read about the [Provider testing](testing_api_provider_testing.html) and [Consumer testing](testing_api_consumer_testing.html) process.

## Deploy ##

Once your consumer product has been assured it will be added to the NHSD Service Catalogue and you will be able to work with an NHS organisation to deliver the GP Connect API.

- Become a first of type deployment - see below to get in touch with the GP Connect programme.

Our developer ecosystem takes you through each stage of a typical GP Connect API project:
  
{% include developer_journey.html %}
