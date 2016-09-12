---
title: End to End SSP Latency Is Negligible
keywords: spine testing demonstrator integration
tags: [news,testing,integration]
sidebar: overview_sidebar
permalink: news_SSP_latency_tests.html
summary: "Volume and load testing confirms the Spine Security Proxy introduces negligible latency."
---

We recently performed some volume and load testing on the [Spine Security Proxy](integration_spine_security_proxy.html) and the non-functional test team have drawn up a timing sequence diagram to summaries and illustrate the results:

![Spine Security Proxy Timings](images/integration/Spine Security Proxy Timings.png)

*Note: The '858 ms' responder delay simulates a response being generated but will vary depending on the responding systems ability to produce the required content.*

<br>
As you can see from the diagram the SSP introduces around a 15ms "Spine imposed delay" into the end-to-end communication process. As we're utilising chunked streaming of the response payload back to the consumer system this latency is basically constant across all message sizes. This is great news as a 15ms latency is orders of magnitude below what a human can percieve and is to all intents and purposes negligible from a systems point of view.