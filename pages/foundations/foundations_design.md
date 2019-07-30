---
title: Foundations design
keywords: foundations design
tags: [design,foundations]
sidebar: foundations_sidebar
permalink: foundations_design.html
summary: "Overview of the design decisions made in relation to the Foundations capability"
---

## Business identifiers ##

The following business identifier types are to be supported by GP Connect systems:

| Identifier | Resource | System |
| ---------- | -------- | ------ |
| NHS Number | Patient | `https://fhir.nhs.uk/Id/nhs-number` |
| Local Identifier | Resource | `http://fhir.nhs.net/Id/local-identifier` |
| ODS Code | Organisation | `https://fhir.nhs.uk/Id/ods-organization-code` |
| ODS Site Code | Location | `https://fhir.nhs.uk/Id/ods-site-code` |
| SDS User ID | Practitioner | `https://fhir.nhs.uk/Id/sds-user-id` |

{% include important.html content="Support for additional identifier types in line with the existing GPSoC requirements is also under consideration." %}

## Definition of organisation and location entities

The GP practice organisation is a legal entities which is represented by the FHIR&reg; `Organization` resource. This entity will have an assigned [ODS code](https://digital.nhs.uk/organisation-data-service). 

The practice organisation will have one or more operating locations (also known as sites or branches) which together perform the patient healthcare for which the organisation is legally responsible. Each operating location is represented by a FHIR `Location` resource. 

Where ODS Site codes are defined in Spine configuration, these map to GP practice operating locations, and hence to Location FHIR resources.

