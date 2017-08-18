---
title: Appointments Release Notes
keywords: appointments, release notes
tags: []
sidebar: appointments_sidebar
permalink: appointments_release_notes.html
summary: "Release notes for the various versions of the Appointment Management capability."
---

- 1.0.0-rc.1
  - Updated datalibrary to be capability specific, moving it to reside under the "Development" menu within the capability. This is to allow the Profiled FHIR Resources to be referenced per capability and updated independantly. For Appointment Management we have updated specification to reference FHIR profiles stored on FHIR reference server rather than those on the old DMS capability pack.

- 1.0.0-beta.2
  - Removed practitioner participant as a mandatory element within the appointment resource (Page - Book an appointment).
  - Added location participant as a mandatory element within the appointment resource (Page - Book an appointment).
  
- 1.0.0-beta.1
  - Initial release of the Appointment Management capability pack on Github in early August 2016.
  
- 1.0.0-alpha.1
  - Initial release for feedback/comments as part of the late May 2016 release.
  