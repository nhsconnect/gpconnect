---
title: Appointment Management known issues
keywords: appointments, design, known issues, bugs
tags: [appointments,design]
sidebar: appointments_sidebar
permalink: appointments_known_issues.html
summary: "Known issues related to the Appointment Management capability"
---

### Organization resource in Search for free slots returned Bundle

A business requirement to include `Organization` is listed in [Search for free slots](appointments_use_case_search_for_free_slots.html), without the corresponding FHIR request parameter to allow the resource to be returned in the `Bundle`.

At the current time consumer systems are using this `Organization` resource in their appointment booking products and so this cannot immediately be removed.

In order to ensure the known issue does not cause problems for providers or consumers, and to support a transition to fixing the issue, the following requirements apply for the current time:

- Provider systems SHALL continue to return the `Organization` resource in the Search for free slots `Bundle`, except where no matching `Slot` resources were found

- Provider systems SHALL accept the `_include:recurse=Schedule:actor:Location` parameter in the [Search for free slots](appointments_use_case_search_for_free_slots.html) request without returning an error, however SHALL continue to return the `Organization` resource regardless of whether this is present.

- Consumer systems SHALL NOT send the `_include:recurse=Schedule:actor:Location` parameter at the current time.  This cannot currently be sent due to upcoming target consumer and provider version deployments.  Consumers will be notified when this can be sent.
