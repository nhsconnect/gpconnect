---
title: Technical Conformance
keywords: acc
tags: [testing,integration,technical conformance]
sidebar: overview_sidebar
permalink: testing_conformance.html
summary: "Details of what activities need to be completed to achieve Technical Conformance"
---

#Technical Conformance

Technical Conformance refers to the technical testing of a consumer end product. NHS Digital will review evidence from the Consumer Test Pack to ensure the technical integration meets requirements for the Spine Security Proxy (SSP) and the API itself.  





##Technical Conformance Pre-Requisites

Prior to beginning formal (NHS Digital) assurance, to achieve Technical Conformance, it is anticipated that a Consumer System Supplier will explore, develop and system test (self-test) the consumer API using the guidance and resources available publically on the developer Ecosystem portal (GitHub). The NHS Digital Solution Assurance team will create a self-testing criteria set (likely to be in the format of a checklist) which will assist Consumer System Supplier’s to determine the level of self-testing required prior to applying to start formal consumer assurance activities. 

Once a Consumer System Supplier believes they have completed their self-testing in line with the self-testing criteria set, they are required to submit the outputs to the NHS Digital Solution Assurance team for review. If the NHS Digital Solution Assurance team deem the level of consumer supplier self-testing is sufficient, formal assurance activities will commence to allow the consumer supplier to achieve Technical Conformance. 





##Technical Conformance User Scenario: _Consumer System Supplier with no Customer_
A Consumer System Supplier has aspirations to develop a product to which interacts with the GP Connect API however, they have not identified who their Commissioning Authority will be or confirmed where the end product will be used. Users in this scenario can only complete deliverables associated with Technical Conformance. 




###How is the User Scenario played out?

The Consumer System Supplier will develop and test their product independently, using the resources available on GitHub. Once a Consumer System Supplier can demonstrate they have completed sufficient independent testing they will apply to NHS Digital to begin formal Assurance.

Consumer Suppliers will firstly be granted access to the Stubbed Provider Test Instance to run test scenarios from the Consumer Test Pack, upon validating that these tests have been executed satisfactorily, approval to proceed to testing within the Actual Provider Test Instance will be granted.

*Please note, for those candidates identified as First of Type (FoT) for the HTML API, it is expected that they can proceed straight to testing against an Actual Provider Test Instance due to the Stubbed Provider Test Instance not being available for the FoT timeframe.* 

Whilst completing testing within the Stubbed and Actual Provider Test Instances, Consumer System Suppliers will also be required to complete the Technical Conformance sections within the Target Operating Model (TOM). The Technical Conformance sections ensure the Consumer System Supplier provides evidence against Architecture, IG, Clinical Safety, Spine and HTML Requirements. The TOM is also a place to evidence the execution of the tests within the Consumer Test Pack.

Following completion of all tests within the Consumer Test Pack and the relevant sections of the TOM, the Consumer System Supplier will submit the TOM to NHS Digital for review. Where acceptance of the Technical Conformance content is granted, a “technical pass” will be awarded by NHS Digital to the Consumer System Supplier and their product be listed in a GP Connect Conformance catalogue. 

The Consumer System Supplier will not be permitted to deploy their product in to the live environment until they have identified who their Commissioning Authority will be and have completed all activities associated with End Product Assurance. 

