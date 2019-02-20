---
title: Getting started for consumer suppliers
keywords: consumer
tags: [consumer]
sidebar: overview_sidebar
permalink: overview_consumer_supplier.html
toc: false
pathways: [consumer]
summary: Step-by-step guide to developing consumer applications
---

<p>As a consumer supplier, you want to use GP Connect to develop an API to consume GP data. To retrieve data from an end-user organisation, your system will need to integrate with the {% include tooltip.html type="Spine" %} as follows:</p>

![Img](images/overview/gp_connect_apis.png)
<p>
##Step by step:##
<p>1. Make a request to the {% include tooltip.html type="PDS" %} to retrieve patient's registered practice.</p>
<p>2. Make a call to {% include tooltip.html type="SDS" %} to retrieve provider endpoint information.</p>
<p>3. Using the endpoint information retrieved in step 2, make a request via {% include tooltip.html type="SSP" %} to the provider.</p>
<p>4. SSP passes request to provider system.</p>
<p>5. Provider returns data to SSP.</p>
<p>6. SSP passes data to consumer.</p>

For more details on consumer request interactions, see the [SSP implementation guide](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html).

## Things to consider
- XML vs JSON
- toolkits
- developer tools: demonstrator, postman
- code samples
- understanding FHIR
- read about the GP Connect [priority capabilities](overview_priority_capabilities.html).
- look through the design decisions made so far in relation to each capability pack ([Foundations](foundations_design.html), [Access Record HTML](accessrecord.html), [Access Record Structured](accessrecord_structured_design.html) and [Appointment Management](appointments_design.html) and get involved:
	- <span class="label label-success">SELECTED</span> / <span class="label label-info">DECISION</span> A decision has been made for first release.
	- <span class="label label-warning">ASSUMPTION</span> An assumption has been made which is under review/needs validated.

## Developer ecosystem
Our developer ecosystem takes you through each stage of a typical GP Connect API project:
  
{% include developer_journey.html %}

## Provide feedback

To provide feedback on the GP Connect specification please send an email to the [GP Connect Team Inbox](mailto://gpconnect@nhs.net).

Some early feedback on the May 2016 release of the GP Connect draft specification can be found on the [OpenHealthHub forum](https://www.openhealthhub.org/c/fhir-implementation){:target="_blank"} under the category of "FHIR Implementation".

## Community engagement

### The Open API ecosystem

GP Connect is part of a wider initiative to expose standards based [Open APIs](designprinciples_open_api_principles.html#open-api){:target="_blank"} to promote innovation and improve care across the NHS.

### INTEROPen

GP Connect FHIR profiles specified within this site have been developed by NHS Digital and where available use CareConnect profiles created in collaboration with the INTEROPen community.

The INTEROPen vision is to create a library of nationally defined HL7® FHIR® resources and interaction patterns that implementers can adopt to simplify integration and interoperability within England’s health and social care systems. Find out more on the [INTEROPen website](https://www.interopen.org/)

## Timescales, benefits and more

The content here is designed for a technical audience (that is, developers, architects and data scientists). For other details, such as the vision, timescales, business benefits and case studies, please see the [NHS Digital GP Connect homepage](https://digital.nhs.uk/article/1275/GP-Connect){:target="_blank"}.

## Next step ##
[Explore](/overview_explore.html)
