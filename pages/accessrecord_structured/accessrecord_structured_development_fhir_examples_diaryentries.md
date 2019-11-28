---
title: FHIR&reg; (Diary Entry) ProcedureRequest examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_diaryentries.html
summary: "Access Record Structured FHIR examples"
---



The following is a set of request/response examples for (Diary Entry) ProcedureRequest:

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
  <li>(Diary Entry) ProcedureRequest</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/diaryentries_request1.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include accessrecord_structured/diaryentries_response1.json %}


</div>
<!--
<div role="tabpanel" class="tab-pane" id="example2">

<p style="line-height: 2; font-size: 20px">Example 2</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient’s structured record:</p>

<ul>
  <li>Immunizations</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/immunizations_request2.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include accessrecord_structured/immunizations_response2.json %}


</div>

<div role="tabpanel" class="tab-pane" id="example3">

<p style="line-height: 2; font-size: 20px">Example 3</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient’s structured record:</p>

<ul>
  <li>Immunizations</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/immunizations_request3.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include accessrecord_structured/immunizations_response3.json %}


</div> -->
</div>
