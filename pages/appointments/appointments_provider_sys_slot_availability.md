---
title: Slot Availability Management
keywords: development
sidebar: appointments_sidebar
toc: false
permalink: slotavailabilitymanagement.html
summary: "Requirements for Provider System End-User to be able to configure what slots are available to GP Connect Consumers"
---

Given the increasing need for cross-organisational appointment access, there is a requirement to better ensure that the right appointment slots are made available to the right external organisations by
  - enhancing the ability of Provider Organisations to control appointment availability and booking to, and by, external organisations
  - ensuring that Consumer organisations obtain only appointment availability appropriate for them
  - providing more standardised categorisation of available appointment slots across provider systems so that inappropriate appointment booking is reduced
  - providing where applicable the GP Branch Surgery location of available appointment slots.
  
## Appointment Availability Control by Organisation Type and Specific Organisations ##

Provider systems SHALL:
- enable end-users to designate the Slots within their appointment books as 'GP Connect bookable' a broad control to make slots in the appointment book, bookable through the GP Connect API
- enable end-users to additionally specify which schedules/slots can be booked by an individual organisation and/or group of organisations, and/or booking organisation type as well as enabling end-users to limit the number of slots which can be booked by this 'organisation access profile'

The end-user SHALL be presented with an 'Organisation Type' list which reflect the NHS Digital [FHIR Organisation Type](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-OrganisationType-1) value set.

The consumer system SHOULD send the booking Organisation Type and booking organization ODS Code in the 'SearchFilter' parameter, as specified in the [Search Free Slots](appointments_use_case_search_for_free_slots.html) page, which the Provider system will then use to determine the matching availability.

## Booking Window/Embargo ##
It is recommended that Provider systems also provide the functionality to enable the end-user to control how far in advance external organisations should be allowed to book slots and how near to the actual slot time - ie via 'Booking Window' or 'Embargo' rules.

Where such rules have been set, the Provider systems SHALL only return slots in respect of the rules.

## Appointment Slot Categorisation ##

Providers systems SHALL enable and require the mandatory selection by end-users of a 'Practitioner Role' and 'Delivery Channel' for the schedules/slots as part of the end-user GP Connect Appointment configuration.

- The 'Practitioner Role' list SHALL reflect the NHS Digital [Practitioner Role](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-PractitionerRole-1) value set.
- The 'Delivery Channel' list SHALL reflect the NHS Digital [Delivery Channel](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-DeliveryChannel-1) value set.
- Provider systems SHALL maintain alignment with the value sets.
- These values SHALL NOT be configurable/modifiable by end-users.


## Branch Surgery Location ##

The Schedule resource has a mandatory 'Location' reference within the actor element. The referenced location SHALL be populated by the provider systems with the name and address of the location where the appointment will take place, either the GP Practice where there are no branch surgeries OR the branch surgery including ODS Site Code where available.

