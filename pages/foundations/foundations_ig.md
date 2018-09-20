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

## PDS S-flagged patients ##

Consumer systems SHALL NOT send GP Connect requests for S-flagged patients.

In cases where a request for an S-flagged patient is sent, provider systems SHALL return a 'Patient Not Found' error.
