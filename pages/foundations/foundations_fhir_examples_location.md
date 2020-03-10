---
title: FHIR&reg; examples
keywords: foundations examples
tags: [design,foundations, location]
sidebar: foundations_sidebar
permalink: foundations_fhir_examples_location.html
summary: "Foundations - Location FHIR example"
---


The following is a set of request/response examples for the Location profile in the Foundations Capability

<p style="line-height: 2; font-size: 20px">Read a Location</p>

<p>Example of a search for a location by logical identifier</p>

<br/>

<p style="line-height: 1; font-size: 18px">Request</p>

```http
GET http://exampleGPSystem.co.uk/GP0001/STU3/1/gpconnect/Location/17
```

<p style="line-height: 1; font-size: 18px">Response payload</p>

{% include foundations/read_location_response.json %}


