---
title: Volumetric and performance
keywords: development
tags: [development]
sidebar: overview_sidebar
permalink: development_api_volume_and_performance.html
summary: "Details of the API volume and performance (V&P) characteristics"
---

## Volumetrics ##

{% include important.html content="The fundamental principle of the approach is to flex the parameters and model as we develop, deploy and understand how the NHS is using the service. Therefore, learnings from the First of Type and Fast Followers are key. We have based usage on population covered by each deployment and some real-world figures around percentage of population in contact with the NHS on a daily basis and then some parameters around how many record reads per encounter. This is all parameter driven so we can adjust the model as we deploy and start to gather actual usage information." %}

{% include download.html content="Draft GP Connect API [volumetric model](downloads/testing/HSCIC.GPSOC.GPCONNECT.API.CallUsageModelTotals.xlsx) sent to principle suppliers on the 2 September 2016." %}

Provider systems SHALL NOT use this volumetric model as a 'gold standard' but MAY use it as the basis of developing their own volumetric models.

### Scalability ###

Provider systems SHALL through V&P profiling and solution assurance activities demonstrate how the system can scale as demand increases.

## Performance ##

### Command APIs ###

A command API is any API which performs a user-initiated operation with a side-effect (for example, booking an appointment, registering a patient). 

Provider systems SHALL process command API calls in &lt;250ms.

Provider systems SHOULD process command API calls in &lt;100ms, as this is the limit beyond which a user no longer feels that the system is reacting instantaneously.

### Query APIs ###

A query API is any API which performs a user-initiated retrieval of data without any side-effects (for example, searching for a patient's medication history).

Provider systems SHOULD process query API calls in &lt;1000ms, as this is the limit beyond which a user feels their workflow has been interrupted.

Provider systems SHALL process query API calls in &lt;3000ms.

## Volume and performance testing ##
 
Suppliers of provider solutions are expected to undertake provider-led V&P testing of their solutions.  
 
### V&P testing model ### 
Suppliers SHALL submit for review a high-level V&P testing model document that covers the stages of testing, details of the environment and how they intend to test.
 
Suppliers' test approaches SHOULD include a LOAD and a RAMP test and ideally a SOAK test.  Suppliers SHALL supply comprehensive results of the test including timings for round-trip API call/response against the message sizes used and the TPS at the time of the request was made.

### V&P testing infrastructure scaling ###

Predictive models of load are provided to give an indication of the likely volume and profile of full production roll-out.

If suppliers are scaling their infrastructure solution over time (such as during First of Type) then the V&P testing must be performed and submitted for review.

Suppliers of provider solutions are expected to scale their infrastructure solutions in line with delivering services within the service level agreement (SLA) and using the V&P testing to proactively monitor and add infrastructure before it is saturated/overloaded.

A plan outlining the points at which infrastructure will be scaled up should be provided after V&P testing is performed.

### V&P test environment ###

Test environments SHALL simulate consumer applications making API calls against simulated test data (such as, patient records, diaries.) 
 
Test data SHALL be populated with realistic complexity, depth and volume - for example, in the case of patients the data should be representative of clinical records of a mix of healthy patients and patients with multiple long-term conditions.  

If a small set of test data is repeatedly used as part of the V&P tests then test setup SHOULD seek to minimise the effects of caching - for example, within API middleware (the data from a small number of patients repeatedly queried in quick succession could be served from cache which would invalidate test results).  
 
### Volumetric model ###

Suppliers SHOULD test API call volumes against a refined volumetric model<sup>1</sup>.
 
During the LOAD test, the timings for end-to-end API calls SHALL NOT exceed the maximum stated (250ms for command APIs, 3000ms for query APIs) and SHOULD NOT exceed the lower limits (100ms and 1000ms respectively).
 
Results for the RAMP test SHALL include the TPS and message size profile at the threshold where the above limits were exceeded, if applicable. 
 
If a SOAK test is performed, results SHALL be provided.  
 
<sup>1</sup>**Note:** V&P test profiles will differ according to the supplier based on the proportion of patient population whose GP records are held with that supplier.
