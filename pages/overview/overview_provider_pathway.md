---
title: Clinical system supplier pathway
keywords: clinical, provider, pathway
tags: [provider,clinical]
sidebar: overview_sidebar
permalink: overview_provider_pathway.html
---

Under construction

Follow this pathway if you're a GP clinical data supplier,such as EMIS Health, INPS Vision,  Microtest Health, TPP, and you want to use GP Connect to develop a way of allowing other systems to access GP data on your system for direct patient care:

## 1. Get started ##

- read about the GP Connect [Priority capabilities](overview_priority_capabilities.html)
- look through the design decisions made so far in relation to each capability pack [Access Record HTML](accessrecord.html), [Access Record Structured](accessrecord_structured_design.html) and [Appointment Management](appointments_design.html) and get involved:
	- <span class="label label-success">SELECTED</span> / <span class="label label-info">DECISION</span> A decision has been made for first release.
	- <span class="label label-warning">ASSUMPTION</span> An assumption has been made which is under review/needs validated.

## 2. Develop ##

- familiarise yourself with HL7&reg; FHIR&reg; ([developer introduction](http://www.hl7.org/implement/standards/fhir/overview-dev.html){:target="_blank"}, [executive summary](http://www.hl7.org/implement/standards/fhir/summary.html){:target="_blank"}, or [clinical intro](http://www.hl7.org/implement/standards/fhir/overview-clinical.html){:target="_blank"})
- get an [open source FHIR development library](development_fhir_open_source_guidance.html) for your favourite programming language
- familiarise yourself with our GP Connect [FHIR API guidance](development_fhir_api_guidance.html) common to all APIs
- explore the GP Connect profiled FHIR resources, a variation of the international [FHIR resources](https://www.hl7.org/fhir/STU3/){:target="_blank"}, [Access Record HTML](accessrecord.html), [Access Record Structured](accessrecord_structured_development_resources_overview.html), and [Appointment Management](datalibraryappointment.html)
- explore one or more of the GP Connect capability packs
  - [Access Record HTML](accessrecord.html) (for example, access HTML views from the primary care record)
  - [Access Record Structured](accessrecord_structured.html) (for example, access structured data from the primary care record)
  - [Appointment Management](appointments.html) (for example, book an appointment for a patient)
- Finally take a look at cross-cutting areas:
  - JSON Web Token - provides [cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html) details
  - Additional HTTP headers and proxy URL - This gives you access to the [Spine Secure Proxy](integration_spine_secure_proxy.html), the secure 'front door' of GP Connect APIs.
  - configure HTTPS and TLS/MA - [Security guidance](development_api_security_guidance.html) allows you to secure and mutually authenticate your service with the Spine (which refers to two parties authenticating each other at the same time) 

## 3. Test and assure ##

- read about the [provider testing](testing_api_provider_testing.html)

## Provide feedback

To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

## Community engagement

GP Connect is working closely with [INTEROPen](http://www.interopen.org/){:target="_blank"}, a healthcare IT interoperability community of suppliers, NHS organisations and healthcare standards bodies in the UK.

## Timescales, benefits and more

The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/article/1275/GP-Connect){:target="_blank"}.

Our developer ecosystem takes you through each stage of a typical GP Connect API project:
  
{% include developer_journey.html %}

![Clinical supplier ecosystem](images/overview/clinical_supplier_ecosystem.png)
