---
title: System topologies
keywords: spine, proxy, endpoint, mhs, asid
tags: [integration]
sidebar: overview_sidebar
permalink: integration_system_topologies.html
summary: "Overview of the different types of deployment topologies for GP Connect providers and consumers"
---

{% include important.html content="The Spine Secure Proxy (SSP) includes a mechanism to filter out all requests between organisations that are not registered on the proxy as having a mutual Data Sharing Agreement. Without this then all GP Connect consumers would be able to send requests to all GP Connect providers. 
In order for the filtering solution to work each consumer/provider organisation MUST have their own unique [Spine ASID](#spinesds-terminology) configured on the SSP."%}

# Consumer topologies #

## Consumer system - shared MHS ##

![Consumer topology 2](images/integration/consumer-topology-2.png)<br>

Several consumer systems connecting to GP Connect via a shared message handling server.

This is a typical deployment for an area based or regional portal, where a central system/TIE (Trust Integration Engine) acting as the message handling server connects to Spine for multiple organisations.

Please note:
- each consumer system using GP Connect **MUST** have a unique [ASID](#spine-endpoint-terms) for each organisation that is using it, in order that messages flowing through Spine can be correctly identified back to the originating organisation
- consumer systems in the shared MHS topology have one [Party Key](#spine-endpoint-terms) shared amongst connecting organisations

{% include important.html content="In consumer system topologies where GP Connect consumer applications are provisioned via a portal or middleware hosted by another organisation, it is vital that the ASID sent in the `Ssp-From` header reflects the organisation from where the request originates, rather than the hosting organisation." %}

## Consumer system - separate MHS ##

![Consumer topology 1](images/integration/consumer-topology-1.png)<br>

Several consumer systems connecting to GP Connect via their own message handling servers.

This could be different types of consumer systems, or the same type of consumer system deployed as separate instances.

Please note:
- each consumer system using GP Connect **MUST** have a unique [ASID](#spine-endpoint-terms) for each organisation that is using it, in order that messages flowing through Spine can be correctly identified back to the originating organisation
- consumer systems using the separate MHS topology each have their own [Party Key](#spine-endpoint-terms)

# Provider topologies #

## Provider system - shared MHS ##

![Provider topology 2](images/integration/provider-topology-2.png) 

{% include important.html content="Please note in the diagram above, the shared message handling server holds three party keys, one associated with each practice. Party Key 1 is for the practice with ASID 1, Party Key 2 is for the practice with ASID 2, and so on."%}

Multiple GP practice systems using a shared message handling server.

This is a typical deployment for a multi-tenanted data centre hosted GP system serving multiple organisations.

Please note:

- each provider system using GP Connect **MUST** have an [ASID](#spine-endpoint-terms) **AND** [Party Key](#spine-endpoint-terms) for each organisation that is using it, in order that messages flowing through Spine can be routed to the correct destination organisation
- each Party Key/ASID combination **MUST** be registered in SDS as a [CMA endpoint](#spine-endpoint-terms)

## Provider system - separate MHS ##

![Provider topology 1](images/integration/provider-topology-1.png) 

Discrete instances of GP practice systems each serving a single GP practice, and each with their own message handling server.

Please note:

- each provider system using GP Connect **MUST** have an [ASID](#spine-endpoint-terms) **AND** [Party Key](#spine-endpoint-terms) for each organisation that is using it, in order that messages flowing through Spine can be routed to the correct destination organisation
- each party key/ASID combination **MUST** be registered in SDS as a [CMA endpoint](#spine-endpoint-terms)

## Spine/SDS terminology ##

{% include sds_terminology.html %}
