---
title: Glossary
keywords: abbreviations, definitions, glossaries, terms
tags: [getting_started]
sidebar: overview_sidebar
permalink: overview_glossary.html
summary: "Glossary of terms used by GP Connect"
toc: false
---

Glossary of common terms and abbreviations used though-out the GP Connect documentation.

#### Direct Patient Care ####
: {{site.data.glossary.direct_patient_care}}

#### First of Type ####
: {{site.data.glossary.first_of_type}}

#### Consumer ####
: {{site.data.glossary.consumer}}

#### Provider ####
: {{site.data.glossary.provider}}

#### Principal Supplier ####
: {{site.data.glossary.principal_supplier}}

#### Accreditation ####
: {{site.data.glossary.accreditation}}

#### Assurance ####
: {{site.data.glossary.assurance}}

#### GPSoC Contract ####
: {{site.data.glossary.gpsoc_contract}}

#### GP Connect Licence ####
: {{site.data.glossary.gpconnect_licence}}

#### Proxy Server ####
: {{site.data.glossary.proxy_server}}

#### Spine ####
: {{site.data.glossary.spine}}

#### PDS ####
: {{site.data.glossary.pds}}

#### SDS ####
: {{site.data.glossary.sds}}

#### ODS ####
: {{site.data.glossary.ods}}

#### Federation ####
: {{site.data.glossary.federation}}

#### Active Patient ####

An `Active` patient as defined by GP Connect is any patient on a providers system that has `Not Left` and is `Not Deceased`. The patient SHALL have also been traced and verified using [PDS](integration_personal_demographic_service.html) before their details are shared through the GP Connect API.

The concept of "Active" is related to the patient's registration ***status*** rather than to the patients registration ***type***. A providers system may have a number of different statuses which should be considered "Active", many of those statuses may apply to a number of different registration type.

***Example:***

Below is a basic ***example*** of a possible GP Practice representation of patient registration type and registration status, to help explain the concept of "Active" patient within GP Connect.

| Patient Registration Status | GP Connect Considered Active |
| --- | --- |
| Registration Pending | <span style="color:green">Yes</span> |
| Fully registered | <span style="color:green">Yes</span> |
| Deduction Pending | <span style="color:green">Yes</span> |
| Deceased | <span style="color:red">No (Inactive)</span> |
| Left/Deducted | <span style="color:red">No (Inactive)</span> |

| Patient Registration Type | Associated Registration Status |
| --- | --- |
| Regular / GMS | "Registration Pending", "Fully registered", "Deduction Pending",<br/> "Deceased", "Left/Deducted" |
| Temporary - Long Stay | "Fully registered", "Deceased", "Left/Deducted" |
| Temporary - Short Stay | "Fully registered", "Deceased", "Left/Deducted" |
| Emergency | "Fully registered", "Deceased", "Left/Deducted" |
