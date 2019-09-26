---
title: FHIR&reg; Documents examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_documents_development_fhir_examples_documents.html
summary: "Access Record Documents FHIR examples"
---



The following is a set of request/response examples for Documents:

<ul id="profileTabs" class="nav nav-tabs">
    <li class="active"><a class="noCrossRef" href="#example1" data-toggle="tab">Example 1</a></li>
<!--    <li><a class="noCrossRef" href="#example2" data-toggle="tab">Example 2</a></li>
    <li><a class="noCrossRef" href="#example3" data-toggle="tab">Example 3</a></li> -->
</ul>
  <div class="tab-content">
<div role="tabpanel" class="tab-pane active" id="example1" markdown="1">

<p style="line-height: 2; font-size: 20px">Example 1</p>
<p style="line-height: 1; font-size: 18px">Request</p>

<p>Example of a call to return the following items from a patient's structured record:</p>



<br>
<p style="line-height: 1; font-size: 18px">Request</p>

```http
GET /DocumentReference?subject=Patient/04603d77-1a4e-4d63-b246-d7504f8bd833&created=ge2019-06-24&_include=DocumentReference:author:Organization&_include=DocumentReference:author:Practitioner&_revinclude=PractitionerRole:practitioner:Practitioner
```

<p style="line-height: 1; font-size: 18px">Response payload</p>



{% include accessrecord_documents/documents_response.json %}



</div>

</div>
