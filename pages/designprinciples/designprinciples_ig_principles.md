---
title: Information governance principles
keywords: engage, fot, information, governance, infogov, ig
tags: [information_governance,engagement,commissioning,first_of_type]
sidebar: overview_sidebar
toc: false
permalink: designprinciples_ig_principles.html
summary: "High-level principles related to information governance (IG) of data with-in the system for FoT"
---

{% include important.html content="The principles below have been discussed and agreed in workshops with the GP Principal Providers and NHS Digital IG stakeholders.<br/><br/>
The detailed requirements supporting these will be available as part of the Provider development, Consumer development and Assurance documentation published within this specification.<br/><br/>
Review and agreement as to the IG model changes to accommodate additional capabilities and use cases is ongoing and will take into account any potential changes arising from GDPR and other strategic projects and work in this arena. The programme Privacy Impact Assessment is currently under review and will be uplifted accordingly.
" %}


## First of Type (FoT) principles ##
 
- Provider systems must be compliant with NHS Codes of Practice and Legal Obligations, and their existing NHS contractual IG requirements;  eg the foundational requirements for the GP Principal System  are covered by the GPSoC IG v 4 schedule as well as the other Common Authority  Requirements; requirements additional to these will be documented and  included in GP Connect Development, Assurance and Deployment  activities and documentation  

- The GP Connect APIs are for use in Direct Patient Care settings only

- Responsibility to ensure that Consuming End User Organisations use of the GP Connect APIs is compliant with NHS Codes of Practice & Legal Obligations in their use of healthcare records and information, resides with the Consuming End User Organisations (not NHS Digital).

- FoT Early Adopter deployments will represent organisation groupings where the necessary data sharing agreements between Data Controllers, augmented by Data Controller-Data Processor contracts, IG process and policy and fair usage notifications are already in place eg existing federation or shared record groups

- Organisational Data-Sharing validation will be implemented as part of the Spine Security Proxy (SSP) and therefore Provider GP Connect go-live must not be dependent on local organisational data-sharing configuration to support this;  local organisational data-sharing rules SHALL NOT be applied as part of GP Connect operation and SHALL NOT be changed as a result of GP Connect 

- FoT Early Adopter Consuming Organisations are  N3, IGSoC and IG Toolkit compliant, and meet national requirements for:
  - Technical (Endpoint) Security
  - User Authentication 
  - User Authorisation

- Consuming Organisations must seek explicit consent from the Patient for use of any GP Connect service; in scenarios where the patient is not present, for example a referral to an outpatient clinic where it would be reasonable to review the GP record prior to the appointment, access to the record can be made based on a Legitimate Relationship with the patient, subject to Data-Sharing agreement and absence of Provider System Patient Dissent to share indicator

- The presence of any local Patient Dissent To Share flag within a GP Practice system must be implemented when accessing the patient medical record and cannot be overridden by consent given at the point of care;  this flag does not necessarily apply for other capabilities

- Functionality to support the application of an exclusion set must be provided;  the current RCGP Sensitive Dataset for specific conditions e.g. sexual health, HIV etc. will be applied (ie excluded) for FoT, with any changes arising from national policy to be reflected

- Any data marked as private/sealed/locked/practice-designated confidential within the GP Patient record must not be shared outside the practice

- The Access Record HTML view will provide appropriate indication of withheld data 

- Audit requirements as defined in existing contractual frameworks as well as the NHS Digital Assurance Target Operating Model must be met by Provider and Consumer systems.

- Demographic Cross Checking: Consumer systems must compare the returned structured patient demographic data (supplied by the provider system as structured data) against the demographic data held in the consumer system.
If differences exist then the consumer system must show an alert/warning and provide details of which fields/values are different between the two systems.
