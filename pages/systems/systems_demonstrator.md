---
title: System demonstrator
keywords: system, demonstrator
tags: [system,demonstrator]
sidebar: overview_sidebar
permalink: system_demonstrator.html
summary: "Demonstrator implementation of the GP Connect FHIR API"
---

## Try the online demonstrator ##

> View the latest build of the [GP Connect Demonstrator](https://orange.testlab.nhs.uk/){:target="_blank"} online now!

{% include tip.html content="Data held in the GP Connect Demonstrator is reset each night to allow for easier testing. Please refer to the Demonstrator's in-built help for further details." %}

## Objective ##

Take the [Ripple](http://rippleosi.org/){:target="_blank"} open source record viewer and use it to demonstrate the GP Connect APIs to validate and accelerate delivery of the GP Connect APIs. The demonstrator acts as a mock Consuming application to show how the data made available by the APIs could be used. 

## Current status ##

We now have a functioning user interface that can drive interactions with the FHIR-based APIs to implement the following capabilities:

- Access Record HTML
- Appointment Management

## System architecture ##

![API Consumer talking to API Provider via the Spine Secure Proxy](images/systems/API Consumer talking to API Provider via the Spine Security Proxy.png)

## Source code ##

The GP Connect demonstrator is an open source software project using the [HAPI open-source FHIR library](http://hapifhir.io/){:target="_blank"}.


- Download the source code from the
[Demonstrator GitHub project repo](https://github.com/nhs-digital/gpconnect){:target="_blank"}

- The project contains step by step instructions to set up a working instance on your own machine.

## Example screens ##

![GP Connect Demonstrator Patient Summary](images/systems/GP Connect Demonstrator Patient Summary.png)
