---
title: Foundations Release Notes
keywords: foundations, release notes
tags: []
sidebar: foundations_sidebar
permalink: foundations_release_notes.html
summary: "Release notes for the various versions of the Foundations capability."
---

- 1.0.0-rc.1
  - Updated datalibrary to be capability specific, moving it to reside under the "Development" menu within the capability. This is to allow the Profiled FHIR Resources to be referenced per capability and updated independantly. For foundations we have updated specification to reference FHIR profiles stored on FHIR reference server rather than those on the old DMS capability pack.

- 1.0.0-beta.2
  - Updated example conformance profile to include GP Connect profile information (Page - [Get the FHIR Conformance Statement](https://nhsconnect.github.io/gpconnect/foundations_use_case_get_the_fhir_conformance_profile.html)).
  - Clarified use of [Register a patient](https://nhsconnect.github.io/gpconnect/foundations_use_case_register_a_patient.html) API is only to support local-only temporary patient registrations to support federated appointment booking
  - Added additional clarification around use of identifiers for all foundation search capabilities (Pages - Find a practitioner, Find a patient, Find an organisation, Find a location).
  - Clarity on mandatory data items for [Register a patient](https://nhsconnect.github.io/gpconnect/(foundations_use_case_register_a_patient.html#payload-request-body) API
  - Moved VRead to out of scope (Pages - [Get the FHIR Conformance Statement, Common API Guidance](https://nhsconnect.github.io/gpconnect/foundations_use_case_get_the_fhir_conformance_profile.html))
  - Added java example code to specification for Read capabilities (Pages - Read a practitioner, Read a patient, Read an organisation, Read a location).
  - Updated example code to bring in line with [FHIR Server Root URL format](https://nhsconnect.github.io/gpconnect/development_fhir_api_guidance.html#fhir-api-versioning) guidance.
  - Updates to [Register a patient](https://nhsconnect.github.io/gpconnect/foundations_use_case_register_a_patient.htm) to include latest operation definition XML, and provide clarity on profiles used on response.

- 1.0.0-beta.1
  - Initial release of the Foundations capability pack on GitHub in early August 2016.
  
- 1.0.0-alpha.1
  - Initial release for feedback/comments as part of the late May 2016 release.