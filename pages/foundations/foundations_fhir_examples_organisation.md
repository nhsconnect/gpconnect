---
title: FHIR&reg; examples
keywords: foundations examples
tags: [design,foundations, organisation]
sidebar: foundations_sidebar
permalink: foundations_fhir_examples_organisation.html
summary: "Foundations - Organisation FHIR examples"
---

The following is a set of request/response examples for Foundations - Organisation

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Find an organisation</a></li>
    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Read an organisation</a></li>
  <!--    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li> -->
</ul>
<div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

<p style="line-height: 2; font-size: 20px">Find an organisation</p>

<p>Example of a search for an organisation by ODS organisation code:</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

```http
GET http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/Organization?https://fhir.nhs.uk/Id/ods-organization-code|A1001
```

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include foundations/find_organisation_response.json %}

</div>

<div role="tabpanel" class="tab-pane active" id="example2">

<p style="line-height: 2; font-size: 20px">Read an organisation</p>

<p>Example of a request to retrieve an organisation’s details</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

<div class="language-http highlighter-rouge"><div class="highlight"><pre class="highlight"><code class="hljs nginx"><span class="err"><span class="hljs-attribute">GET</span> http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/Organization/23</span></code></pre></div>    </div>


<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include foundations/read_organisation_response.json %}



</div>
</div>

