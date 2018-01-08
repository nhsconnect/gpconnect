---
title: System topologies
keywords: spine, proxy, endpoint, mhs, asid
tags: [integration]
sidebar: overview_sidebar
permalink: integration_system_topologies.html
summary: "Overview of the different types of deployment topologies for GP Connect clients"
---

{% include important.html content="The topologies depicted are illustrative rather than prescriptive."%}

{% include important.html content="The Spine Security Proxy (SSP) includes a mechanism to filter out all requests between organisations that are not registered on the proxy as having a mutual data sharing agreement. Without this, all GP Connect consumers would be able to send requests to all GP connect providers. 
For the filtering solution to work, each consumer/provider organisation needs an ASID registered on the SSP."%}

## Single consumer system ##
 
![Single System](images/integration/topology1-singleSystem.png)
 
This represents (typically) a GP Practice with a single system hosted locally or a single instance hosted elsewhere. This topology has a single Common Management Agent (CMA) endpoint.
 
## Supplier data centre hosted consumer ##
 
![Datacentre System](images/integration/topology2-multiSystem.png)

This is typical of a large GP systems supplier with many practice instances hosted in a data centre, where a message handling system (MHS) endpoint is used and each instance has its own ASID.
 
## Acute trust portal using a trust integration engine (TIE) ##
 
![Acute with Portal](images/integration/topology3-acuteWithTIE.png)

This represents an acute trust acting as a GP Connect consumer via a TIE, showing the information on a clinical portal and ingested into an electronic patient record (EPR).

**Notes:**

-	the ASID is for each system which consumes data from the GP record 
-	the acute systems and non-GP Connect endpoints depicted are for illustrative purposes. An e-Referral Service (e-RS) endpoint is **not** a prerequisite for GP Connect

## Regional shared care record ##

![Shared Care Record](images/integration/topology4-hostedregionalcarerecord.png)

A regional shared care initiative hosted by one of the participating organisations might have a similar topology. This illustrates a consuming portal deployment. The hosting organisation holds the ASID for the consumer application and (subject to the usual governance controls) the data can be shared via the portal to other organisations. However, in such scenarios it is important that the originating clinician and organisation details are provided in the request so that consumer and provider audit requirements can be met. See [Cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html). 

## Spine endpoint terms ##

| MHS endpoint | An endpoint registered with Spine for use with multiple systems via an MHS. Each system has its own ASID. |
| CMA endpoint | Combined MHS and accredited system endpoint. An endpoint registered with Spine for a single system. |
| ASID | Accredited system identifier. A unique number allocated to a system on accreditation for connection to Spine. |
| MHS | Message handling server.  A middleware that handles messaging to/from Spine. |
