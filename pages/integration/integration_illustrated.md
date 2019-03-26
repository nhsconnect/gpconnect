---
title: Spine integration illustrated
keywords: spine, pds, ssp, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_illustrated.html
summary: "Illustration of the use of the GP Connect API showing all interactions required - both with Spine services and GP Connect endpoint API calls."
---

## Spine integration required to consume GP Connect capabilities ##

GP Connect provider APIs are accessed through the NHS Spine. As such, consumers of GP Connect APIs are required to integrate with the following Spine services as a pre-requisite to making API calls to GP Connect provider APIs:

- [Personal Demographics Service (PDS)](integration_personal_demographic_service.html)
- [Spine Directory Service (SDS)](integration_spine_directory_service.html)
- [Spine Security Proxy (SSP)](integration_spine_secure_proxy.html)

To illustrate this, an example is given below of all the steps required consume GP Connect capabilities. For full details, please refer to the relevant spine service pages.

## Example: Integrate with Spine to retrieve a care record in HTML format ##

The following sequence diagram illustrates all the steps which a GP Connect consumer would be required to undertake in order retrieve a care record in HTML format

![Sequence diagram for booking an appointment end to end interactions](images/integration/Spine_Integration_Illustrated_AccessRecordHTML.png)

The steps shown in the diagram are detailed below.

| Step | Description |
|------|-------------|
|      | *Step 1 is optional in the sense that a cached version of a previous these trace results may be available to the consumer.* |    
| 1a   | **Consumer** is responsible for performing a  [Personal Demographics Service(PDS)](integration_personal_demographic_service.html) Trace to both verify the NHS Number and obtain the ODS code of the GP Practice system. |
| 1b   | **PDS** returns NHS Number verification status, and the ODS code of the GP Practice system. |
|      | *Step 2 is optional in the sense that cached or configured endpoint details for the Practice may be available from a previous SDS interaction.* |    
| 2a   | **Consumer** calls Spine Directory Service again to discover the URL of the FHIR server endpoint at the practice | 
| 2b   | **SDS** returns details of the FHIR endpoint. | 
| 2c   | **Consumer** calls [Spine Directory Service (SDS)](integration_spine_directory_service.html) to discover the Accredited System ID (ASID) of the system which provides a FHIR endpoint at the practice identified by the specified ODS code. |
| 2d   | **SDS** returns the ASID. |
|      | *Step 3 is optional in the sense that the conformance profile may be used to verify the capability which the endpoint provides should this be required at run time. The results of this call may be cached for future interactions.* |    
| 3a   | **Consumer** calls the [metadata endpoint](foundations_use_case_get_the_fhir_conformance_profile.html) at the practice FHIR server to request full details of which FHIR operations are implemented at that server - the Conformance Profile. |
| 3b   | **Spine Security Proxy (SSP)** receives the call from the Consumer, performs security checks, and if these pass, forwards the consumer request to the provider. |
| 3c   | **Provider** returns the Conformance Profile to the SSP. |
| 3d   | **SSP** forwards the Conformance Profile received from the Provider to the Consumer. |
| 4a   | **Consumer** then makes an API call to [Retrieve a care record section](accessrecord_use_case_retrieve_a_care_record_section.html) at the practice in the specified time-frame. |
| 4b   | **SSP** forwards the call from the Consumer, performs security checks, and if these pass, forwards the consumer request to the provider. |
| 4c   | **Provider** responds with the requested details of the care record. |
| 4d   | **SSP** forwards the requested details of the care record to the Consumer. | 
