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

## Volume and Performance Testing ##
 
Suppliers of Provider solutions are expected to undertake provider led V&P testing of their solutions.  
 
### V&P Testing Model ### 
Suppliers SHALL submit for review a high level V&P testing model document that covers the stages of testing, details of the environment and how they intend to test.
 
Suppliers' test approaches SHOULD include a LOAD and a RAMP test and ideally a SOAK test.  Suppliers SHALL supply comprehensive results of the test including timings for round trip API call/response against the message sizes used and the tps at the time of the request was made.

### V&P Testing Infrastructure Scaling ###

Predictive models of load have are provided to give an indication of the likely volume and profile of full production roll out.

If suppliers are scaling their infrastructure solution over time (such as during First of Type) then the V&P testing must be performed and submitted for review.

Suppliers of provider solutions are expected to scale their infrastructure solutions in line with delivering services within the SLA and using the V&P Testing to proactively monitor and add infrastructure before it is saturated/overloaded.

A plan outlining the points at which infrastructure will be scaled up should be provided after V&P testing is performed.

 
### V&P Test Environment ###
Test environments SHALL simulate consumer applications making API calls against simulated test data (patient records, diaries, tasks etc) 
 
Test data SHALL be populated with realistic complexity, depth and volume, i.e. in the case of patients the data should be representative of clinical records of a mix of healthy patients and patients with multiple long term conditions.  

If a small set of test data is repeatedly used as part of the V&P tests then test setup SHOULD seek to minimise the effects of caching e.g. within API middleware (the data from a small number of patients repeatedly queried in quick succession could be served from cache which would invalidate test results).  
 
### Volumetric Model ###
Suppliers SHOULD test API call volumes against the provided Volumetric Model (linked spreadsheet).  For phases after the initial tranche(s) of First of Type deployments, it is anticipated that a standard GP Connect automated test harness will be made available to test the provider APIs according to the volumetric model*.
 
During the LOAD test, the timings for end to end API calls SHALL NOT exceed the maximum stated (250ms for command APIs, 3000ms for query APIs) and SHOULD NOT exceed the lower limits (100ms and 1000ms respectively).
 
Results for the RAMP test SHALL include the tps and message size profile at the threshold where the above limits were exceeded, if applicable. 
 
If a SOAK test is performed, results SHALL be provided.  
 
*note the test profile differs according to the supplier, based on the proportion of patient population whose GP records are held with that supplier.  It would not be fair to test a large supplier's system against a usage profile based on the population of a small supplier.


## External Documents / Policy Documents ##

| Name | Author | Version | Updated |
| TODO | NHS Digital | v1.0 | 01/08/2016 |
