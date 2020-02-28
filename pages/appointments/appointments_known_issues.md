---
title: Known issues
keywords: appointments, design, known issues, bugs
tags: [appointments,design]
sidebar: appointments_sidebar
permalink: appointments_known_issues.html
summary: "Known issues related to the Appointment Management capability"
---

### Organization resource in Search for free slots returned Bundle

A business requirement to include `Organization` was listed in a previous version of [Search for free slots](appointments_use_case_search_for_free_slots.html), without the corresponding FHIR request parameter to allow the resource to be returned in the `Bundle` (according to the FHIR rules for inclusion).

At the current time consumer applications are using this `Organization` resource in their appointment booking products and so this resource cannot immediately be removed from the Bundle.

In order to ensure the known issue does not cause problems for providers or consumers, and to support a transition to fixing the issue, the following requirements apply for the current time:

- Provider systems **SHALL** continue to return the `Organization` resource in the Search for free slots `Bundle`, except where no matching `Slot` resources were found.

- Provider systems **SHALL** accept the `_include:recurse=Location:managingOrganization` parameter in the [Search for free slots](appointments_use_case_search_for_free_slots.html) request without returning an error, however **SHALL** continue to return the `Organization` resource regardless of whether this parameter is present.

- Consumer applications **SHALL** send the `_include:recurse=Location:managingOrganization` parameter, **IF** they require corresponding `Organization` resources to be returned in the `Bundle`.

{% include important.html content="In a future version of GP Connect API, `Organization` resources will only be returned where the `_include:recurse=Location:managingOrganization` parameter is passed by consumers, therefore consumers shall pass this parameter if they require the `Organization` resource to continue to be returned as part of their Search for free slots response." %}

### Consumer sent patient temporary contact details when booking an appointment

It is recognised that a consumer organisation end user may wish to send temporary contact details for a patient at the point an appointment is booked.

At the present time, temporary contact details can only be sent by the consumer application in the [Register patient](foundations_use_case_register_a_patient.html) message which is used to create a patient record at the provider organisation where a record for the patient doesn't already exist.  Furthermore there is no corresponding "update patient demographics" message to subsequently add temporary contact details.

Therefore there is a known discrepancy in when a consumer may send temporary contact details for a patient - when a patient record is created on the provider system, but not when one already exists.

A solution to this is being considered, however as a temporary workaround, consumer organisations MAY send temporary contact details in the text `description` field of the `Appointment` resource in [Book appointment](appointments_use_case_book_an_appointment.html) or [Amend appointment](appointments_use_case_amend_an_appointment.html). However if doing so consumers must be aware this field is written to a text field stored against the booked appointment in the provider systems appointment book, and will not be saved in the usual place in the demographic record that contact details are normally stored.
