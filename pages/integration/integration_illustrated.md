---
title: Spine integration Illustrated
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
- [Spine Security Proxy (SSP)](integration_spine_security_proxy.html)

To illustrate this, an example is given below of all the steps required to consume GP Connect capabilities. For full details, please refer to the relevant Spine service pages:

## Example: Integrate with Spine to book an appointment at a GP practice ##

The following sequence diagram illustrates all the steps which a GP Connect consumer would be required to undertake in order to book an appointment at a GP practice:

![Sequence diagram for booking an appointment end to end interactions](images/integration/integration_sequence_diagram.png)

The steps shown in the diagram are detailed below:

| Step | Description |
|------|-------------|
|      | *Step 1 is optional in the sense that a cached version of previous trace results may be available to the consumer.* |    
| 1a   | **Consumer** is responsible for performing a  [(PDS)](integration_personal_demographic_service.html) trace to both verify the NHS Number and obtain the ODS code of the GP practice system. |
| 1b   | **PDS** returns NHS Number verification status, and the ODS code of the GP practice system. |
|      |      |
|      | *Step 2 is optional in the sense that cached or configured endpoint details for the practice may be available from a previous SDS interaction.* |    
| 2a   | **Consumer** calls [SDS](integration_spine_directory_service.html) to discover the accredited system ID (ASID) of the system which provides a FHIR endpoint at the practice identified by the specified ODS code. |
| 2b   | **SDS** returns the ASID. | 
| 2c   | **Consumer** calls Spine Directory Service again to discover the URL of the FHIR server endpoint at the practice. | 
| 2d   | **SDS** returns details of the FHIR endpoint. | 
|      |      |
|      | *Step 3 is optional in the sense that the capability statement may be used to verify the FHIR capabilities which the endpoint provides, should this be required at run time. The results of this call may be cached for future interactions.* |    
| 3a   | **Consumer** calls the [metadata endpoint](foundations_use_case_get_the_fhir_capability_statement.html) at the practice FHIR server to request full details of which FHIR operations are implemented at that server - the capability statement. |
| 3b   | **Spine Security Proxy (SSP)** receives the call from the consumer, performs security checks, and if these pass, forwards the consumer request to the provider. |
| 3c   | **Provider** returns the capability statement to the SSP. |
| 3d   | **SSP** forwards the capability statement received from the provider to the consumer. |
|      |      |
| 4a   | **Consumer** then makes an API call to [search for free slots](appointments_use_case_search_for_free_slots.html) at the practice in the specified timeframe. |
| 4b   | **SSP** forwards the call from the consumer, performs security checks and, if these pass, forwards the consumer request to the provider. |
| 4c   | **Provider** responds with details of what slots are available for booking. Should no applicable slots be returned, the consumer may make repeated calls to [search for free slots](appointments_use_case_search_for_free_slots.html) with amended date ranges. |
| 4d   | **SSP** forwards the free slots received from the provider to the consumer. |   
|      |      |
| 5a   | **Consumer** makes API call to [find a patient](foundations_use_case_find_a_patient.html) providing the patient's NHS Number. |
| 5b   | **SSP** receives the call from the consumer, performs security checks, and if these pass, forwards the consumer request to the provider. |
| 5c   | **Provider** finds patient record and returns the logical identifier of the patient record at this practice in their system. See [Patient record not present](appointments_consumer_sessions.html#consumer-session---booking-an-appointment---no-patient-record) for an illustration of the steps required in this case. |
| 5d   | **SSP** forwards the patient details received from the provider to the consumer. |
|      |      |
| 6a   | **Consumer** calls [Book an appointment](appointments_use_case_book_an_appointment.html) indicating the slots selected in the UI together with the logical ID of the patient. |
| 6b   | **SSP** forwards the call from the consumer, performs security checks and, if these pass, forwards the consumer request to the provider. |
| 6c   | **Provider** responds with details of the booked appointment as confirmation of success. |
| 6d   | **SSP** forwards the appointment details received from the provider to the consumer. |
