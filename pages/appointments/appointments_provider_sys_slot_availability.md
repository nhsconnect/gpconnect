---
title: Slot availability management
keywords: development
sidebar: appointments_sidebar
toc: false
permalink: appointments_slotavailabilitymanagement.html
summary: "Requirements for provider system end-user to be able to configure what slots are available to GP Connect consumers"
---

Given the increasing need for cross-organisational appointment access, there is a requirement to better ensure that the right appointment slots are made available to the right external organisations by
  - enhancing the ability of provider organisations to control those appointments which can be booked by external organisations
  - ensuring that consumer organisations obtain only available appointments which are appropriate to them
  - providing a more standardised categorisation of available appointment slots across provider systems so that inappropriate appointment booking is reduced
  - providing where applicable the GP branch surgery location of available appointment slots

{% include note.html content="The requirements below only apply for slot availability management so should only apply to the '`Search for free slots`' GP Connect API use case and none of the other GP Connect API use cases such as '`Retrieve a patient's appointments`' or '`Amend an appointment`', for these the returned resources should reflect the complete organization appointment book." %}
  
## Appointment availability control ##

Provider systems SHALL:
- enable provider system end-users to designate the slots within their appointment books as 'GP Connect bookable'. This is a broad control to make slots in the appointment book available for booking through the GP Connect API
- enable provider system end-users to additionally specify which schedules/slots can be booked by an individual organisation and/or group of organisations, and/or booking organisation type as well as enabling end-users to limit the number of slots which can be booked by this 'organisation access profile'

The provider system end-user SHALL be presented with an 'Organisation Type' list which reflects the NHS Digital [FHIR Organisation Type](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-OrganisationType-1) value set.

The consumer system SHOULD send their booking Organisation Type and booking organization ODS Code in the 'SearchFilter' parameter, as specified in the [Search for free slots](appointments_use_case_search_for_free_slots.html) page, which the provider system will then use to determine the matching availability.

If the consumer system does not send any 'SearchFilter' parameters then the provider system will only return slots that are not restricted for booking to an individual organisation, a group of organisations, or by organisation type.

The following table describes the matching rules for a provider system when applying the search filter passed by a consumer to the [Search for free slots](appointments_use_case_search_for_free_slots.html) call:

<table>
  <thead>
    <tr>
      <th>Search filter sent by consumer</th>
      <th>Slots are returned that:</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>(no search filter)</td>
      <td>
      	&bull; Are marked as GP Connect bookable<br/>
      	&bull; AND have no organisation type restriction set<br/>
      	&bull; AND have no organisation/organisation group restriction set
      </td>
    </tr>
    <tr>
      <td>
      	searchFilter<br/>
       	&nbsp; with organisation type set
      </td>
      <td>
      	&bull; Are marked as GP Connect bookable<br/>
      	&bull; AND have no organisation/organisation group restriction set<br/>
      	&bull; AND [<br/>
		&nbsp; &nbsp; &bull; have no organisation type restriction set<br/>
		&nbsp; &nbsp; &bull; OR have an organisation type restriction matching that passed in the searchFilter ]
      </td>
    </tr>
    <tr>
      <td>
      	searchFilter<br/>
       	&nbsp; with organisation code set
      </td>
      <td>
      	&bull; Are marked as GP Connect bookable<br/>
      	&bull; AND have no organisation type restriction set<br/>
      	&bull; AND [<br/>
		&nbsp; &nbsp; &bull; have no organisation code/group restriction set<br/>
		&nbsp; &nbsp; &bull; OR have an organisation code/group restriction matching that passed in the searchFilter ]
      </td>
    </tr>
    <tr>
      <td>
      	searchFilter<br/>
       	&nbsp; with organisation type set<br/>
       	&nbsp; and organisation code set
      </td>
      <td>
      	&bull; Are marked as GP Connect bookable<br/>
      	&bull; AND [<br/>
		&nbsp; &nbsp; &bull; have no organisation type restriction set<br/>
		&nbsp; &nbsp; &bull; OR have an organisation type restriction matching that passed in the searchFilter ]<br/>
      	&bull; AND [<br/>
		&nbsp; &nbsp; &bull; have no organisation code/group restriction set<br/>
		&nbsp; &nbsp; &bull; OR have an organisation code/group restriction matching that passed in the searchFilter ]
      </td>
    </tr>
  </tbody>
</table>

## Booking window/embargo ##

It is recommended that provider systems also provide the functionality to enable the provider system end-user to control how far in advance external organisations should be allowed to book slots and how near to the actual slot time - that is, via 'Booking Window' or 'Embargo' rules.

Where such rules have been set, provider systems SHALL only return slots which respect these rules.

## Appointment slot categorisation ##

Providers systems SHALL enable and require the mandatory selection by provider system end-users of a 'Practitioner Role' and 'Delivery Channel' for schedules/slots as part of the end-user GP Connect appointment configuration.

- The 'Practitioner Role' list SHALL reflect the GP Connect value subset of NHS Digital [Practitioner Role](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-PractitionerRole-1) .
- The 'Delivery Channel' list SHALL reflect the GP Connect value set of [Delivery Channel](https://fhir.nhs.uk/STU3/ValueSet/GPConnect-DeliveryChannel-1).
- Provider systems SHALL maintain alignment with the value sets.
- These values SHALL NOT be configurable/modifiable by end-users.


## Branch surgery location ##

The Schedule resource has a mandatory 'Location' reference within the actor element. The referenced location SHALL be populated by provider systems with the name and address of the location where the appointment will take place. This will either be the GP practice where there are no branch surgeries OR the branch surgery (including ODS site code where available).
