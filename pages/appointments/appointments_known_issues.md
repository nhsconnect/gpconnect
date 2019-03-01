---
title: Appointment Management known issues
keywords: appointments, design, known issues, bugs
tags: [appointments,design]
sidebar: appointments_sidebar
permalink: appointments_known_issues.html
summary: "Known issues related to the Appointment Management capability"
---

### Organization resource in Search for free slots returned Bundle

A business requirement to include `Organization` was listed in a previous version of [Search for free slots](appointments_use_case_search_for_free_slots.html), without the corresponding FHIR request parameter to allow the resource to be returned in the `Bundle` (according to the FHIR rules for inclusion).

At the current time consumer systems are using this `Organization` resource in their appointment booking products and so this resource cannot immediately be removed from the Bundle.

In order to ensure the known issue does not cause problems for providers or consumers, and to support a transition to fixing the issue, the following requirements apply for the current time:

- Provider systems **SHALL** continue to return the `Organization` resource in the Search for free slots `Bundle`, except where no matching `Slot` resources were found.

- Provider systems **SHALL** accept the `_include:recurse=Location:managingOrganization` parameter in the [Search for free slots](appointments_use_case_search_for_free_slots.html) request without returning an error, however **SHALL** continue to return the `Organization` resource regardless of whether this parameter is present.

- Consumer systems **SHALL** send the `_include:recurse=Location:managingOrganization` parameter, **IF** they require corresponding `Organization` resources to be returned in the `Bundle`.

{% include important.html content="In a future version of GP Connect API, `Organization` resources will only be returned where the `_include:recurse=Location:managingOrganization` parameter is passed by consumers, therefore consumers should pass this parameter if they require the `Organisation` resource as part of their Search for free slots response." %}
