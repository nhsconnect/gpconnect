---
title: Information governance
keywords: foundations ig
tags: [ig,foundations]
sidebar: foundations_sidebar
permalink: foundations_ig.html
summary: "Information Governance controls applicable to the Foundations capability pack"
---


## Patient dissent to share flag ##

When Foundations APIs are used to support the Appointment Management capability, the above flag SHALL NOT be applied by provider systems.

## PDS sensitive patients ##

Consumer systems SHALL NOT send GP Connect requests for PDS sensitive (S-flagged) patients.

Provider systems SHALL NOT return patient information in cases where a request for a PDS sensitive patient is sent to the Foundations API endpoint.  For specific handling for each Foundation API endpoint, please follow the links below:

- [Find a patient](foundations_use_case_find_a_patient.html#error-handling)
- [Read a patient](foundations_use_case_read_a_patient.html#error-handling) 
- [Register a patient](foundations_use_case_register_a_patient.html#error-handling)
