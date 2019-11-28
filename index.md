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

## About the FHIR&reg; API specifications ##

Each specification has a dual objective:
 
* to show consumer suppliers how to connect to the APIs from their applications
* to show provider suppliers how to develop APIs that connect to their clinical data

The specifications are arranged by version number and grouped into separate [capabilities](overview_priority_capabilities.html), for example:  

* Access Record HTML - provides a read-only view of a patient’s GP practice record 
*	Appointment Management - allows the management of GP practice appointments between different systems
* Access Record Structured - enables structured, machine-readable information to be retrieved from the patient’s GP practice record (including medication and allergies) 

The capabilities available in each specification are shown in the yellow, version box at the top of each page. To find out about other specifications, visit the [specification directory](https://digital.nhs.uk/services/gp-connect/gp-connect-specifications-for-developers).

## Audience ##
The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/services/gp-connect){:target="_blank"}.

We have identified three main types of customer:

#### Consumer supplier ####
*	you're a software development company already working with the NHS or would like to work with the NHS
*	you want to use GP Connect to develop a product that consumes GP data
* you intend to work with a suitable end-user organisation, which you may or may not have already identified

Our developer ecosystem takes you through each stage of a consumer supplier journey for a typical GP Connect API project. Click on a stage to find out more.

{% include developer_journey.html %}

#### Provider supplier ####
*	you're a GP clinical data supplier, such as EMIS Health, INPS Vision, Microtest Health and TPP
*	you want to use GP Connect to enable other systems to access GP data on your system for direct patient care

Information of particular relevance to provider suppliers is indicated within the specification.

#### End-user organisation ####
*	you're a clinical commissioning group (CCG) with GP practices organised in a federation or hub; you're a hospital or provider of emergency care or other care setting
*	you want to use an existing GP Connect API or commission a new, GP Connect-enabled system to access GP data from more than one GP clinical data provider to improve direct patient care

See [Getting involved with GP Connect](https://digital.nhs.uk/services/gp-connect/getting-involved-with-gp-connect#information-for-commissioning-or-end-user-organisations).

## Community engagement ##
GP Connect is working closely with [INTEROPen](http://www.interopen.org/){:target="_blank"}, a healthcare IT interoperability community of suppliers, NHS organisations and healthcare standards bodies in the UK.

## Provide feedback ##
To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

{% include twitterfollow.html %}

{% include gitterbadge.html %}
