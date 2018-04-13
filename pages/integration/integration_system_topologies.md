---
title: System topologies
keywords: spine, proxy, endpoint, mhs, asid
tags: [integration]
sidebar: overview_sidebar
permalink: integration_system_topologies.html
summary: "Overview of the different types of deployment topologies for GP Connect clients"
---

{% include important.html content="The topologies depicted are illustrative rather than prescriptive, and a real world implementation may have a mix of styles."%}

{% include important.html content="The Spine Security Proxy (SSP) includes a mechanism to filter out all requests between organisations that are not registered on the proxy as having a mutual data sharing agreement. Without this, all GP Connect consumers would be able to send requests to all GP Connect providers. For the filtering solution to work, each consumer/provider organisation needs an ASID registered on the SSP."%}

# Consumer Topologies #

## Simple Model ##
![Simple Topology](images/integration/consumer-topology1-simple.png)<br>

A grouping of different GP Connect consumer systems, all connecting directly to GP Connect via the SSP.  Each consumer in this example is registered as a CMA endpoint.  The key point is that each consumer system has its own ASID.

## Aggregator Model ##

![Simple Model](images/integration/consumer-topology2-aggregator.png)

Several different consumer systems connecting to GP Connect via middleware (Message Handling Server / MHS)

# Provider Topologies #

## Single Practice System ##

![Single Practice System](images/integration/provider-topology1-single.png) 

A discrete instance of a Primary Care System serving a single GP Practice.

## Data Centre Hosted Practice System ##

![Hosted Practice System](images/integration/provider-topology2-datacentre.png) 

A GP Practice system instance hosted in a Primary Care System (PCS) supplier's data centre.  Note each individual practice has a logical CMA endpoint with its own ASID but sharing the Party Key.

![Legend](images/integration/topologies-legend.png)

## Spine endpoint terms ##

| ASID | Accredited system identifier. A unique number allocated to a system on accreditation for connection to Spine. |
| CMA endpoint | Combined MHS and accredited system endpoint. An endpoint registered with Spine for a single system. |
| MHS | Message handling server.  A middleware that handles messaging to/from Spine. |
| MHS endpoint | An endpoint registered with Spine for use with multiple systems via an MHS. Each system has its own ASID. |
| Party Key | The identity of a MHS handling messages for an Accredited System |



