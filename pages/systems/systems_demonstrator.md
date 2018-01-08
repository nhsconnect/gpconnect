---
title: System demonstrator
keywords: system, demonstrator
tags: [system,demonstrator]
sidebar: overview_sidebar
permalink: system_demonstrator.html
summary: "Demonstrator implementation of the GP Connect FHIR&reg; APIs"
---

## Objective ##

Take the [Ripple](http://rippleosi.org/){:target="_blank"} open source record viewer and use it to demonstrate the GP Connect APIs' ability to validate and accelerate the delivery of data. The demonstrator would act as a mock consuming application to show how the data made available by the APIs could be used. 

## Methodology ##

- iterative and rapid design in collaboration with [NHS Digital](http://digital.nhs.uk/){:target="_blank"} 
- requirements driven by supplier workshops and FHIR&reg; standard releases
- [open source artefacts on GitHub](https://github.com/nhs-digital/gpconnect){:target="_blank"} for later re-use
- can be extended into more focussed use cases in the future (for example, testing, assurance tooling, developer tools)
- using the [HAPI open-source FHIR library](http://hapifhir.io/){:target="_blank"} to bootstrap FHIR compliance

## System architecture ##

![API consumer talking to API provider via the Spine Security Proxy](images/systems/API Consumer talking to API Provider via the Spine Security Proxy.png)

## Source code ##
The GP Connect demonstrator is a free open source software (FOSS) project.

- download the source code from the
[Demonstrator GitHub project repo](https://github.com/nhs-digital/gpconnect){:target="_blank"}

- the project contains step by step instructions to set up a working instance on your own machine

## Current status ##

We now have a functioning user interface that can drive interactions with the FHIR-based APIs to:

- Access Record (HTML) across the 11 defined record sections (date range searching and/or paging are not currently implemented)
- Appointment Management for a patient across practice diaries
- Task Management for a patient across organisational boundaries

## Online system ##

View the latest build of the [GP Connect Demonstrator](http://ec2-54-194-109-184.eu-west-1.compute.amazonaws.com/){:target="_blank"}

{% include tip.html content="All data held in the GP Connect Demonstrator is a cleared down and reseeded each night to allow for easier testing. See the demonstrator's in-built help for further details." %}

## Community projects ##

Dave Bould has developed a Vagrant config file for building a complete GP Connect Demonstrator environment with only a few commands:

[GP Connect Vagrant](https://github.com/dbould/gpconnect-vagrant)

## Example screens ##

![GP Connect Demonstrator Patient Summary](images/systems/GP Connect Demonstrator Patient Summary.png)
