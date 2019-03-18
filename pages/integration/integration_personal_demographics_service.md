---
title: Personal Demographic Service
keywords: spine, pds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_personal_demographic_service.html
summary: "Overview of the role of the Personal Demographic Service within GP Connect."
---

## PDS tracing ##

GP Connect systems **SHALL** be capable of performing [Personal Demographic Service](https://digital.nhs.uk/Demographics) (PDS) tracing of patients to obtain their NHS number, date of birth and current registered GP organisation.

[Spine Core FHIR API Framework - Personal Demographics Service](https://developer.nhs.uk/apis/spine-core-1-0/pds_overview.html) provides a summary of the role of PDS in the NHS Spine architecture, and describes three options for accessing it. Systems **SHALL** perform this tracing using one of the three options.

{% include important.html content="The term “consuming system” on the PDS page of the Spine Core FHIR API Framework site applies in the GP Connect context to both consumer and provider systems. " %}
