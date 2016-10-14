---
title: Consumer Demonstrator
keywords: system, demonstrator
tags: [system,demonstrator]
sidebar: overview_sidebar
permalink: system_demonstrator.html
summary: "Consumer demonstrator implementation of the GP Connect FHIR APIs."
---

## Objective ##

Take the [Ripple](http://rippleosi.org/){:target="_blank"} open source record viewer and use it to demonstrate the GP Connect APIs to validate and accelerate delivery of the GP Connect APIs. The demonstrator would act as a mock Consuming application to show how the data made available by the APIs could be used. 

## Methodology ##

- [Answer Digital](http://www.answerdigital.com/){:target="_blank"} has undertaken seven development sprints and seven releases.
- Iterative and rapid design in collaboration with [NHS Digital](http://digital.nhs.uk/){:target="_blank"}. 
- Requirements driven by supplier workshops and FHIR&reg; standard releases.
- [Open source artefacts on GitHub](https://github.com/nhs-digital/gpconnect){:target="_blank"} for later re-use.
- Can be extended into more focussed use cases in the future (e.g. testing, assurance tooling, developer tools).
- Using the [HAPI open-source FHIR library](http://hapifhir.io/){:target="_blank"} to bootstrap FHIR compliance.

## System Architecture ##

![API Consumer talking to API Provider via the Spine Security Proxy](images/systems/API Consumer talking to API Provider via the Spine Security Proxy.png)

## Current Status ##

We now have a functioning user interface that can drive interactions with the FHIR-based APIs to:

- Access Record (HTML) across the 11 defined record sections <br/>(date range searching and/or paging are not currently implemented).
- Appointment Management for a patient across practice diaries.
- Task Management for a patient across organisational boundaries.

## Online System ##

View the latest build of the [GP Connect Demonstrator](http://ec2-54-194-109-184.eu-west-1.compute.amazonaws.com/){:target="_blank"} online now!

{% include tip.html content="All data held in the GP Connect Demonstrator is a cleared down and reseeded each night to allow for easier testing. <br/>Please refer to the Demonstrator's in-built help for further details." %}

## Example Screens ##

![GP Connect Demonstrator Patient Summary](images/systems/GP Connect Demonstrator Patient Summary.png)
