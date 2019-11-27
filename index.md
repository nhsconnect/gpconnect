---
title: Introduction
keywords: homepage
tags: [introduction]
sidebar: overview_sidebar
permalink: index.html
toc: false
summary: An introduction to the GP Connect FHIR® APIs
---

{% comment %}
[![Semver](http://img.shields.io/badge/semver-2.0.0-yellow.svg)](http://semver.org/spec/v2.0.0.html){:target="_blank" class="no_icon"} [![License](http://img.shields.io/:license-apache2-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html){:target="_blank" class="no_icon"} 
{% endcomment %}

In partnership with principal GP clinical system suppliers, GP Connect has developed a set of FHIR&reg; API specifications that make data from different clinical systems available to clinicians when and where they need it.

GP Connect supports the development of products that use the clinical data made available by our APIs.

## Community engagement ##
GP Connect is working closely with [INTEROPen](http://www.interopen.org/){:target="_blank"}, a healthcare IT interoperability community of suppliers, NHS organisations and healthcare standards bodies in the UK.

## Timescales, benefits and more
The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/services/gp-connect){:target="_blank"}.

## FHIR&reg; API specifications ##

Each specification has a dual objective:

* to show consumer suppliers how to connect to the APIs from their applications
* to show provider suppliers how to develop APIs that connect to their clinical data

The specifications are arranged by version number and grouped into separate capabilities, so that authorised users in different care settings can, for example:  

* view a patient’s GP practice record
*	manage GP appointments
* import or download medication and allergies information

The specification you are currently reading has [these capabilities](overview_priority_capabilities.html).

To find out about other specifications, visit the [specification directory](https://digital.nhs.uk/services/gp-connect/gp-connect-specifications-for-developers).

## Audience ##
We have identified three main customer types:

#### Consumer supplier ####
*	You're a software development company already working with the NHS or would like to work with the NHS.
*	You want to use GP Connect to develop an API to consume GP data. You intend to work with a suitable end-user organisation, which you may or may not have already identified.

See [Getting started](overview_engage.html).

#### Provider supplier ####
*	You're a GP clinical data supplier, such as EMIS Health, INPS Vision, Microtest Health and TPP.
*	You want to use GP Connect to enable other systems to access GP data on your system for direct patient care.

See [Getting started](overview_engage.html).

#### End-user organisation ####
*	You're a clinical commissioning group (CCG) with GP practices organised in a federation or hub; you're a hospital or provider of emergency care or other care setting.
*	You want to use an existing GP Connect API or commission a new, GP Connect-enabled system to access GP data from more than one GP clinical data provider to improve direct patient care.

See [Getting involved with GP Connect](https://digital.nhs.uk/services/gp-connect/getting-involved-with-gp-connect#information-for-commissioning-or-end-user-organisations).

## Development ecosystem ##

Our developer ecosystem takes you through each stage of a typical GP Connect API project. Click on a stage to find out more.

{% include developer_journey.html %}

## Provide feedback ##
To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

{% include important.html content="This site is under active development by the GP Connect team and is intended to provide all the technical resources you need to successfully develop GP Connect provider APIs or consuming applications. Some areas are being formulated and iterative updates to content will be added on a regular basis. See our GitHub [releases page](https://github.com/nhsconnect/gpconnect/releases) for more information." %}

{% include twitterfollow.html %}

{% include gitterbadge.html %}
