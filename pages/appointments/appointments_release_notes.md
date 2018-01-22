---
title: Appointments Release Notes
keywords: appointments, release notes
tags: []
sidebar: appointments_sidebar
permalink: appointments_release_notes.html
summary: "Release notes for the various versions of the Appointment Management capability."
---

#### 1.0.0-rc.4 (Released: )

- [Appointment Management](appointments.html)
  - The "[Implementation And Testing](appointments.html#implementation-and-testing)" section has been added to indicate the best approach for implementing the appointment management capability pack.
- [Book an appointment](appointments_use_case_book_an_appointment.html)
  - Added note regarding the inclusion of `patient temporary contact details` for the purposes of the appointment and where to include them in the appointment resource.
  - Added additional guidance around the must-support requirement for the bookingOrganization element within the appointment resource.
- [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html)
  - Added additional wording to make clear the expectations around a search where no search prefix is included in the request parameter.
  
#### [1.0.0-rc.3 (Released: 28/11/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_rc.3_Foundations_rc.4_GP_Connect_rc.1) 

{% include important.html content="Release 1.0.0-rc.3 contains a change of FHIR version from DSTU2 to STU3 as the base fhir version for the GP Connect API Capbility." %}

- [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html) 
  - Uplifted to STU3 profiles.
  - Updated the wording and examples relating to the `start` search parameter(s) to clear up the expectations and remove the mis- leading wording around start and end of the date range
  - Updated wording to reflect the decision that only a Patient's future appointments should be available via GP Connect
  - [Payload Response Body](appointments_use_case_retrieve_a_patients_appointments.html#payload-response-body) - Added requirement to only return appointments in the future.
- [Search for free slots](appointments_use_case_search_for_free_slots.html)
  - Uplifted to STU3 FHIR profiles for all resources
  - Available Slot Filtering:  Added requirement for Provider Systems to immediately support filtering of available slots such that only those bookable via GP Connect are provided, with strong indication that more granular slot availability control will be required to through the use of a newly added place-holder parameter called searchFilter.
  - `freeBusyType` has changed to `status`
  - The Practitioner reference has moved in the schedule resource from an extension to `Schedule.actor`
- [Read an appointment](appointments_use_case_read_an_appointment.html) 
  - Uplifted to STU3 profiles.
  - Updated requirements that only future appointments may be read by a consumer and the provider should return and error if the consumer tries to read a past appointment.
- [Book an appointment](appointments_use_case_book_an_appointment.html) 
  - Uplifted to STU3 profiles
  - The 'create' extension has become the standard 'created' element within the Appointment resource
  - Added guidance for providers that do not support both Appointment Description and Appointment Comment to append the received comment string to the mandatory description element 
- [Amend an appointment](appointments_use_case_amend_an_appointment.html) 
  - Uplifted to STU3 profiles
  - Updated wording to reflect the decision that only a Patient's future appointments should be available via GP Connect
  - Added guidance for providers that do not support both Appointment Description and Appointment Comment to append the received comment string to the mandatory description element
  - Updated requirements that only future appointments may be amended by a consumer and the provider should return and error if the consumer tries to amend a past appointment.
- [Cancel an appointment](appointments_use_case_cancel_an_appointment.html)
  - Uplifted to STU3 profiles
  - Updated requirements that only future appointments may be cancelled by a consumer and the provider should return and error if the consumer tries to cancel a past appointment.
  
- [Introduction](appointments.html)
  - Uplifted wording to reflect inclusion of Urgent Care deployment setting
  - Uplifted wording to reflect requirement for Provider Systems to filter slot availability so that the ones available via GP Connect can be controlled by the Practice, with indication of further requirement to support more granular Appointment Slot Control 

- [Clinical scenarios](appointments_clinical_scenarios.html)
  - Uplifted wording to include the GP Practice requirement to control slot availability via GP Connect 
  - Uplifted wording to reflect the decision that only a Patient's future booked appointments should be available via GP Connect
 
- [Design Decisions](appointments_design.html#viewing-and-amending-booked-appointments)
  - Uplifted wording to reflect the decision that only a Patient's future booked appointments should be available for viewing/amending via GP Connect
  - Uplifted wording to reflect the decision that Patient Dissent to Share will NOT be applied for this capability

- [Information Governance](appointments_ig.html)
  - New page to describe the IG controls to be applied in the Appointment Management Capability

#### [1.0.0-rc.2 (Released: 13/10/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_Management_rc.2_release)

  ***Specification Updates***
  - [Appointment Management](appointments.html), [Search for free slots](appointments_use_case_search_for_free_slots.html), [Operation Guidance](development_fhir_operation_guidance.html) - Changed to the InteractionId for "Search for free slots" to reflect move to restful endpoint instead of operation.
  - [Search for free slots](appointments_use_case_search_for_free_slots.html#search-parameters) - Updated formatting of search for free slots page and added clarification around the use of start and end parameters.
  - [Book an appointment](appointments_use_case_book_an_appointment.html#payload-request-body) - Added guidance around use of bookingOrganization and creation dateTime extension within appointment resource.
  - [Search for free slots](appointments_use_case_search_for_free_slots.html#search-parameters) - Added `disposition` and `service-id` search parameters for urgent care use cases.
  - [Appointments - Consumer Sessions Illustrated](appointments_consumer_sessions.html), [Spine Integration Illustrated](integration_illustrated.html) - Added pages to highlight the sequence of interactions required to perform common business processes using the GP Connect API.
  
  ***Profile Updates***
  - [gpconnect-appointment-1](https://fhir.nhs.uk/StructureDefinition/gpconnect-appointment-1) - Added `bookingOrganization` extension and `created` extension within appointment resource profile.

#### [1.0.0-rc.1 (Released: 22/09/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_rc.1_and_Foundations_rc.3_release)
  - [Book an appointment](appointments_use_case_book_an_appointment.html#payload-request-body), [Search for free slots](appointments_use_case_search_for_free_slots.html#payload-response-body) - Additional information has been added on how providers should indicate that slots are adjacent and therefore can be used for multi slot appointment booking by consumers.
  - [Design Decisions](appointments_design.html) - API will not provide appointment re-scheduling through a single API interaction.
  - [Book an appointment](appointments_use_case_book_an_appointment.html#payload-request-body) - where participants are specified in request body, these must include a actor resource reference.
  - [Amend Appointment](appointments_use_case_amend_an_appointment.html#error-handling) - Uplifted error handling guidanace around modification of appointment resource elements.
  - [Amend Appointment](appointments_use_case_amend_an_appointment.html#payload-request-body) - Changed specification to clarify which fields may be amended.
  - [Book an appointment](appointments_use_case_book_an_appointment.html), [Common API Guidance](development_fhir_api_guidance.html#managing-return-content) - Moved and uplifted guidance on resource state from book appointment to common api guidance.
  - [Search for free slots](appointments_use_case_search_for_free_slots.html) - Provider will return only details of free slots which have a date/time span fully within the time period specified
  - [Book an appointment](appointments_use_case_book_an_appointment.html#error-handling) - Added guidance around providers right to implement business rules to prevent misuse of the appointment booking api.
  - [Amend an appoinment](appointments_use_case_amend_an_appointment.html) - Clarity on use of PUT verb and the effect on the resultant state of the `Appointment.reason` element.
  - [Search for free slots Use Case](appointments_use_case_search_for_free_slots.html), [Appointment Management Resources](datalibraryappointment.html#search-for-free-slots) - Changed "Search for free slots" from a fhir operation to restful call.

#### [1.0.0-beta.2 (Released: 08/09/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_beta.2_and_Foundations_rc.2_release)
  - Removed practitioner participant as a mandatory element within the appointment resource (Page - Book an appointment).
  - Added location participant as a mandatory element within the appointment resource (Page - Book an appointment).
  - Updated datalibrary to be capability specific, moving it to reside under the "Development" menu within the capability. This is to allow the Profiled FHIR Resources to be referenced per capability and updated independantly. For Appointment Management we have updated specification to reference FHIR profiles stored on FHIR reference server rather than those on the old DMS capability pack.
  - Updated book appointment with guidance on use of the comment and description elements within the resource.
  - Updated search prefixes listed on "Retrieve a patient's appointments" page, within Appointment Management API Use Case section, to align with common API guidance, removed "ne" search prefix and added the "eq" search prefix. Also updated the link to the Common API Guidance page to directly link to the search section.
  - Corrected examples on API Use Cases pages to include FHIR Resource Profile in the returned FHIR resources.
  - Added clarification on the expected response when the [Search for free slots](appointments_use_case_search_for_free_slots.html) API use case does not return any free slots for the requested time period.
  - Updated API Use Case pages to make clear the expectations around the FHIR Resource Metadata Profile element, along with updates to examples to show new profile definitions.
  - Added clarification around GP Connect "FHIR Resource Profile" and "Metadata Profile" requirements on the request/consumer side of the [Book an Appointment](appointments_use_case_book_an_appointment.htm), [Amend  an Appointment](appointments_use_case_amend_an_appointment.html) and [Cancel an appointment](appointments_use_case_cancel_an_appointment.html) API use cases. 
  - Added clarification on the expected response content for the [Retrieve a Patient's Appointments](appointments_use_case_retrieve_a_patients_appointments.html) API use case.
  - Additional detail on error conditions for [Read an appointment](appointments_use_case_read_an_appointment.html)
  - [Cancel an appointment](appointments_use_case_cancel_an_appointment.html) API use case associated with cancel an appointment interaction
  - [Book an appointment](development_fhir_api_guidance.html#create-resource) emphasised requirement for provider to return Location header describing details of the newly created resource.
  - [Retrieve a patient's appointments](appointments_use_case_retrieve_a_patients_appointments.html#payload-response-body) includes guidance on what data items should be returned where date range parameters are ommitted in the request querystring.
  - [Search for free slots](appointments_use_case_search_for_free_slots.html) - updated identifier system within examples to match identifiers within new fhir profiles
  - Added [design decision](appointments_design.html) to clarify responsibilities for consumer, SSP and provider in an implementation which provides a federated appointment management capability. 
  - [Amend Appointment](appointments_use_case_amend_an_appointment.html), [Book Appointment](appointments_use_case_book_an_appointment.html), [Cancel Appointment](appointments_use_case_cancel_an_appointment.html), [Read Appointment](appointments_use_case_read_an_appointment.html), [Retrieve a patiens appointments](appointments_use_case_retrieve_a_patients_appointments.html), [Search for free slots](appointments_use_case_search_for_free_slots.html) - Added C# and Java code examples for all the appointment management API Use Cases.
  - [Book and appointment](appointments_use_case_book_an_appointment.html#consumer) - Added clarification around the prerequisites, indicating that the consumer should have performed a "Find a patient" request to obtain the patient logical identifier on the fhir server.
  - [Amend Appointment](appointments_use_case_amend_an_appointment.html), [Book Appointment](appointments_use_case_book_an_appointment.html), [Cancel Appointment](appointments_use_case_cancel_an_appointment.html), [Read Appointment](appointments_use_case_read_an_appointment.html), [Retrieve a patiens appointments](appointments_use_case_retrieve_a_patients_appointments.html), [Search for free slots](appointments_use_case_search_for_free_slots.html) - Uplifted examples to use correct urls and elements.
  
#### 1.0.0-beta.1
  - Initial release of the Appointment Management capability pack on Github in early August 2016.
  
#### 1.0.0-alpha.1
  - Initial release for feedback/comments as part of the late May 2016 release.
  
