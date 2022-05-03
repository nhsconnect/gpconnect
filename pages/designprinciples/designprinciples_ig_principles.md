---
title: Information governance principles
keywords: engage, fot, information, governance, infogov, ig
tags: [information_governance,engagement,commissioning]
sidebar: overview_sidebar
toc: false
permalink: designprinciples_ig_principles.html
summary: "High-level principles related to information governance (IG) of data within the system"
---

{% include important.html content="The principles below have been discussed and agreed in workshops with the GP principal providers and NHS Digital IG stakeholders.<br/><br/>
The detailed requirements supporting these will be available as part of the provider development, consumer development and assurance documentation published within this specification.<br/><br/>
Review and agreement as to IG model changes (to accommodate additional capabilities and use cases) is ongoing and will take into account any potential changes arising from the General Data Protection Regulation (GDPR) and other strategic projects in this arena. The programme privacy impact assessment is currently under review and will be updated accordingly.  Specifications may evolve to meet changing health and care standards, legal frameworks and patient reasonable and informed expectation.
" %}


- provider systems **MUST** be compliant with NHS codes of practice and legal obligations, and their existing NHS contractual IG requirements - for example, the foundational requirements for the GP principal systems are covered by the GP Systems of Choice (GPSoC) IG v4 schedule as well as the other common authority requirements
  - requirements additional to these will be documented and included in GP Connect development, assurance and deployment activities and documentation  

- the GP Connect APIs are for use in direct patient care settings only

- the responsibility of ensuring that consuming suppliers' use of the GP Connect APIs is compliant with NHS codes of practice and legal obligations resides with the consuming supplier (not NHS Digital)

- consuming organisations are responsible for data sharing agreements with data controllers, augmented by data controller-data processor contracts, IG process and policy and fair usage notifications if national agreements are not in place

- organisational data-sharing validation will be implemented as part of the Spine Secure Proxy (SSP) and therefore provider GP Connect go-live must not be dependent on local organisational data-sharing configuration to support this;  local organisational data-sharing rules **MUST NOT** be applied as part of GP Connect operation and **MUST NOT** be changed as a result of GP Connect

- consuming organisations **MUST** be N3, IGSoC and IG Toolkit compliant, and meet national requirements for:
  - technical (endpoint) security
  - user authentication
  - user authorisation

- consuming organisations **MUST** seek permission to view from the Patient for any information supplied via a GP Connect service; in scenarios where the patient is not present, for example a referral to an outpatient clinic where it would be reasonable to review the GP record prior to the appointment, access to the record can be made based on a Legitimate Relationship with the patient, subject to Data-Sharing agreement and absence of Provider System Patient Dissent to share indicator

- consuming organisations **MUST**
  - ensure the service is only accessed for the sole purpose of supporting direct patient care, and
  - ensure appropriate role-based access controls are applied such that only appropriate users are able to access the service, subject to the extent to which it can be limited for each capability, and
  - be aware of any limitations set as to the extent of access allowed for a healthcare setting and / or user role, and ensure such limitations are robustly applied

- the presence of any local patient dissent to share flag within a GP Practice system **MUST** be implemented when accessing the patient medical record and cannot be overridden by consent given at the point of care

- functionality to support the application of an exclusion set **MUST** be provided;  the current Royal College of General Practitioners (RCGP) sensitive dataset for specific conditions (for example, sexual health, HIV and so on) will be applied (excluded) with any changes arising from national policy to be reflected

- any data marked as private/sealed/locked/practice-designated confidential within the GP Patient record **MUST NOT** be shared outside the practice

- the Access Record HTML view will provide appropriate indication of withheld data

- audit requirements as defined in existing contractual frameworks as well as the NHS Digital assurance process **MUST** be met by provider and consumer systems

- consumer systems **MUST** compare the returned structured patient demographic data (supplied by the provider system as structured data) against the demographic data held in the consumer system
  - if differences exist then the consumer system **MUST** show an alert/warning and provide details of which fields/values are different between the two systems
