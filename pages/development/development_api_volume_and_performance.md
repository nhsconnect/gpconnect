---
title: Volumetric & Performance
keywords: development
tags: [development]
sidebar: overview_sidebar
permalink: development_api_volume_and_performance.html
summary: "Details of the API volume and performance characteristics."
---

## Volumetrics ##

{% include todo.html content="Coming Soon..." %}

## Performance ##

### Command APIs ###

A command API is any API which performs a user initiated operation with a side-effect (i.e. booking an appointment, registering a patient etc.). 

Provider systems SHALL process command API calls in &lt;250ms.

Provider systems SHOULD process command API calls in &lt;100ms, as this is the limit beyond which a user no longer feels that the system is reacting instantaneously.

### Query APIs ###

A query API is any API which performs a user initiated retrival of data without any side-effects (i.e. searching for a patient's medication history).

Provider systems SHOULD process query API calls in &lt;1000ms, as this is the limit beyond which a user feels their workflow has been interrupted.

Provider systems SHALL process query API calls in &lt;3000ms.

## External Documents / Policy Documents ##

| Name | Author | Version | Updated |
| TODO | NHS Digital | v1.0 | 01/08/2016 |
