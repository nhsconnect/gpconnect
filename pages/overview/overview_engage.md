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
As an approximate guide you can expect to complete the following stages and tasks on your GP Connect development journey:

- Read about the GP Connect capabilities
- Study the prerequisites
- Contact GP Connect team
- Describe use case (purpose of your product)
- Obtain use case approval
- Contact GP Connect Consumer Assurance team
- Receive Supplier Conformance Assessment List (SCAL)
- Develop product
- Communication – ongoing communication with GP Connect
<p><strong>Assurance:</strong></p>
- Test against internet-facing demonstrator
- Test against OpenTest demonstrator
- Test against environment demonstrator in Integration (INT)
- Fill in and submit SCAL, incuding evidence of clinical safety
- Test against providers in INT
- Consumer receives technical conformance certificate
- Receive connection agreement
<p><strong>End-user engagement:</strong></p>
- Start of end-user group engagement with GP Connect (end-user group consists of, for example, practices that are sharing with a hospital)
- Data sharing agreement
- End-user group reviews SCAL
- End-user declaration signed
<p><strong>Deploy:</strong></p>
- Approval to Go Live
- Commissioner and Supplier Deployment Approach
- Go Live

<p></p>
<p>To get started, read the following pages:</p>

- read about the GP Connect [capabilities](overview_priority_capabilities.html)
- look through the design decisions made so far in relation to each capability ([Foundations](foundations_design.html), [Access Record Structured](accessrecord_structured_design.html) and [Appointment Management](appointments_design.html)) and get involved:
	- <span class="label label-success">SELECTED</span> / <span class="label label-info">DECISION</span> a decision has been made for first release.
	- <span class="label label-warning">ASSUMPTION</span> an assumption has been made which is under review/needs validated
- read the GP Connect [FHIR&reg; API guidance](development_fhir_api_guidance.html) common to all APIs

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

### Developer ecosystem ###

Our developer ecosystem diagram takes you through each stage of a consumer supplier journey for a typical GP Connect API project. Click on a stage to find out more.

{% include developer_journey.html %}

## Provider suppliers ##

Provider suppliers, such as EMIS Health, INPS Vision, Microtest Health or TPP, can use GP Connect to develop APIs that allow consumer applications to access GP data on their systems.

<p></p>
<p>To get started, read the following pages:</p>

- read about the GP Connect [capabilities](overview_priority_capabilities.html) within this specification
- see the latest specifications and release notes in the [specification directory](https://digital.nhs.uk/services/gp-connect/gp-connect-specifications-for-developers)
- read the [Spine integration overview](https://gpc-spec-restructure2.netlify.com/integration_overview.html)

### Provider ecosystem ###

The provider ecosystem diagram takes you through each stage of a provider supplier journey for a typical GP Connect API project. Click on a stage to find out more.

{% include provider_journey.html %}
