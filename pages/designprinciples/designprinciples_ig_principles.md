---
title: Information Governance Principles
keywords: engage, fot, information, governance, infogov, ig
tags: [information_governance,engagement,commissioning,first_of_type]
sidebar: designprinciples_sidebar
permalink: designprinciples_ig_principles.html
summary: "High-level principles related to information governance (IG) of data with-in the system for FoT."
---

## First of Type (FoT) Principles ##

{% include important.html content="The principles below have been discussed in workshops with the GP Principal Providers, and with their underpinning detailed requirements, are currently undergoing review to obtain the  necessary stakeholder agreement.<br/><br/>
The detailed requirements supporting these will be available as part of the Provider, Consumer Development and Assurance documentation to be published during August/September 2016.<br/><br/>
Review and agreement as to the IG model for additional and beyond FoT clinical settings is underway and taking into account other strategic projects and work in this arena.  Changes may arise to these principles and detailed supporting requirements as a result." %}

 
- Provider systems must be compliant with NHS Codes of Practice and Legal Obligations, and their existing NHS contractual IG requirements;  eg the foundational requirements for the GP Principal System  are covered by the GPSoC IG v 4 schedule as well as the other Common Authority  Requirements; requirements additional to these will be documented and  included in GP Connect Development, Assurance and Deployment  activities and documentation  

- The GP Connect APIs are for use in Direct Care settings only, where Direct Care is defined as 
clinical activity concerned with the prevention, diagnosis or treatment of illness; data must not be used for any other purposes or uses;  see example use cases and user stories on the GP Connect portals.

- Responsibility to ensure that Consuming organisation use of the GP Connect APIs is compliant with NHS Codes of Practice & Legal Obligations in their use of healthcare records and information, resides with the Commissioning Organisation (not NHS Digital).

- FoT Early Adopter deployments will represent organisation groupings where the necessary data sharing agreements between data controllers, augmented by Data Controller-Data Processor contracts, IG process and policy and fair usage notifications are already in place eg existing federation or shared record groups.
 
- FoT Early Adopter Consuming Organisations are  N3, IGSoC and IG Toolkit compliant, and meet national requirements for:
  - Technical (Endpoint) Security
  - User Authentication 
  - User Authorisation

- Consuming Organisations must deploy Permission to View processes based on the Summary Care Record (SCR) guidelines and these must be implemented and audited by the consuming system as per the detailed GP Connect Consumer IG requirements; in scenarios where the patient is not present, for example a referral to an outpatient clinic where it would be reasonable to review the GP record prior to the appoint, access to the record can be made based on a Legitimate Relationship with the patient, subject to Data-Sharing agreement and Provider System Patient Consent.

- Any data marked as private/sealed/locked within the GP Patient record must not be shared outside the practice;  override/break seal capabilities will not be developed within the APIs for FoT.

- Exclusion sets such as SCR and others for specific conditions e.g. sexual health, HIV etc. are not expected to be applied by the principal systems for FoT; to mitigate this, organisations involved in sharing must have established the relevant controls such as data sharing agreements & fair use notices explicitly covering this;  work is ongoing to obtain more detailed understanding of currently defined exclusion sets and how these are applied within SCR and other systems to determine the agreed model for GP Connect.

- Audit requirements as defined in existing contractual frameworks as well as the NHS Digital Assurance Target Operating Model must be met by Provider and Consumer systems.