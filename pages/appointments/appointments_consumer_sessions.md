---
title: Consumer sessions illustrated
keywords: appointments
tags: [appointments,first_of_type]
sidebar: appointments_sidebar
permalink: appointments_consumer_sessions.html
summary: "An illustration of consumer Appointment Management sessions"
---

The Appointment Management consumer application makes use of individual API calls described in 'API use cases' to perform business processes.

## Consumer session - booking an appointment ##

The sequence diagram below illustrates which individual API calls are required by a consumer to book an appointment at a GP practice in the simplest case. It describes interactions of the consumer with the provider FHIR endpoint at the practice, and does not include details of the prerequisite interactions with Spine services. See [Spine integration illustrated](integration_illustrated.html) for details of an end-to-end appointment booking scenario with Spine service interactions included.

![Sequence diagram for booking an appointment - simplest case](images/appointments/sequence_book_simple.png)

| Step | Description                                                                                                                                                                                                                                                                                                              |
| ---- | -----------                                                                                                                                                                                                                                                                                                              |
| 1a   | **Consumer** makes an API call to [Search for free slots](appointments_use_case_search_for_free_slots.html) at the practice in the specified time frame.                                                                                                                                                                  |
| 1b   | **Provider** responds with details of what slots are available for booking. Should no applicable slots be returned, the consumer may make repeated calls to [Search for free slots](appointments_use_case_search_for_free_slots.html) with amended date ranges.                                                          |
|      |                                                                                                                                                                                                                                                                                                                          |
| 2a   | **Consumer** then makes API call to [Find a patient](foundations_use_case_find_a_patient.html) providing the patient's NHS Number.                                                                                                                                                                                       |
| 2b   | **Provider** finds patient record and returns the logical identifier of the patient record at this practice in their system. See [Patient record not present](appointments_consumer_sessions.html#consumer-session---booking-an-appointment---no-patient-record) for an illustration of the steps required in this case. |
|      |                                                                                                                                                                                                                                                                                                                          |
| 3a   | **Consumer** calls [Book an appointment](appointments_use_case_book_an_appointment.html) indicating the slots selected in the UI together with the logical ID of the patient.                                                                                                                                            |
| 3b   | **Provider** responds with details of the booked appointment as confirmation of success.                                                                                                                                                                                                                                 |

## Consumer session - booking an appointment at a collection of federating practices ##

Where a consumer user interface provides a view of available bookings across a collection of federating practices, some steps are repeated for each practice, as shown below:

![Sequence diagram for booking an appointment - no patient found](images/appointments/sequence_book_simple_federated.png)

| Step | Description                                                                                                                                                                                                                                                                                                              |
| ---- | -----------                                                                                                                                                                                                                                                                                                              |
|      | *Repeat step 1 for each federated practice to gain a view of slot availability across the federation*                                                                                                                                                                                                                    |
| 1a   | **Consumer** makes an API call to [Search for free slots](appointments_use_case_search_for_free_slots.html) at the practice in the specified time frame.                                                                                                                                                                  |
| 1b   | **Provider** responds with details of what slots are available for booking. Should no applicable slots be returned, the consumer may make repeated calls to [Search for free slots](appointments_use_case_search_for_free_slots.html) with amended date ranges.                                                          |
|      |                                                                                                                                                                                                                                                                                                                          |
| 2a   | **Consumer** then makes API call to [Find a patient](foundations_use_case_find_a_patient.html) providing the patient's NHS Number.                                                                                                                                                                                       |
| 2b   | **Provider** finds patient record and returns the logical identifier of the patient record at this practice in their system. See [Patient record not present](appointments_consumer_sessions.html#consumer-session---booking-an-appointment---no-patient-record) for an illustration of the steps required in this case. |
|      |                                                                                                                                                                                                                                                                                                                          |
| 3a   | **Consumer** calls [Book an appointment](appointments_use_case_book_an_appointment.html) indicating the slots selected in the UI together with the logical ID of the patient.                                                                                                                                            |
| 3b   | **Provider** responds with details of the booked appointment as confirmation of success.                                                                                                                                                                                                                                 |

## Consumer session - booking an appointment - no patient record ##

![Sequence diagram for booking an appointment - no patient found](images/appointments/sequence_book_no_patient.png)

| Step | Description                                                                                                                                                                                                                                                     |
| ---- | -----------                                                                                                                                                                                                                                                     |
| 1a   | **Consumer** makes an API call to [Search for free slots](appointments_use_case_search_for_free_slots.html) at the practice in the specified time frame.                                                                                                         |
| 1b   | **Provider** responds with details of what slots are available for booking. Should no applicable slots be returned, the consumer may make repeated calls to [Search for free slots](appointments_use_case_search_for_free_slots.html) with amended date ranges. |
|      |                                                                                                                                                                                                                                                                 |
| 2a   | **Consumer** then makes API call to [Find a patient](foundations_use_case_find_a_patient.html) providing the patient's NHS Number.                                                                                                                              |
| 2b   | **Provider** returns zero patient records indicating that the patient with the specified NHS Number does not have a patient record at the practice.                                                                                                             |
|      |                                                                                                                                                                                                                                                                 |
| 3a   | **Consumer** makes API call to [Register a patient](foundations_use_case_register_a_patient.html) providing sufficient details to make a *temporary* registration at the practice.                                                                              |
| 3b   | **Provider** returns the details of the temporarily registered patient, including the logical ID of the new patient record at the practice system, as confirmation of success.                                                                                  |
|      |                                                                                                                                                                                                                                                                 |
| 4a   | **Consumer** calls [Book an appointment](appointments_use_case_book_an_appointment.html) indicating the slots selected in the UI together with the logical ID of the newly created patient record at the practice.                                              |
| 4b   | **Provider** responds with details of the booked appointment as confirmation of success.                                                                                                                                                                        |
