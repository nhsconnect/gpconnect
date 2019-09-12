---
title: Introduction - what is GP Connect?
keywords: homepage
tags: [introduction]
sidebar: home_sidebar
permalink: index.html
toc: false
summary: An introduction to the GP Connect FHIR® APIs
---

{% comment %}
[![Semver](http://img.shields.io/badge/semver-2.0.0-yellow.svg)](http://semver.org/spec/v2.0.0.html){:target="_blank" class="no_icon"} [![License](http://img.shields.io/:license-apache2-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html){:target="_blank" class="no_icon"} 
{% endcomment %}

GP Connect is a service that can allow authorised clinical staff in GP practices and other care settings to share GP practice clinical information and data between IT systems, quickly and efficiently. This ensures patient medical information is available to clinicians when and where they need it, improving patient care.

<p>GP Connect is developing standardised {% include tooltip.html type="API" %} specifications to be used by any system for the sharing of data, so that clinicians in different care settings can:</p>

* view a patient’s GP practice record
* import or download medication and allergies information from this record 
*	manage a patient's GP appointments

This will provide better, safer, more convenient care for patients and save time for clinicians. It will also help meet targets under [NHS England’s improving access to general practice programme](https://www.england.nhs.uk/gp/gpfv/redesign/improving-access/).

## GP Connect overview ##

![Img](images/overview/GP Connect Model.png)

## GP Connect APIs and capabilities ##
The APIs are grouped into sets, known as 'capabilities', which enable specific business functionality. GP Connect has worked with GP clinical system suppliers to deliver the following capabilities:

*	Access Record HTML – enables clinicians to view a patient’s medical record
*	Appointment Management – enables clinical staff to book, amend or cancel an appointment for a patient
*	Access Record Structured – enables an export of a patient’s medications and allergies 

[Find out more about the capabilities](/overview_priority_capabilities.html)

## Pilot using the GP Connect APIs ##
The GP Connect programme is now supporting the development of systems that connect with the APIs to use data from patient records and appointment schedulers for patient care by integrating it or importing it into local clinical systems.

We’re working with selected partnerships of health and care organisations and software suppliers. Partnerships will use the APIs to develop technical solutions to local issues with sharing patient records and appointment booking across system boundaries.
We’ve developed a process called ‘First of Type’ to support this development and provide assurance for these early products.

[Getting involved with GP Connect](https://digital.nhs.uk/services/gp-connect)

## Developer ecosystem

Our developer ecosystem takes you through each stage of a typical GP Connect API project. Click on a stage to find out more.
  
{% include developer_journey.html %}

{% include important.html content="This site is under active development by the GP Connect team and is intended to provide all the technical resources you need to successfully develop GP Connect provider APIs or consuming applications. Some areas are being formulated and iterative updates to content will be added on a regular basis. See our GitHub [releases page](https://github.com/nhsconnect/gpconnect/releases) for more information." %}

{% include warning.html content="This site is provided for information only and is intended for those engaged with NHS Digital in First of Type activities. Other parties are advised not to develop against these specifications until a formal announcement has been made." %}

## Community engagement ##

GP Connect is working closely with [INTEROPen](http://www.interopen.org/){:target="_blank"}, a healthcare IT interoperability community of suppliers, NHS organisations and healthcare standards bodies in the UK.

## Provide feedback ##

To provide feedback on the GP Connect specification, send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

## The Open API ecosystem

GP Connect is part of a wider initiative to expose standards based on [Open APIs](designprinciples_open_api_principles.html#open-api){:target="_blank"} to promote innovation and improve care across the NHS.

## INTEROPen

GP Connect FHIR profiles specified within this site have been developed by NHS Digital and where available use Care Connect profiles created in collaboration with the INTEROPen community.

The INTEROPen vision is to create a library of nationally defined HL7® FHIR® resources and interaction patterns that implementers can adopt to simplify integration and interoperability within England’s health and social care systems. Find out more on the [INTEROPen website](https://www.interopen.org/).

## Timescales, benefits and more

The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/article/1275/GP-Connect){:target="_blank"}.

{% include twitterfollow.html %}

{% include gitterbadge.html %}

## Next step ##
[Get started](/overview_engage.html)
