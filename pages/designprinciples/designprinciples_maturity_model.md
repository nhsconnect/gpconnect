---
title: Maturity Model
keywords: development, roadmap
tags: [engage,development,fhir]
sidebar: designprinciples_sidebar
permalink: designprinciples_maturity_model.html
summary: High-level maturity model for GP Connect systems.
---

{% include important.html content="All delivery dates are indicative and subject to on-going review." %}

The maturity roadmap of a compliant Principal GP system is expected to follow the following FHIR&reg; and business capability maturity stages as follows:

## Stage 1 - Current ##
- Access Record (v1.0), Appointment (v1.0) and Task (v1.0) capabilities.
 - Access Record includes: HTML Patient Summary, Encounters, Clinical Items, Problems and Issues, Allergies and Adverse Reactions, Medications, Referrals, Observations, Immunisations & Administrative Items.
- Spine Security Proxy (SSP) integration.
- Organisational Data Sharing Agreement checking in the SSP.
- RBAC Auditing of local user roles in the JWT.
 
## Stage 2 ##
- Access Record (v2.0) with bundled structured resources.
 - May include some improvements to HTML content such as:  HTML Warnings, Key Indicators, Current Recalls, Patient Details, Investigations, Medications Sections Improvements, Date-Range Improvements.
 - HTML View Clinical Safety, Cross-Vendor Consistency Changes.
 - Structured content for current Medications and Allergies (more resources to follow, see priortisation list below)
- CORS Support in the SSP.
- RBAC Auditing of Spine Smartcard user roles in the JWT.

## Stage 3 ##
- Unbundled direct read-only access to specific resources (see priortisation list below).


# Prioritised Structured Content #
This is the working list of structured resources required for Access Record v2.0 and Stage 3 RESTful access

## Priority confirmed ##

1. a) MedicationOrder 
<br/> b) MedicationStatement
2. AllergyIntolerance
3. Immunization
4. Condition

## To be confirmed ##

5. DiagnosticOrder
6. DiagnosticReport
7. Encounter
8. Flag
9. MedicationDispense
10. MedicationAdministration
11. Observation
12. Problem
13. Procedure
14. Referral
15. Patient

{% include important.html content="It is expected that unbundled direct read-only access to resources will be undertaken in-line with the high-level approach being pursued in other jurisdictions (i.e. Project Argonaut's and specifically the [Argonaut Implementation Guide](http://argonautwiki.hl7.org/index.php?title=Implementation_Guide))." %} 
