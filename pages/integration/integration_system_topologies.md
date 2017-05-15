---
title: System Topologies
keywords: spine, proxy, endpoint, mhs, asid
tags: [integration]
sidebar: overview_sidebar
permalink: integration_system_topologies.html
summary: "Overview of the different types of deployment topologies for GP Connect clients"
---

{% include important.html content="The topologies depicted are illustrative rather than prescriptive."%}

{% include important.html content="The Spine Security Proxy includes a mechanism to filter out all requests between organisations that are not registered on the proxy as having a mutual Data Sharing Agreement. Without this then all GP Connect consumers would be able to send request to all GP connect Providers. 
In order for the filtering solution to work each consumer/provider organisation needs an ASID registered on the SSP."%}

## Single Consumer System ##
 
![Single System](images/integration/topology1-singleSystem.png)
 
This represents typically a GP Practice with a single system hosted locally or a single instance hosted elsewhere.  This topology has a single "CMA Endpoint".
 
## Supplier Datacentre Hosted Consumer ##
 
![Datacentre System](images/integration/topology2-multiSystem.png)

This is typical of a large GP Systems supplier with many Practice instances hosted in a datacentre, where a "MHS Endpoint" is used and each instance has its own ASID.
 
## Acute Trust Portal using TIE ##
 
![Acute with Portal](images/integration/topology3-acuteWithTIE.png)

This represents an acute trust acting as a GP Connect consumer via a Trust Integration Engine, showing the information on a clinical portal and also ingested into an EPR.
Note the ASID for each system which consumes data from the GP record.  Also please note the acute systems and non GP Connect endpoints depicted are for illustrative purposes.  An e-RS endpoint is **not** a pre-requisite for GP Connect.

## Regional Shared Care Record ##

![Shared Care Record](images/integration/topology4-hostedregionalcarerecord.png)

A regional shared care initiative hosted by one of the participating organisations might have a topology similar to this.  This  illustrates a consuming portal deployment. The hosting organisation holds the ASID for the consumer application and (subject to the usual governance controls) the data can be shared via the portal to other organisations.  However in such scenarios it is important that the originating clinician and organisation details are provided in the request so that consumer and provider audit requirements can be met. See [Cross Organisation Audit and Provenance](integration_cross_organisation_audit_and_provenance.html) 

## Spine Endpoint Terms ##

| MHS Endpoint | An endpoint registered with Spine for use with multiple systems via a MHS.  Each system has its own ASID. |
| CMA Endpoint | Combined MHS and Accredited System Endpoint. An endpoint registered with Spine for a single system. |
| ASID | Accredited System Identifer. A unique number allocated to a system on accreditation for connection to Spine. |
| MHS | Message Handling Server.  A middleware that handles messaging to/from Spine. |
