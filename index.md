---
title: Introduction to GP Connect API
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

In partnership with GP clinical system suppliers, GP Connect has developed a set of FHIR&reg; API specifications that make data from different clinical systems available to clinicians when and where they need it.

GP Connect supports the development of products that use the data made available by the APIs for direct care purposes.

## Audience ##
The content here is designed for a technical audience (that is, developers, technical architects and testers). For timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/services/gp-connect){:target="_blank"}.

We have identified three main types of customer:

#### Consumer supplier ####
*	you're a software development company already working with the NHS or would like to work with the NHS
*	you want to use GP Connect to develop a product that consumes GP data
* you intend to work with a suitable end-user organisation, which you may or may not have already identified

#### Provider supplier ####
*	you're a GP clinical system supplier or are working with the NHS to become one
*	you want to use GP Connect to enable other systems to access GP data on your system for direct patient care

Information of particular relevance to provider suppliers is indicated within the specification.

#### End-user organisation ####
*	you're a clinical commissioning group (CCG) with GP practices organised in a federation or Primary Care Network (PCN); you're a hospital or provider of emergency care or other care setting
*	you want to use an existing GP Connect API or commission a new, GP Connect-enabled system to access GP data from more than one GP clinical data provider to improve direct patient care

See [Getting involved with GP Connect](https://digital.nhs.uk/services/gp-connect/getting-involved-with-gp-connect#information-for-commissioning-or-end-user-organisations).

## About the FHIR&reg; API specifications ##

Each specification has a dual objective:
 
* to show consumer suppliers how to develop APIs for their applications so they can access clinical data
* to show provider suppliers how to develop APIs for their systems so they can share their clinical data

The specifications are arranged by version number and grouped into separate [capabilities](overview_priority_capabilities.html). To read about our versioning method, see [Specification versioning](design_product_versioning.html). To find out about other specifications, visit the [Specification directory](https://digital.nhs.uk/services/gp-connect/gp-connect-specifications-for-developers).

## Provide feedback ##
To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

{% include twitterfollow.html %}

{% include gitterbadge.html %}

&nbsp;
&nbsp;

<strong>Next steps:</strong>
- [Getting started for consumer suppliers](overview_getting_started_consumers.html)
- [Getting started for provider suppliers](overview_getting_started_providers.html)
