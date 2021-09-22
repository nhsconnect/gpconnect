---
title: Provider system configuration for service filtering
keywords: appointments design
tags: [design,appointments]
sidebar: appointments_sidebar
permalink: appointments_serviceid_configuration.html
summary: "Configuration to support the rollout of the service filtering feature"
---
<br/>

Service filtering in a provider system **SHALL** be controlled by two levels of configuration:

1. a supplier-controlled configuration enablement switch ("supplier switch")
2. organisation-controlled configuration ("organisation configuration"), incorporating an organisation enablement switch ("organisation switch")

The supplier switch allows the service filtering configuration to be made visible to selected (or all) organisations using the supplier's provider system.

Once the service configuration screens are made available to an organisation, a user at the organisation can configure service filtering, and once configuration is completed, switch service filtering on so that the configuration takes effect upon the API, for their organisation.

## Supplier switch ##

The visibility of the service filtering configuration in a provider system **SHALL** be controlled by a global supplier system switch, with three states:

1. OFF
2. ON AT SELECTED ORGANISATIONS - this state requires an associated selected organisation list
3. ON

{% include note.html content="The supplier switch allows service filtering configuration to be made available to provider organisations in a controlled manner, and not before Directory of Services changes have been made to support them." %}

The supplier switch, and associated selected organisation list **SHALL**:

- control service filtering functionality as described in the sub-sections below
- only be controlled by appropriate staff at the supplier
- be changed and applied quickly to the supplier's system without requiring a code change or software release
- be initially defaulted to OFF, and empty
- be audited, capturing:
	- date/time of change
	- supplier staff member responsible for the change
	- current and previous state of the switch
	- changes to the selected organisation list (if any)

{% include important.html content="The configuration visibility switch does not affect service filtering changes in an appointments consumer in the same supplier system, such as displaying service name when searching for free slots." %}

### Supplier switch set to OFF ###

When the service filtering supplier switch is set to OFF:

- For ALL organisations in the supplier's system:
	- the organisation-controlled service configuration **SHALL NOT** be visible to users, and **SHALL NOT** take effect upon the API (regardless of the value of the organisation switch)

### Supplier switch set to ON AT SELECTED ORGANISATIONS ###

When the service filtering supplier switch is set to ON AT SELECTED ORGANISATIONS:

- For organisations in the selected organisation list that are eligible to use GP Connect:
  - the organisation configuration **SHALL** be visible
  - the effect of service filtering upon the API **SHALL** be dependent on the organisation configuration
- For organisations NOT held in the selected organisation list:
	- the organisation configuration **SHALL NOT** be visible, and **SHALL NOT** take effect upon the API (regardless of the value of the organisation switch)

### Supplier switch set to ON ###

When the service filtering supplier switch is set to ON:

- For ALL organisations in the supplier's system that are eligible to use GP Connect:
	- the organisation configuration **SHALL** be visible
	- the effect of service filtering upon the API **SHALL** be dependent on the organisation configuration

{% include note.html content="This state has been included so that when service filtering configuration can be made available to all organisations using the supplier's system, there is no need to continue to maintain the selected organisation list." %}


## Organisation configuration ##

The organisation configuration for service filtering **SHALL** be used by staff within a provider organisation to:

- set up a list of services for their organisation (taken from the service(s) in DOS provided by the organisation)
- assign services to schedules (or schedule "templates")
- enable or disable service filtering for their organisation

{% include important.html content="See [supplier switch](#supplier-switch) above for conditions when the organisation configuration is visible to a provider organisation." %}

### Service list ###

The organisation configuration **SHALL** include a list of services for a user to set up, that their organisation provides.

A service in the list **SHALL** at a minimum be comprised of:

- service ID
- service name
- service type

The user at the organisation **SHALL** be able to:

- view the list
- add, delete and change the services in the list

{% include note.html content="The correct list of services for a provider organisation to configure will be determined with assistance from the DOS leads" %}

The screenshot below shows an example service in Directory of Service (DOS) showing the service ID, name and type fields.

<img src="images/appointments/dos-screenshot.png" style="width: 500px; padding-bottom: 10px;" />

Changes to the list **SHALL** be audited, capturing:
- date/time of change
- user responsible for the change
- current and previous values

The list of services **SHALL** be maintained irrespective of the value of the organisation switch, so they can be set up prior to the local switch being ON.

If there is already a list of DOS service IDs in the provider system provided by the current organisation, this **SHOULD** be used rather than creating a new list of service IDs.

#### Service list validation ####

