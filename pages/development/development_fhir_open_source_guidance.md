---
title: FHIR&reg; library
keywords: fhir, development, open source
tags: [fhir,development]
sidebar: overview_sidebar
permalink: development_fhir_open_source_guidance.html
summary: "There are benefits to using an existing FHIR&reg; library"
toc: false
---

## Using an existing FHIR&reg; library ##

GP Connect strongly advises suppliers to use an existing FHIR library as it will reduce development time and result in more robust implementations of the GP Connect API. Benefits of using an existing FHIR library for the implementation of both the consumer and provider side of a GP Connect API are:

* ***Reduced complexity*** - using a library can reduce the quantity of boilerplate code required to configure provider endpoints, structure a request and validate consumed resources. This will help keep the code base smaller, and make it easier to work on and maintain.
* ***Quicker development*** - a library gives developers the standard FHIR data types, FHIR resources and some validation of the FHIR resources, allowing developers to focus on data transformation and business rules.
* ***Solution resilience*** - using a tried and tested implementation of the FHIR resources and data types should result in the implementation being more resilient to receiving valid but unexpected elements within FHIR resources. Many libraries will also include some level of validation to aid in ensuring that only valid data enters the system.


## What libraries to use? ##

There is an ever-increasing list of open source FHIR libraries appearing on the web, written for a wide variety of languages, such as Java, C#.NET, JavaScript and PHP. As a starting point, the Health Level Seven (HL7&reg;) International standards body maintains a list of open source FHIR implementations on its [Wiki](http://wiki.hl7.org/index.php?title=Open_Source_FHIR_implementations) page.

{% include tip.html content="It's a good idea to give feedback into open source FHIR library projects to improve the implementations and  increase the maturity of the technologies for everyone's benefit." %}

In addition to open source FHIR libraries, many widely used health software systems now support FHIR as a standard message type, which means some consumers and providers may be able to create a GP Connect interface with extensions available on their current system.

**Please refer to the Spine Core FHIR API Framework for details of open source [FHIR client libraries](https://developer.nhs.uk/apis/spine-core-1-0/explore_fhir_open_source_guidance.html#1-open-source-fhir-libraries) and open source [FHIR reference servers](https://developer.nhs.uk/apis/spine-core-1-0/explore_fhir_open_source_guidance.html#2-open-source-fhir-reference-servers) available for use.**

{% include important.html content="The FHIR clients above allow serialisation in both JSON and XML; however, consumers planning their development should read [the following information](support_faq.html#which-serialisation-format-should-i-choose-as-an-gp-connect-api-consumer---json-or-xml) before setting the serialisation format (JSON or XML) in their chosen FHIR library." %}
