---
title: FHIR&reg; examples
keywords: structured design
tags: [design,structured]
sidebar: access_documents_sidebar
permalink: access_documents_development_fhir_examples_documents.html
summary: "Access Document FHIR examples"
---



The following is a set of request/response examples for Access Document:

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Search for a patient's documents</a></li>
    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Retrieve a document</a></li>
  <!--    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li> -->
</ul>
<div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

<p style="line-height: 2; font-size: 20px">Search for a patient's documents</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a search for a list of a patient's documents:</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

```http
GET http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/documents/Patient/04603d77-1a4e-4d63-b246-d7504f8bd833/DocumentReference?created=ge2019-06-24&_include=DocumentReference:subject:Patient&_include=DocumentReference:custodian:Organization&_include=DocumentReference:author:Organization&_include=DocumentReference:author:Practitioner&_revinclude:recurse=PractitionerRole:practitioner&author=https://fhir.nhs.uk/Id/sds-user-id|G13579135
```

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include access_documents/documents_response.json %}

</div>

<div role="tabpanel" class="tab-pane active" id="example2">

<p style="line-height: 2; font-size: 20px">Retrieve a document</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a request to retrieve a document:</p>



<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

<div class="language-http highlighter-rouge"><div class="highlight"><pre class="highlight"><code class="hljs nginx"><span class="err"><span class="hljs-attribute">GET</span> http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/documents/Binary/07a6483f-732b-461e-86b6-edb665c45510</span></code></pre></div>    </div>

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include access_documents/documents_response2.json %}



</div>
</div>
