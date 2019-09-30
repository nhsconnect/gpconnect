---
title: FHIR&reg; Consultations examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_forwards_consultations.html
summary: "Access Record Structured FHIR examples"
---



The following is an example of a request/response where a consumer using version 1.3.0 of this specification attempts to request consultations, problems, medications and allergies from a provider who has implemented version 1.2.3 of the GP Connect API:

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Example 1</a></li>
</ul>

<div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1">

<p style="line-height: 2; font-size: 20px">Example 1</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient's structured record:</p>

<ul>
  <li>Consultations</li>
  <li>Problems</li>
  <li>Medications</li>
  <li>Allergies</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/consultations_forwards_request1.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include accessrecord_structured/consultations_forwards_response1.json %}

Note the inclusion of an OperationOutcome with two issues about the unsupported parameters, includeConsultations and includeProblems.


</div>

</div>
