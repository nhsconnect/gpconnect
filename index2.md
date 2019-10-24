---
title: Introduction
keywords: homepage
tags: [introduction]
sidebar: home_sidebar
permalink: index2.html
toc: false
summary: An introduction to the GP Connect FHIR® APIs
---

{% comment %}
[![Semver](http://img.shields.io/badge/semver-2.0.0-yellow.svg)](http://semver.org/spec/v2.0.0.html){:target="_blank" class="no_icon"} [![License](http://img.shields.io/:license-apache2-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html){:target="_blank" class="no_icon"} 
{% endcomment %}

GP Connect is a service that allows GP practices and authorised clinical staff to share and view GP practice clinical information and data between IT systems, quickly and efficiently.

The GP Connect programme is supporting the development of products which will enable different systems to communicate so that clinicians in different care settings can:

* view a patient’s GP practice record
* import or download medication and allergies information
*	manage a patient's GP appointments

GP Connect is developing standardised {% include tooltip.html type="API" %} specifications to be used by any system for the sharing of data.


## Capabilities ##

The APIs are grouped into sets, known as 'capabilities', which enable specific business functionality. GP Connect has worked with GP clinical system suppliers to deliver the following capabilities:

*	Access Record HTML – enables clinicians to view a patient’s medical record
*	Appointment Management – enables clinical staff to book, amend or cancel an appointment for a patient
*	Access Record Structured – enables an export of a patient’s medications and allergies 

[Find out more about the capabilities](/overview_priority_capabilities.html)

## Using this specification ##

This specification has been created to support the adoption of GP Connect APIs and FHIR&reg; resources. As such, the site is structured around GP Connect stakeholders including API users, developers and architects.  

{% include custom/api_overview.svg %}

The above steps outline a complete API journey from imagination and exploring to developing apps using GP Connect APIs all the way to deploying a live API.

## Pilot using the GP Connect APIs ##
The GP Connect programme is now supporting the development of systems that connect with the APIs to use data from patient records and appointment schedulers for patient care by integrating it or importing it into local clinical systems.

We’re working with selected partnerships of health and care organisations and software suppliers. Partnerships will use the APIs to develop technical solutions to local issues with sharing patient records and appointment booking across system boundaries.
We’ve developed a process called ‘First of Type’ to support this development and provide assurance for these early products.

[Getting involved with GP Connect](https://digital.nhs.uk/services/gp-connect)

## Community engagement ##
GP Connect is working closely with [INTEROPen](http://www.interopen.org/){:target="_blank"}, a healthcare IT interoperability community of suppliers, NHS organisations and healthcare standards bodies in the UK.

## Timescales, benefits and more
The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/article/1275/GP-Connect){:target="_blank"}.

## Provide feedback ##
To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

{% include twitterfollow.html %}

{% include gitterbadge.html %}
