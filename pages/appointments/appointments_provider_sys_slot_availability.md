---
title: Slot Availability Management
keywords: development
sidebar: appointments_sidebar
toc: false
permalink: slotavailabilitymanagement.html
summary: "Requirements for Provider System End-User to be able to configure what slots are available to GP Connect Booking Organisation Consumers"
---

Given the increasing requirement for cross-organisational appointment access, there is a requirement to better ensure that the right appointment slots are made available to the right external organisations by
  - enhancing the ability of Provider Organisations to control appointment availability and booking to, and by, external organisations
  - ensuring that Consumer organisations obtain only appointment availability appropriate for them
  - providing more standardised categorisation of available appointment slots across provider systems so that inappropriate appointment booking is reduced.
  
## Appointment Availability Control by Organisation Type, Specific Organisations ##
Provider systems SHALL, in addition to enabling end-users to designate the Slots within their Appointment books as 'GP Connect bookable', provide the following additional functionality:
  - enable end-users to specify which appointment schedules/slots can be booked by an individual organisation and/or group of organisations, and/or booking organisation type
  - limit the number of slots which can be booked by this 'organisation access profile'
  
The Organisation Type list from which the end-user selects SHALL reflect the specified FHIR Organisation Type value set. 

The consumer system will send the booking Organisation Type and ODS Code in the Search Free Slots API SearchFilter which the Provider system will then use to determine the matching availability.

## Booking Window/Embargo ##
It is recommended that Provider systems also provide the functionality to enable the end-user to control how far in advance external organisations should be allowed to book slots and how near to the actual slot time - ie via 'Booking Window' or 'Embargo' rules.

Where such rules have been set, the Provider systems SHALL only return slots in respect of them.

## Appointment Slot Categorisation ##

Providers systems SHALL enable and require the mandatory selection by end-users of a value from the new FHIR 'Practitioner Role' and 'Delivery Channel' value set, as part of the end-user GP Connect Appointment configuration. These values SHALL NOT be configurable by end-users.

## FHIR Value Sets - Organisation Type, Practitioner Role, Delivery Channel  ##

Provider systems SHALL maintain alignment with the CareConnect FHIR value sets.

