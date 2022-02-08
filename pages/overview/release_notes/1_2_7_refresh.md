---
title: GP Connect API 1.2.7-refresh release notes
keywords: GP Connect, release notes
tags: [release]
sidebar: overview_sidebar
permalink: overview_release_notes_1_2_7_refresh.html
summary: "GP Connect API 1.2.7-refresh released on Mar 2022"
toc: true
---

## Introduction ##

The GP Connect API 1.2.7-refresh is a refresh of the 1.2.7 specification to improve the readability and clarity of content.  It **does not** contain changes for suppliers to implement.

## 1.2.7-refresh changes ##

## Appointments ##

### Improve appointments FHIR resources page ###

**Tickets:**&nbsp; [#1148](https://github.com/nhsconnect/gpconnect/issues/1148)

**Affects:**&nbsp; Appointments

**Impacts:** *(none)*

**Description:**

- Split the resource relationships diagram into two
- Improve layout of the API interactions listing

**Pages changed:**

- [FHIR&reg; resources](datalibraryappointment.html)

---

### Remove superseded pages from the business requirements spreadsheet ###

**Tickets:**&nbsp; [#1113](https://github.com/nhsconnect/gpconnect/issues/1113)

**Affects:**&nbsp; Appointments

**Impacts:** *(none)*

**Description:**

- Remove superseded and superfluous pages from the business requirements spreadsheet

**Pages changed:**

- [Business requirements](appointments_requirements.html)

---

### Improve layout of Appointments API definition pages ###

**Tickets:**&nbsp; [#1149](https://github.com/nhsconnect/gpconnect/issues/1149)

**Affects:**&nbsp; Appointments

**Impacts:** *(none)*

**Description:**

- Co-locate request and response examples at the end of page
- Create additional examples
- Move error handling from request operation section to request response section
- Add free slot resource relationship diagram to search for free slots page

**Pages changed:**

- [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html)
- [Search for free slots](appointments_use_case_search_for_free_slots.html)
- [Read an appointment](appointments_use_case_read_an_appointment.html)
- [Book an appointment](appointments_use_case_book_an_appointment.html)
- [Amend an appointment](appointments_use_case_amend_an_appointment.html)
- [Cancel an appointment](appointments_use_case_cancel_an_appointment.html)

---

## Foundations ##

### Improve layout of Foundations API definition pages ###

**Tickets:**&nbsp; [#1150](https://github.com/nhsconnect/gpconnect/issues/1150)

**Affects:**&nbsp; Foundations

**Impacts:** *(none)*

**Description:**

- Co-locate request and response examples at the end of page
- Create additional examples
- Move error handling from request operation section to request response section

**Pages changed:**

- [Get the FHIR&reg; capability statement](foundations_use_case_get_the_fhir_capability_statement.html)
- [Find a patient](foundations_use_case_find_a_patient.html)
- [Read a patient](foundations_use_case_read_a_patient.html)
- [Find a practitioner](foundations_use_case_find_a_practitioner.html)
- [Read a practitioner](foundations_use_case_read_a_practitioner.html)
- [Find an organisation](foundations_use_case_find_an_organisation.html)
- [Read an organisation](foundations_use_case_read_an_organisation.html)
- [Read a location](foundations_use_case_read_a_location.html)
- [Register a patient](foundations_use_case_register_a_patient.html)

