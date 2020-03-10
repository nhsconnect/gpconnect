---
title: FHIR&reg; examples
keywords: foundations examples
tags: [design,foundations, capabilty statement]
sidebar: foundations_sidebar
permalink: foundations_fhir_examples_capability.html
summary: "Foundations - Capability Statement FHIR example"
---


The following is a request/response example to retrieve the Capability Statement profile in the Foundations Capability

<p style="line-height: 2; font-size: 20px">Retrieve the Capability Statement</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

```http
GET http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/metadata
```

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include foundations/read_capability_response.json %}
