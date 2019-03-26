---
title: System topologies
keywords: spine, proxy, endpoint, mhs, asid
tags: [integration]
sidebar: overview_sidebar
permalink: integration_system_topologies.html
summary: "Overview of the different types of deployment topologies for GP Connect providers and consumers"
---

{% include important.html content="The Spine Secure Proxy includes a mechanism to filter out all requests between organisations that are not registered on the proxy as having a mutual Data Sharing Agreement. Without this then all GP Connect consumers would be able to send requests to all GP Connect providers. 
In order for the filtering solution to work each consumer/provider organisation MUST have their own unique [Spine ASID](#spine-endpoint-terms) configured on the SSP."%}

# Consumer Topologies #

## Consumer system - shared MHS ##

![Consumer topology 2](images/integration/consumer-topology-2.png)<br>

Several consumer systems connecting to GP Connect via a shared message handling server.

This is a typical deployment for an area based or regional Portal, where a central system/TIE (Trust integration engine) acting as the message handling server connects to Spine for multiple organisations.

Please note:
- each consumer system using GP Connect **MUST** have a unique [ASID](#spine-endpoint-terms) for each organisation that is using it, in order that messages flowing through Spine can be correctly identified back to the originating organisation
- consumer systems in the shared MHS toplogy have one [Party Key](#spine-endpoint-terms) shared amongst connecting organisations

## Consumer system - seperate MHS ##

![Consumer topology 1](images/integration/consumer-topology-1.png)<br>

Several consumer systems connecting to GP Connect via their own message handling servers.

This could be different types of consumer systems, or the same type of consumer system deployed as seperate instances.

Please note:
- each consumer system using GP Connect **MUST** have a unique [ASID](#spine-endpoint-terms) for each organisation that is using it, in order that messages flowing through Spine can be correctly identified back to the originating organisation
- consumer systems using the seperate MHS topology each have their own [Party Key](#spine-endpoint-terms)

# Provider Topologies #

## Provider system - shared MHS ##

![Provider topology 2](images/integration/provider-topology-2.png) 

Multiple GP practice systems using a shared message handling server.

This is a typical deployment for a multi tenanted data centre hosted GP system serving multiple organisations.

Please note:

- each provider system using GP Connect **MUST** have an [ASID](#spine-endpoint-terms) **AND** [Party Key](#spine-endpoint-terms) for each organisation that is using it, in order that messages flowing through Spine can be routed to the correct destination organisation
- each Party Key/ASID combination **MUST** be registered in SDS as a [CMA endpoint](#spine-endpoint-terms)

## Provider system - seperate MHS ##

![Provider topology 1](images/integration/provider-topology-1.png) 

Discrete instances of GP practice systems each serving a single GP Practice, and each with their own message handling server.

Please note:

- each provider system using GP Connect **MUST** have an [ASID](#spine-endpoint-terms) **AND** [Party Key](#spine-endpoint-terms) for each organisation that is using it, in order that messages flowing through Spine can be routed to the correct destination organisation
- each Party Key/ASID combination **MUST** be registered in SDS as a [CMA endpoint](#spine-endpoint-terms)

## Spine/SDS terminology ##

{% include sds_terminology.html %}
