---
title: Getting started
keywords: engage, about
tags: [getting_started]
sidebar: overview_sidebar
toc: false
permalink: overview_engage.html
summary: "Getting started with GP Connect"
---

## Consumer suppliers ##

- read about the GP Connect [capabilities](overview_priority_capabilities.html)
- look through the design decisions made so far in relation to each capability ([Foundations](foundations_design.html), [Access Record Structured](accessrecord_structured_design.html) and [Appointment Management](appointments_design.html)) and get involved:
	- <span class="label label-success">SELECTED</span> / <span class="label label-info">DECISION</span> a decision has been made for first release.
	- <span class="label label-warning">ASSUMPTION</span> an assumption has been made which is under review/needs validated
- read the GP Connect [FHIR&reg; API guidance](development_fhir_api_guidance.html) common to all APIs

## Consumer supplier pathway ##

- Read about the GP Connect capabilities
- Study the prerequisites
- Contact GP Connect Consumer Assurance team
- Describe use case (purpose of your product)
- Obtain use case approval
- Receive Supplier Conformance Assessment List (SCAL)
- Develop product
- Communication – ongoing communication with GP Connect
- Assurance:
1 Test against internet-facing demonstrator
2 Test against OpenTest demonstrator
3 Test against environment demonstrator in Int
4 Fill in SCAL
5 Test against providers in Int
- Receive technical conformance certificate
- Receive connection agreement
- End-user engagement:
1 End-user portal
2 Data sharing agreement
3 SCAL review
4 End-user declaration signed  (Speak to Sharon and Rebecca)
- Deploy:
1 Approval to Go Live
2 Commissioner and Supplier Deployment Approach
3 Go Live

### Integration with Spine ###

<p>Consumer suppliers can develop applications that use GP Connect {% include tooltip.html type="FHIR&reg;" %} {% include tooltip.html type="API" %} specifications to consume GP data. To retrieve data from an end-user organisation, your application will need to integrate with the {% include tooltip.html type="Spine" %} as follows:</p>

![Img](images/overview/gp_connect_apis.png)

**Step by step:**
<p>1. Make a request to the {% include tooltip.html type="PDS" %} to retrieve patient's registered practice.</p>
<p>2. Make a call to {% include tooltip.html type="SDS" %} to retrieve provider endpoint information.</p>
<p>3. Using the endpoint information retrieved in step 2, make a request via {% include tooltip.html type="SSP" %} to the provider.</p>
<p>4. {% include tooltip.html type="SSP" %} passes request to provider system.</p>
<p>5. Provider returns data to {% include tooltip.html type="SSP" %}.</p>
<p>6. {% include tooltip.html type="SSP" %} passes data to consumer.</p>

For more details on consumer request interactions, see the [SSP implementation guide](https://developer.nhs.uk/apis/spine-core-1-0/ssp_implementation_guide.html).

## Provider suppliers ##

Provider suppliers, such as EMIS Health, INPS Vision, Microtest Health or TPP, can use GP Connect to develop APIs that allow consumer applications to access GP data on their systems.

- read about the GP Connect [capabilities](overview_priority_capabilities.html) within this specification
- see the latest specifications and release notes in the [specification directory](https://digital.nhs.uk/services/gp-connect/gp-connect-specifications-for-developers)

## Developer ecosystem ##

Our developer ecosystem diagram takes you through each stage of a consumer supplier journey for a typical GP Connect API project. Click on a stage to find out more.

{% include developer_journey.html %}

