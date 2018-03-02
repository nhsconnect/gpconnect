---
title: Slot Availability Management
keywords: development
sidebar: appointments_sidebar
toc: false
permalink: appointments_slotavailabilitymanagement.html
summary: "Requirements for Provider System End-User to be able to configure what slots are available to GP Connect Consumers"
---

Given the increasing need for cross-organisational appointment access, there is a requirement to better ensure that the right appointment slots are made available to the right external organisations by
  - enhancing the ability of Provider Organisations to control those appointments which can be booked by external organisations
  - ensuring that Consumer organisations obtain only available appointments which are appropriate to them
  - providing a more standardised categorisation of available appointment slots across Provider systems so that inappropriate appointment booking is reduced
  - providing where applicable the GP branch surgery location of available appointment slots

{% include note.html content="The requirements below only apply for slot availability management so should only apply to the '`Search for free slots`' GP Connect API use case and none of the other GP Connect API use cases such as '`Retrieve a patient's appointments`' or '`Amend an appointment`', for these the returned resources should reflect the complete organization appointment book." %}
  
## Appointment availability control ##

Provider systems SHALL:
- enable Provider system end-users to designate the slots within their appointment books as 'GP Connect bookable'. This is a broad control to make slots in the appointment book available for booking through the GP Connect API
- enable Provider system end-users to additionally specify which schedules/slots can be booked by an individual organisation and/or group of organisations, and/or booking organisation type as well as enabling end-users to limit the number of slots which can be booked by this 'organisation access profile'

The Provider system end-user SHALL be presented with an 'Organisation Type' list which reflects the NHS Digital [FHIR Organisation Type](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-OrganisationType-1) value set.

The consumer system SHOULD send their booking Organisation Type and booking organization ODS Code in the 'SearchFilter' parameter, as specified in the [Search Free Slots](appointments_use_case_search_for_free_slots.html) page, which the Provider system will then use to determine the matching availability.

## Booking window/embargo ##
It is recommended that Provider systems also provide the functionality to enable the Provider system end-user to control how far in advance external organisations should be allowed to book slots and how near to the actual slot time - ie via 'Booking Window' or 'Embargo' rules.

Where such rules have been set, Provider systems SHALL only return slots which respect these rules.

## Appointment slot categorisation ##

Providers systems SHALL enable and require the mandatory selection by Provider system end-users of a 'Practitioner Role' and 'Delivery Channel' for schedules/slots as part of the end-user GP Connect appointment configuration.

- The 'Practitioner Role' list SHALL reflect the NHS Digital [Practitioner Role](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-PractitionerRole-1) value set.
- The 'Delivery Channel' list SHALL reflect the NHS Digital [Delivery Channel](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-DeliveryChannel-1) value set.
- Provider systems SHALL maintain alignment with the value sets.
- These values SHALL NOT be configurable/modifiable by end-users.


## Branch surgery location ##

The Schedule resource has a mandatory 'Location' reference within the actor element. The referenced location SHALL be populated by Provider systems with the name and address of the location where the appointment will take place. This will either be the GP Practice where there are no branch surgeries OR the branch surgery (including ODS Site Code where available).
