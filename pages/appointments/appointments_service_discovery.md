---
title: Appointment Management service discovery
keywords: appointments design
tags: [design,appointments]
sidebar: appointments_sidebar
permalink: appointments_service_discovery.html
summary: "Determining which GP practices to book into"
---

## Determining which GP practice to book into ##

### Patient's registered practice ###

The "default" GP connect flow (as used in other capabilities) is shown in the diagram below, and includes the retrieval of the **ODS organisation code of the patient's registered practice** from PDS in step 1 (<span style="color: yellow; background-color: silver;">in yellow</span>).  For more details on this flow please see [Spine integration illustrated](integration_illustrated.html).

<img src="images/integration/gpconnect-appts-flow.png" alt="Diagram showing the high level three step flow for making GP Connect calls" style="width: 60%;">

This flow is suitable for Appointment Management consumers that wish to book into the patient's registered practice, but where an appointment is required at a different practice, an alternate mechanism for determining the practice and their ODS organisation code is needed.

{% include important.html content="For a GP practice with multiple surgeries (locations), the ODS organisation code returned from PDS represents the GP practice organisation as a whole.  In order to determine the patient's preferred branch surgery please see [Branch surgeries](development_branch_surgeries.html) for more information." %}

### Booking into other practices or hubs ###

Where a GP Connect Appointment Management consumer wishes to book into a GP practice or hub that is not the patient's registered practice, a different mechanism is required to discover the practice or hub and their ODS organisation code.

{% include note.html content="In sub-sections below, the word *practice* is used to mean *practice or hub* in the context of booking into other practices or hubs, to prevent frequent repetition." %}

#### Consumer system configuration ####

Appointment consumer systems that are predominantly used to book into GP practices within the local area (such as within a local federation or PCN) may use local system configuration to determine the practice to book into, and their ODS organisation code.

For example a pre-configured pick list of organisations on the booking screen of the consumer screen allowing a user to choose which practice to book into.  The pick list may be configured by the consumer organisation or by the consumer system supplier in conjunction with the consumer organisation.

#### Directory of Services (DOS) - currently for UEC consumers only ####

Appointment consumer systems that are used to book into practices in a wider context where local knowledge of service availability cannot be relied on (such as 111 call centres that receive calls from across England) will need an enhanced mechanism for determining an appropriate practice to book the patient into, based on criteria such as:

- opening hours
- distance from patient
- service provision
- service availability to patient

The [Directory of Services](https://developer.nhs.uk/apis/uec-appointments/dos_overview.html) (DOS) is a service discovery and information tool for this purpose, and is currently being configured (June 2019) with GP Connect bookable services.

When booking into other practices, DOS replaces the function of PDS in determining where to book into.  However the PDS step is still required in order to verify the patient's NHS number, and as part of the logic to determine the ODS organisation code of practice (see [below](appointments_service_discovery.html#determining-the-ods-code-to-use-for-gp-connect-from-dos)).

<img src="images/integration/gpconnect-appts-dos-flow.png" alt="Diagram showing the high level four step flow for making GP Connect calls when using Directory of Services" style="width: 60%;">

##### Determining the ODS code to use for GP Connect from DOS #####

Once a consumer system user has selected a service from the list returned by the DOS search, the system needs to determine the ODS code to use to look up the practice's GP Connect endpoint in SDS. The logic to do so is described below:

1. Check the `serviceEndpoints` element of the chosen service in the DOS search response:

	a. If there is a FHIR Scheduling endpoint present where the address field is prefixed with `ODS:`, e.g. `ODS:A10001`, then this is the ODS code to use to look up the GP Connect endpoint in SDS.

	b. If there is no FHIR scheduling endpoint with an `ODS:` prefix, go to step 2.

2. Compare the chosen DOS service's ODS code (in the `odsCode` element) to the patient's registered practice ODS code obtained from the PDS. This will determine if the returned service is their registered practice.

	a. If there is a match, then use this ODS code to lookup the GP Connect endpoint in SDS.

	b. If there is no match then booking via GP Connect is not possible for this service.

This logic is described in the context of a full [GP Connect workflow example](https://developer.nhs.uk/apis/uec-appointments/dos_endpoints_booking.html) in the Urgent and Emergency Care Appointment Booking specification.

##### DOS service filtering #####

Consumer systems that have used the DOS to determine a practice to book at must send the DOS service ID as part of the [Search for free slots](appointments_use_case_search_for_free_slots.html#search-parameters) call.

This is to allow the practice to return slots only for the selected service, as they may be running multiple services.

Please read the [Service filtering introduction](appointments_service_filtering.html) for more information.

##### Further information on DOS integration #####

Please see the following pages from the Urgent and Emergency Care Appointment Booking specification for further information on integrating GP Connect Appointment UEC consumer systems with Directory of Services: 

- [DOS overview](https://developer.nhs.uk/apis/uec-appointments/dos_overview.html)
- [GP Connect workflow overview](https://developer.nhs.uk/apis/uec-appointments/gpc_wfoverview.html)
- [GP Connect workflow example](https://developer.nhs.uk/apis/uec-appointments/gpc_wfexample.html)
