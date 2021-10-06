---
title: Service filtering introduction
keywords: appointments design
tags: [design,appointments]
sidebar: appointments_sidebar
permalink: appointments_service_filtering.html
summary: "Introducing the service concept into Appointment Management"
---

## Why is service filtering needed? ##

Appointment Management consumer systems used by NHS 111 use the [Directory of Services (DOS)](appointments_service_discovery.html#directory-of-services-dos---currently-for-uec-consumers-only) in order to determine which service (i.e. practice or GP hub) to book a patient into.

When a user of one these systems chooses a service from DOS to book the patient into and searches for free appointment slots via GP Connect, if service filtering is not enabled at the provider organisation, all GP Connect bookable slots are returned regardless of whether the provider organisation is running more than one service. 

This consumer system user must browse through the slots returned to determine which are related to the service they chose. This is error prone due to the variability in slot naming and may lead to an incorrect booking.

### Booking at a provider organisation with one DOS service ##

This **IS NOT an issue where the provider organisation is only running one service**, such as in this example, since all free slots correspond with the service chosen.

The example below shows a practice with one location providing appointments to its registered patients.

When a consumer system user chooses this service and searches for free slots, all slots shown correspond with the service selected.

<img src="images/appointments/service-and-dos-1.png" />

### Booking at a provider organisation with more than one DOS service ##

This **IS an issue when the provider organisation runs more than one service**.

In the example below the practice is running two services - GP surgery for registered patients, and an extended access hub for its own patients and patients registered to other practices within the local area.

When a consumer system user chooses one of these services and searches for free slots, if service filtering is not enabled at the provider organisation, all GP Connect bookable slots are returned for the organisation - including slots for both services.  The user must now look at the individual slots to work out which are related to the service chosen.

<img src="images/appointments/service-and-dos-2.png" />

Although the slots will be labelled according to the [consumer display requirements](appointments_use_case_search_for_free_slots.html#consumer-display-requirements) and therefore include multiple descriptive fields such as slot type and schedule type, it is not intuitive for the user to receive slots for services not chosen by them, and selecting a slot becomes error prone due to variability in slot type and schedule type naming.  Furthermore it prevents the comissioning rules applied in the DOS service search from functioning correctly - a patient may be booked into a slot for which they are not eligible.

{% include note.html content="Please note the ODS code shown against each DOS service is the ODS code used to determine the GP Connect endpoint, determined according to [these rules](appointments_service_discovery.html#directory-of-services-dos---currently-for-uec-consumers-only), and may not be the same as the 'main' ODS code field on the DOS service." %}

## Service filtering - the solution ##

The solution to this problem is to introduce the service concept to Appointment Management - in short -

- for consumer systems to send DOS service ID in a slot search, where a service has been chosen from the DOS
- for provider systems to:
  - introduce the service concept to their appointment books, and allow users to link appointment schedules to services
  - filter slots in the [Search for free slots](appointments_use_case_search_for_free_slots.html) response using the DOS service ID sent by the consumer

{% include important.html content="The full list of changes required for service filtering are best viewed on the [1.2.8 release note](overview_release_notes_1_2_8.html)." %}

The example below shows the provider organisation has defined two services in their system corresponding with the services they provide in DOS.  The unique service IDs (taken from DOS) are added to the services defined in the provider system.

<img src="images/appointments/service-and-dos-3.png" />

When a slot search occurs from a consumer that has sent a DOS service ID in the request, only slots linked to the service with a matching service ID are returned.


## When will service filtering be used? ##

Consumer systems sending a DOS service ID in the Search for free slots request will receive slots only for that service where:

- the provider system has deployed the service filtering functionality
- AND the provider organisation has set their service filtering enablement switch to ON

### Rollout and scope ###

Service filtering will be enabled gradually across GP Connect provider organisations, starting with organisations that run GP access hubs.

Practices with branch surgeries are currently out of scope due to a current restriction (Sep 2021) in the DOS search results - DOS services representing branch surgeries are not currently returned in the DOS search results in most circumstances.

## When will service filtering NOT be used? ##

### Consumers that do not use the DOS ###

Consumer systems that do not use the DOS to locate a service will continue to search for free slots without a service ID and therefore receive slots back from the provider organisation as a whole, regardless of whether they are running multiple services.

This also applies to consumer systems that do use the DOS, but where the user has chosen not to use the DOS as part of the current booking - for example where they are booking directly into the patient's registered practice without searching the DOS for a suitable service.

### Service filtering functionality is not yet deployed at a provider organisation ###

Where the provider organisation's system supplier has not yet implemented or deployed a version of their software which implements service filtering, their software will ignore the service ID parameter in the slot search - and slots will be returned for all services run by the provider organisation.

### Service filtering is not enabled at a provider organisation ###

To support the rollout of service filtering, a service filtering enablement switch (defaulted to OFF) is present in each provider organisation.

This allows the provider organisation to set up their list of services, and link them to appointment schedules before they switch service filtering on.

If the provider organisation has not enabled service filtering, the service ID parameter will be ignored in the slots search and slots will be returned for all services.  The Search for free slots response message includes a [filtering status field](appointments_use_case_search_for_free_slots.html#payload-response-body) which allows the consumer system to determine whether service filtering was applied or not.
