---
title: FHIR&reg; examples
keywords: foundations examples
tags: [design,foundations, patient]
sidebar: foundations_sidebar
permalink: foundations_fhir_examples_patient.html
summary: "Foundations - Patient FHIR examples"
---


The following is a set of request/response examples for the Patient profile in the Foundations Capability

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Find a patient</a></li>
    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Read a patient</a></li>
  <!--    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li> -->
</ul>
<div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

<p style="line-height: 2; font-size: 20px">Find a patient</p>

<p>Example of a search for a patient by their NHS Number</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

```http
GET 
http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/Patient?identifier=https://fhir.nhs.uk/Id/nhs-number|9476719931
```

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include foundations/find_patient_response.json %}

</div>

<div role="tabpanel" class="tab-pane active" id="example2">

<p style="line-height: 2; font-size: 20px">Read a patient</p>

<p>Example of a request to retrieve a patient’s details</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

```http
GET 
http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/Patient/2
```

```http
GET 
http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/Patient?identifier=https://fhir.nhs.uk/Id/nhs-number|9476719931
```

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include foundations/read_patient_response.json %}



</div>
</div>

