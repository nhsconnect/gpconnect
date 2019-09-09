---
title: Develop with GP Connect
keywords: develop
tags: [development]
sidebar: overview_sidebar
toc: false
pathways: [consumer,provider]
permalink: overview_development.html
summary: Start building applications that use GP Connect to consume or expose data
---

**Introductory text to be provided by Jonny....**

- Develop a capability
- Integrate with Spine
- Implement the JWT
- Configure the TLS

## Consumer suppliers ##

- familiarise yourself with HL7&reg; FHIR&reg; ([developer introduction](http://www.hl7.org/implement/standards/fhir/STU3/overview-dev.html){:target="_blank"}, [executive summary](http://www.hl7.org/implement/standards/fhir/STU3/summary.html){:target="_blank"}, or [clinical intro](http://www.hl7.org/implement/standards/fhir/STU3/overview-clinical.html){:target="_blank"})
- grab an [open source FHIR development library](development_fhir_open_source_guidance.html) for your favourite programming language
- decide which wire format to use (JSON or XML)
{% include important.html content="Consumers planning their development should read [the following information](support_faq.html#which-serialisation-format-should-i-choose-as-an-gp-connect-api-consumer---json-or-xml) before choosing whether to use JSON or XML in their implementation." %}
- familiarise yourself with our GP Connect [FHIR API guidance](development_fhir_api_guidance.html) common to all APIs
- explore the GP Connect profiled FHIR resources, a variation of the international [FHIR resources](https://www.hl7.org/fhir/STU3/){:target="_blank"}, for [Foundations](datalibraryfoundation.html), [Access Record HTML](datalibraryaccessRecord.html), and [Appointment Management](datalibraryappointment.html).
- dig in deep and explore one or more of the GP Connect capability packs and start building new or hitting existing APIs
  - [Foundations](foundations.html) (for example, resolve a patient to their logical identifier for further API calls)
  	- note the foundation per-requisites are mandatory and may restrict your ability to utilise the GP Connect APIs
  - [Access Record HTML](accessrecord.html) (for example, access HTML views from the primary care record)
  - [Access Record REST](accessrecord_rest.html) (for example, access structured data from the primary care record)
  - [Appointment Management](appointments.html) (for example, book an appointment for a patient)
  - [Task Management](tasks.html) (for example, send a notification task to a general practice organisation)
- finally take a look at cross-cutting areas:
  - JSON Web Token - provides [cross-organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html) details
  - additional HTTP headers and proxy URL - this gives you access to the [Spine Security Proxy](integration_spine_security_proxy.html), the secure 'front door' of GP Connect APIs
  - configure HTTPS and TLS/MA - [security guidance](development_api_security_guidance.html) allows you to secure and mutually authenticate your service with the Spine (which refers to two parties authenticating each other at the same time) 
  
## Clinical system suppliers ##
* Text to be added - development actions required by providers *

## Next step ##
[Test and assure](/overview_test_and_assurance.html)

