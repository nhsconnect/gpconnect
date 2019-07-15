---
title: ReferralRequest
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_referralrequest.html
summary: "FHIR resource for population guidance for ReferralRequest"
div: resource-page
---
## Introduction

The headings below list the elements of the ReferralRequest resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_immunization.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [ReferralRequest profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1)." %}

## ReferralRequest elements

### id

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the ReferralRequest resource.

### meta.profile

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The Immunization profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1)



## Elements **not in use**

The following elements **MUST NOT** be populated:
