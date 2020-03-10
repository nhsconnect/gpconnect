---
title: FHIR&reg; examples
keywords: foundations examples
tags: [design,foundations, practitioner]
sidebar: foundations_sidebar
permalink: foundations_fhir_examples_practitioner.html
summary: "Foundations - Practitioner FHIR examples"
---

The following is a set of request/response examples for the Practitioner profile in the Foundations Capability

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Find a practitioner</a></li>
    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Read a practitioner</a></li>
  <!--    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li> -->
</ul>
<div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

<p style="line-height: 2; font-size: 20px">Find a practitioner</p>

<p>Example of a search for a practitioner by their Spine Directory Service user id</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

```http
GET http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/Practitioner?identifier=https://fhir.nhs.uk/Id/sds-user-id|111222333444
```

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include foundations/find_practitioner_response.json %}

</div>

<div role="tabpanel" class="tab-pane active" id="example2">

<p style="line-height: 2; font-size: 20px">Read a practitioner</p>

<p>Example of a request to retrieve a practitioner’s details</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

<div class="language-http highlighter-rouge"><div class="highlight"><pre class="highlight"><code class="hljs nginx"><span class="err"><span class="hljs-attribute">GET</span> http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/Practitioner/15</span></code></pre></div>    </div>

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include foundations/read_practitioner_response.json %}



</div>
</div>

