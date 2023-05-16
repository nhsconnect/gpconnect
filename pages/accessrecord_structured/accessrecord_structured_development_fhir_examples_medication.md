---
title: FHIR&reg; Medication examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_medication.html
summary: "Access Record Structured FHIR examples"
---

The following is a set of request/response examples for Medication:

<ul id="profileTabs" class="nav nav-tabs">
  <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Example 1</a></li>
<!--
  <li><a class="noCrossRef" href="#example2" data-toggle="tab">Example 2</a></li>
  <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li>
-->
</ul>

<div class="tab-content">
  <div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

  <p style="line-height: 2; font-size: 20px">Example 1</p>
  <p style="line-height: 1; font-size: 18px">Request</p>
  <p>Example of a call to return the following items from a patient's structured record:</p>
  <ul>
    <li>Medication</li>
    <li>Prescription Issues</li>
  </ul>
  <br>
  <p style="line-height: 1; font-size: 18px">Request payload</p>
  <p>Note: The <code class="highlighter-rouge">includePrescriptionIssues</code> parameter has explicitly been set to <code class="highlighter-rouge">true</code>.</p>
  {% include accessrecord_structured/meds_request.json %}
  <p style="line-height: 1; font-size: 18px">Response payload</p>
  {% include accessrecord_structured/meds_response.json %}

  </div>

  <div role="tabpanel" class="tab-pane" id="example2">
  <p style="line-height: 2; font-size: 20px">Example 2</p>
  <p style="line-height: 1; font-size: 18px">Request</p>
  <p>Example of a call to return the following items from a patient’s structured record:</p>
    <ul>
      <li>Medication</li>
    </ul>
  <p style="line-height: 1; font-size: 18px">Request payload</p>
  <p style="line-height: 1; font-size: 18px">Response payload</p>
  </div>

  <div role="tabpanel" class="tab-pane" id="example3">
  <p style="line-height: 2; font-size: 20px">Example 3</p>
  <p style="line-height: 1; font-size: 18px">Request</p>
  <p>Example of a call to return the following items from a patient’s structured record:</p>
    <ul>
      <li>Medication</li>
    </ul>
  <p style="line-height: 1; font-size: 18px">Request payload</p>
  <p style="line-height: 1; font-size: 18px">Response payload</p>
  </div>
</div>
