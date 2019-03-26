---
title: Spine integration illustrated
keywords: spine, pds, ssp, sds, integration, patient, demographics
tags: [integration]
sidebar: overview_sidebar
permalink: integration_illustrated.html
summary: "Illustration of the use of the GP Connect API showing all interactions required - both with Spine services and GP Connect endpoint API calls."
---

## Spine integration required to consume GP Connect capabilities ##

GP Connect provider APIs are accessed through the NHS Spine. As such, consumers of GP Connect APIs are required to integrate with the following Spine services as a prerequisite to making API calls to GP Connect provider APIs:

- [Personal Demographics Service (PDS)](integration_personal_demographic_service.html)
- [Spine Directory Service (SDS)](integration_spine_directory_service.html)
- [Spine Secure Proxy (SSP)](integration_spine_secure_proxy.html)

To illustrate this, an example is given below of all the steps required consume the GP Connect Appointments capability. For full details, please refer to the relevant spine pages.

## Example: Integrate with Spine to book an appointment at a GP practice ##

The following sequence diagram illustrates all the steps which a GP Connect consumer would be required to undertake in order to book an appointment at a GP practice.

<img src="images/integration/integration_sequence_diagram.png" alt="Sequence diagram for booking an appointment end to end interactions" style="max-width:100%;max-height:100%;">

The steps shown in the diagram are detailed below.

| Step | Description |
|------|-------------|
|      | *Step 1 is optional in the sense that a cached version of a these trace results may be available to the consumer.* |    
| 1a   | **Consumer** is responsible for performing a  [Personal Demographics Service(PDS)](integration_personal_demographic_service.html) Trace to both verify the NHS Number and obtain the ODS code of the GP Practice system. |
| 1b   | **PDS** returns NHS Number verification status, and the ODS code of the GP Practice system. |
|      |      |
|      | *Step 2 is optional in the sense that cached or configured endpoint details for the Practice may be available from a previous SDS interaction.* |    
| 2a   | **Consumer** calls Spine Directory Service again to discover the URL of the FHIR server endpoint at the practice | 
| 2b   | **SDS** returns details of the FHIR endpoint. | 
| 2c   | **Consumer** calls [Spine Directory Service (SDS)](integration_spine_directory_service.html) to discover the Accredited System ID (ASID) of the system which provides a FHIR endpoint at the practice identified by the specified ODS code. |
| 2d   | **SDS** returns the ASID. |
|      |      |
|      | *Step 3 is optional in the sense that the Capability Statement may be used to verify the FHIR capabilities which the endpoint provides should this be required at run time. The results of this call may be cached for future interactions.* |    
| 3a   | **Consumer** calls the [metadata endpoint](foundations_use_case_get_the_fhir_capability_statement.html) at the practice FHIR server to request full details of which FHIR operations are implemented at that server - the Capability Statement. |
| 3b   | **Spine Secure Proxy (SSP)** receives the call from the Consumer, performs security checks, and if these pass, forwards the consumer request to the provider. |
| 3c   | **Provider** returns the Capability Statement to the SSP. |
| 3d   | **SSP** forwards the Capability Statement received from the Provider to the Consumer. |
|      |      |
| 4a   | **Consumer** then makes an API call to [Search for free slots](appointments_use_case_search_for_free_slots.html) at the practice in the specified time-frame. |
| 4b   | **SSP** forwards the call from the Consumer, performs security checks, and if these pass, forwards the consumer request to the provider. |
| 4c   | **Provider** responds with details of what slots are available for booking. Should no applicable slots be returned, the consumer may make repeated calls to [Search for free slots](appointments_use_case_search_for_free_slots.html) with amended date ranges. |
| 4d   | **SSP** forwards the free slots received from the Provider to the Consumer. |   
|      |      |
| 5a   | **Consumer** makes API call to [Find a patient](foundations_use_case_find_a_patient.html) providing the patient's NHS Number. |
| 5b   | **Spine Secure Proxy (SSP)** receives the call from the Consumer, performs security checks, and if these pass, forwards the consumer request to the provider. |
| 5c   | **Provider** finds patient record and returns the logical identifier of the patient record at this practice in their system. See [Patient record not present](appointments_consumer_sessions.html#consumer-session---booking-an-appointment---no-patient-record) for an illustration of the steps required in this case. |
| 5d   | **SSP** forwards the Patient details received from the Provider to the Consumer |
|      |      |
| 6a   | **Consumer** calls [Book an appointment](appointments_use_case_book_an_appointment.html) indicating the slots selected in the UI together with the logical ID of the patient. |
| 6b   | **Spine Secure Proxy (SSP)** forwards the call from the Consumer, performs security checks, and if these pass, forwards the consumer request to the provider. |
| 6c   | **Provider** responds with details of the booked appointment as confirmation of success. |
| 6d   | **SSP** forwards the Appointment details received from the Provider to the Consumer. |
