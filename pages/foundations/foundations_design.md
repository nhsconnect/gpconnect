---
title: Foundations Design
keywords: foundations design
tags: [design,foundations]
sidebar: foundations_sidebar
permalink: foundations_design.html
summary: "Overview of the design decisions made in relation to the Foundations capability."
---

## Business Identifiers ##

The following business identifier types are to be supported by GP Connect systems:

| Identifier | Resource | System |
| ---------- | -------- | ------ |
| NHS Number | Patient | `http://fhir.nhs.net/Id/nhs-number` |
| Local Identifier | Resource | `http://fhir.nhs.net/Id/local-identifier` |
| ODS Code | Organisation | `http://fhir.nhs.net/Id/ods-organization-code` |
| ODS Site Code | Location | `http://fhir.nhs.net/Id/ods-site-code` |
| SDS User ID | Practitioner | `http://fhir.nhs.net/Id/sds-user-id` |

{% include important.html content="Support for additional identifier types inline with the existing GPSoC requirements is also under consideration." %}