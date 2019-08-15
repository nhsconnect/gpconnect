---
title: Design decisions
keywords: foundations design
tags: [design,foundations]
sidebar: foundations_sidebar
permalink: foundations_design.html
summary: "Overview of the design decisions made in relation to the Foundations capability pack"
---

## Business identifiers ##

The following business identifier types are to be supported by GP Connect systems:

| Identifier | Resource | System |
| ---------- | -------- | ------ |
| NHS Number | Patient | `https://fhir.nhs.uk/Id/nhs-number` |
| ODS Code | Organisation | `https://fhir.nhs.uk/Id/ods-organization-code` |
| ODS Site Code | Location | `https://fhir.nhs.uk/Id/ods-site-code` |
| SDS User ID | Practitioner | `https://fhir.nhs.uk/Id/sds-user-id` |

{% include important.html content="Support for additional identifier types in line with the existing GPSoC requirements is also under consideration." %}


## Definition of Organisation and Location entities ##

The GP practice organisation is a legal entity which is represented by the FHIR `Organization` resource. This entity will have an assigned [ODS code](https://digital.nhs.uk/organisation-data-service). 

The practice organisation will have one or more operating locations (also known as 'sites' or 'branches') which, together, perform the patient healthcare for which the organisation is legally responsible. Each operating location is represented by a FHIR `Location` resource. 

Where ODS site codes are defined in Spine configuration, these map to GP practice operating locations, and hence to location FHIR resources.

The above definition of the organization and location are particularly relevant to two elements within the `Patient` resource and the `location participant` within the `Appointment` resource.

### Organization and location in the patient resource ###

The [Patient](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) resource contains the `managingOrganization` element which should reference an organization resource representing the legal entity which is responsible for the patient's record.

The [Patient](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1) resource also contains the `preferredBranchSurgery` element within the [Registration Details](https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-RegistrationDetails-1) extension. This preferred branch surgery should contain a reference to a location resource representing the patient's preferred operating location which may be a branch surgery or the organization's main surgery.

### Location in the appointment resource ###

When [booking an appointment](appointments_use_case_book_an_appointment.html) it must contain one participant element which references a location resource. This location resource should represent the physical location where the appointment is to take place. This location resource may be a representation of a branch surgery, the main surgery, a room within a surgery or another location.

When booking an appointment using the GP Connect API, the [search for free slots](appointments_use_case_search_for_free_slots.html) interaction needs to be performed to get back free slots in which the appointment can be booked. The slots are linked to a schedule which is linked to a location. If the patient's preferred branch surgery is known it could be used to filter the free slots based on the location within the schedule to which they are linked.

