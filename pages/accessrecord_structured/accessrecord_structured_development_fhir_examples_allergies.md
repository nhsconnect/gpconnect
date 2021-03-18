---
title: FHIR&reg; Allergies examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_allergies.html
summary: "Access Record Structured FHIR examples"
---



The following is a set of request/response examples for Allergies:

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Example 1</a></li>
    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Example 2</a></li>
    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li>
</ul>
  <div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

<p style="line-height: 2; font-size: 20px">Example 1</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient's structured record:</p>

<ul>
  <li>Allergies</li>
  <li>Resolved allergies</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/allergies_request1.json %}


<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include accessrecord_structured/allergies_response1.json %}


</div>

<div role="tabpanel" class="tab-pane" id="example2">

<p style="line-height: 2; font-size: 20px">Example 2</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient’s structured record:</p>

<ul>
  <li>Allergies</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/allergies_request2.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

<p>Assumes - ‘No Known Allergies’ has been positively asserted on record and is not contradicted by presence of active allergies on record.</p>

{% include accessrecord_structured/allergies_response2.json %}

</div>

<div role="tabpanel" class="tab-pane" id="example3">

<p style="line-height: 2; font-size: 20px">Example 3</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient’s structured record:</p>

<ul>
  <li>Allergies</li>
</ul>

<br>
<p style="line-height: 1; font-size: 18px">Request payload</p>

{% include accessrecord_structured/allergies_request3.json %}

<p style="line-height: 1; font-size: 18px">Response payload</p>

<p>Assumption - ‘No Known Allergies’ has not been positively asserted on record, but is not contradicted by presence of active allergies on record.</p>

{% include accessrecord_structured/allergies_response3.json %}

</div>
</div>
