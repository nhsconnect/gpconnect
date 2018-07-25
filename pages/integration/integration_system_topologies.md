---
title: System topologies
keywords: spine, proxy, endpoint, mhs, asid
tags: [integration]
sidebar: overview_sidebar
permalink: integration_system_topologies.html
summary: "Overview of the different types of deployment topologies for GP Connect clients"
---

{% include important.html content="The topologies depicted are illustrative rather than prescriptive, and a real-world implementation may have a mix of styles."%}

{% include important.html content="The Spine Secure Proxy (SSP) includes a mechanism to filter out all requests between organisations that are not registered on the proxy as having a mutual data sharing agreement. Without this, all GP Connect consumers would be able to send requests to all GP Connect providers. For the filtering solution to work, each consumer/provider organisation needs an ASID registered on the SSP."%}

# Consumer topologies #

## Simple model ##
![Simple topology](images/integration/consumer-topology1-simple.png)<br>

A grouping of different GP Connect consumer systems, all connecting directly to GP Connect via the SSP.  Each consumer in this example is registered as a CMA endpoint. The key point is that each consumer system has its own ASID.

## Aggregator model ##

![Simple model](images/integration/consumer-topology2-aggregator.png)

Several different consumer systems connecting to GP Connect via middleware (Message Handling Server/MHS).

# Provider topologies #

## Single practice system ##

![Single practice system](images/integration/provider-topology1-single.png) 

A discrete instance of a primary care system serving a single GP practice.

## Data centre hosted practice system ##

![Hosted practice system](images/integration/provider-topology2-datacentre.png) 

A GP practice system instance hosted in a primary care system (PCS) supplier's data centre. Note each individual practice has a logical CMA endpoint with its own ASID but sharing the party key.

![Legend](images/integration/topologies-legend.png)

## Spine endpoint terms ##

The [NHS Spine FHIR API Framework](https://developer.nhs.uk/apis/spine-core-1-0/build_endpoints.html#spine-accredited-systems-and-endpoints) presents an introduction to Spine endpoints, and provides definitions of terms used above.




