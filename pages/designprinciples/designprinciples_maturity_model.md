---
title: Maturity Model
keywords: development, roadmap
tags: [engage,development,fhir]
sidebar: designprinciples_sidebar
permalink: designprinciples_maturity_model.html
summary: High-level maturity model for GP Connect systems.
---

[<i class="fa fa-arrow-left" aria-hidden="true"/> Back to GP Connect - Getting Started.](index.html)

{% include important.html content="All delivery dates are indicative and subject to on-going review." %}

The maturity roadmap of a compliant Principal GP system is expected to follow the following FHIR&reg; and business capability maturity stages as follows:

## Stage 1. Q3 2016 ##
- HTML Get Care Record, Appointment and Task capabilities.
 - HTML Patient Summary, Encounters, Clinical Items, Problems and Issues, Allergies and Adverse Reactions, <br/>Medications, Referrals, Observations, Immunisations & Administrative Items.
- Spine Security Proxy (SSP) integration.
- Organisational Data Sharing Agreement checking in the SSP.
- RBAC Auditing of local user roles in the JWT.
 
## Stage 2. Q4 2016 ##
- Get Care Record with bundled structured resources.
- HTML Warnings, Key Indicators, Current Recalls, Patient Details, Investigations.
- HTML View Clinical Safety, Cross-Vendor Consistency Changes, Medications Sections Review, Date-Range Review.
- CORS Support in the SSP.
- RBAC Auditing of Spine Smartcard user roles in the JWT.

## Stage 3. Q4 2016 into Q1 2017 ##
- Unbundled direct read-only access to specific resources.  

{% include important.html content="It is expected that unbundled direct read-only access to resources will be undertaken in-line with the high-level approach being pursued in other jurisdictions (i.e. Project Argonaut's and specifically the [Argonaut Implementation Guide](http://argonautwiki.hl7.org/index.php?title=Implementation_Guide))." %} 