Provider systems **MAY** make use of the [Search by Service ID](https://developer.nhs.uk/apis/dos-api/byServiceId.html) endpoint in the DOS API to:
- validate that any service ID entered by the user appears on the DOS and is therefore a valid service
- pull back the service name and type which corresponds with the service ID and display it on the screen

The *Service by ODS Code* endpoint in the DOS API **MUST NOT** be used as this will not return a complete list of DOS services provided by an organisation.  Furthermore it is important that when entering the service list, the user is assisted by their DOS lead, to ensure the DOS correctly represents the services offered by their organisation.

### Linking services to schedules ###

The organisation configuration **SHALL** include the ability for a user to link services to schedules, so that service filtering can return free slots for a service.

{% include important.html content="The term schedule (in line with FHIR nomenclature) is used to indicate a grouping of slots, however in provider systems these are typically called sessions or rotas, and in fact the linking may occur to session or rota templates, rather than to instances of sessions/rotas." %}

Provider suppliers **SHOULD** determine the best way for users to link services and schedules within their system.

Linking between services and schedules **MAY** occur in different ways, depending on the appointment configuration workflow of the provider system, for example:

- Services may be assigned to schedules (or their "templates") on the schedule or schedule "template" screen when they are created
- Schedule "templates" (or "template types") may be assigned to services on the service list

Linking between services and schedules **SHALL** be possible irrespective of the value of the organisation switch, so a user can create links prior to the organisation switch being ON.

Linking between services and schedules (or their "templates") **SHALL** be audited, capturing:
- date/time of change
- user responsible for the change
- current and previous link state

#### Optionality ####

Linking between services and schedules or schedule templates **SHALL** be mandatory for a user to perform where:

- the [organisation switch](#organisation-switch) is set to ON
- and a schedule or schedule template or slot within a schedule is marked as [GP Connect bookable](appointments_slotavailabilitymanagement.html#appointment-availability-control)

When linking a service to a schedule (or schedule template), the list **SHALL** be driven from the [service list](#service-list) in the organisation configuration, and in addition **SHALL** include a 'Not applicable' option.

In all other circumstances, linking between services and schedules or schedule templates **SHALL NOT** be mandatory for a user to perform.

#### GP Connect bookable prompt ####

If a slot is amended to become 'GP Connect bookable' and the [organisation switch](#organisation-switch) is set to ON, and the slot's schedule is not linked to a service, the user **SHALL** be prompted and required to select a service from the service list (or a 'Not applicable' option) to link to the slot's schedule.

If a schedule is amended to become 'GP Connect bookable' and the [organisation switch](#organisation-switch) is set to ON, and the schedule is not linked to a service, the user **SHALL** be prompted and required to select a service from the service list (or a 'Not applicable' option) to link to the schedule.

### Organisation switch ###

The organisation configuration **SHALL** include a service filtering enablement switch that allows a user at a provider organisation to enable or disable service filtering for their organisation.

The organisation switch **SHALL**:

- control service filtering enablement for the current organisation
- only be controlled by appropriate staff logged on at the provider organisation
- allow two states (ON and OFF), and be initially defaulted to OFF
- take effect immediately
- be audited, capturing:
	- date/time of change
	- user responsible for the change
	- current and previous state of the switch

{% include note.html content="The purpose of the organisation switch is so that organisations can set up their list of service IDs and link them to sessions/rotas, before they enable service filtering.  If the feature was deployed in the enabled state without the list of service IDs set up, no slots would be returned to consumers that requested free slots for a specific service.
<br/>In addition, some organisations may not wish to or need to use service filtering, such as those with a single DOS service. " %}

{% include important.html content="Please note if the [supplier switch](#supplier-switch) is set to OFF, or set to ON AT SELECTED ORGANISATIONS and the current organisation is not in the selected organisation list, the organisation configuration including the organisation switch **SHALL NOT** be visible, and **SHALL NOT** take effect upon the API, regardless of the value of the organisation switch." %}

#### Organisation switch set to OFF ####

When the organisation switch is set to OFF:

- service filtering in the API **SHALL NOT** take effect
	- `schedule.actor:healthcareservice` parameter on [Search for free slots](appointments_use_case_search_for_free_slots.html#search-parameters) **SHALL** be ignored
  - ...

{% include todo.html content="List areas to disable" %}

#### Organisation switch set to ON ####

When the organisation switch is set to ON:

- service filtering in the API **SHALL** take effect
  - ...
  
{% include todo.html content="List areas to enable" %}

#### Changing the organisation switch ####

When a user attempts to change the organisation switch from OFF to ON the user **SHALL**:

- be prevented from doing so if:
  - [GP Connect, or GP Connect Appointment Management are disabled](development_api_non_functional_requirements.html#enablement) at the organisation
  - the service list is empty.  The user **SHALL** be prompted to set up their service list
- be prompted to confirm their decision when the service list is not empty using the text below:

> Have you completed the list of your services and linked them to sessions/rotas? Please refer to the guidance at **TBC** for more information
