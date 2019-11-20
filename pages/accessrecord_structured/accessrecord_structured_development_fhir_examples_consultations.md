---
title: FHIR&reg; Consultations and Problems examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_consultations.html
summary: "Access Record Structured FHIR examples"
---



The following is a set of request/response examples for Consultations and problems:

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Example 1</a></li>
<!--    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Example 2</a></li>
    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li> -->
</ul>

<div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1">

<p style="line-height: 2; font-size: 20px">Example 1</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient's structured record:</p>

<ul>
  <li>Consultations</li>
  <li>Problems</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/consultations_request1.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

The response payload is available as a json file by clicking on the link below. The first consultation in the example is in line with the diagram on the consultation guidance page. It also contains a further two consultations which are described in the spreadsheet that can be downloaded using the link below.

<br>

<a href="_includes/accessrecord_structured/consultations_response1.json">Response payload</a>

<br>

<a href="pages/accessrecord_structured/Consultations and problems example details.xlsx">Spreadsheet description of example</a>

</div>
<!--
<div role="tabpanel" class="tab-pane" id="example2">

<p style="line-height: 2; font-size: 20px">Example 2</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient’s structured record:</p>

<ul>
  <li>Consultations</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/consultations_request2.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include accessrecord_structured/consultations_response2.json %}


</div>

<div role="tabpanel" class="tab-pane" id="example3">

<p style="line-height: 2; font-size: 20px">Example 3</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient’s structured record:</p>

<ul>
  <li>Consultations</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/consultations_request3.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include accessrecord_structured/consultations_response3.json %}


</div> -->
</div>
