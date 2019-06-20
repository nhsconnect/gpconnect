---
title: Service discovery
keywords: appointments design
tags: [design,appointments]
sidebar: appointments_sidebar
permalink: appointments_service_discovery.html
summary: "Determining which GP practices to book into"
---

## Determining which GP practice to book into ##

### Patient's registered practice ###

The "default" GP connect flow (as used in other capabilities) is shown in the diagram below, and includes the retrieval of the **ODS organisation code of the patient's registered practice** from PDS in step 1 (<span style="color: yellow; background-color: silver;">in yellow</span>).  For more details on this flow please [Spine integration illustrated](integration_overview.html).

<img src="images/integration/gpconnect-appts-flow.png" alt="Diagram showing the high level three step flow for making GP Connect calls" style="width: 60%;">

This flow is suitable for Appointment Management consumers that wish to book into the patient's registered practice, but where an appointment is required at a different practice, an alternate mechanism for determining the practice and their ODS organisation code is needed.

{% include important.html content="For a GP practice with multiple surgeries (locations), the ODS organisation code returned from PDS represents the GP practice organisation as a whole.  In order to determine the patient's preferred branch surgery please see [Branch surgeries](development_branch_surgeries.html) for more information." %}

### Booking into other practices ###

Where a GP Connect Appointment Management consumer wishes to book into GP practices that are not the patient's registered practice, a different mechanism to discover the practice and their ODS organisation is required.

#### Local system configuration ####



#### Directory of Services (DOS) - for UEC consumers only ####

