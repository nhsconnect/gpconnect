---
title: Provider system configuration for service ID filtering
keywords: appointments design
tags: [design,appointments]
sidebar: appointments_sidebar
permalink: appointments_serviceid_configuration.html
summary: "Configuration to support the rollout of the service ID filtering feature"
---
<br/>

Service ID filtering in a provider system **SHALL** be controlled by two levels of configuration:

1. a supplier-controlled configuration availability switch ("supplier switch")
2. organisation-controlled configuration, incorporating an enablement switch ("organisation configuration")

The supplier switch allows the service ID filtering configuration to be made available to selected (or all) organisations using the supplier's provider system.

Once the service ID configuration screens are made available to an organisation, a user at the organisation can configure service ID filtering, and once configuration is completed, enable service ID filtering on so that the configuration takes effect upon the API, for their organisation.

## Supplier switch ##

The availability of the service ID filtering configuration in a provider system **SHALL** be controlled by a global supplier system switch, with three states:

1. OFF
2. ON AT SELECTED ORGANISATIONS - this state requires an associated selected organisation list
3. ON

{% include note.html content="The supplier switch allows service ID filtering configuration to be made available to provider organisations in a controlled manner, and not before Directory of Services changes have been made to support them." %}

The supplier switch, and associated selected organisation list **SHALL**:

- control service ID filtering functionality as described in the sub-sections below
- only be controlled by appropriate staff at the supplier
- be changed and applied quickly to the supplier's system without requiring a code change or software release
- be initially defaulted to OFF, and empty
- be audited, capturing:
	- date/time of change
	- supplier staff member responsible for the change
	- current and previous state of the switch
	- changes to the selected organisation list (if any)

{% include important.html content="The configuration availability switch does not affect service ID filtering changes in an appointments consumer system in the same supplier system, such as displaying service name when searching for free slots." %}

### Supplier switch set to OFF ###

When the service ID supplier switch is set to OFF:

- For ALL organisations in the supplier's system:
	- the organisation-controlled service ID configuration screen(s) **SHALL NOT** be visible to users, or take effect upon the API

### Supplier switch set to ON AT SELECTED ORGANISATIONS ###

When the service ID supplier switch is set to ON AT SELECTED ORGANISATIONS:

- For organisations in the selected organisation list that are eligible to use GP Connect:
  - the organisation configuration **SHALL** be visible
  - the effect of service ID filtering upon the API **SHALL** be dependent on the organisation configuration
- For organisations NOT held in the selected organisation list:
	- the organisation configuration **SHALL NOT** be visible, or take effect upon the API

### Supplier switch set to ON ###

When the service ID supplier switch is set to ON:

- For ALL organisations in the supplier's system that are eligible to use GP Connect:
	- the organisation configuration **SHALL** be visible
	- the effect of service ID filtering upon the API **SHALL** be dependent on the organisation configuration

{% include note.html content="This state has been included so that when service ID filtering configuration can be made available to all organisations using the supplier's system, there is no need to continue to maintain the selected organisation list." %}


## Organisation configuration ##

The organisation configuration for service ID filtering **SHALL** used by staff within a provider organisation to:

- set up a list of services for their organisation (taken from the service(s) in DOS provided by the organisation)
- assign services to appointment sessions/rotas or session/rota templates
- enable or disable service ID filtering for their organisation

{% include important.html content="See [supplier switch](#supplier-switch) above for conditions when the organisation configuration is available to a provider organisation." %}

### Service list ###

The organisation configuration **SHALL** include a list of services for a user to configure, and be used to perform service ID filtering.

A service in the list **SHALL** at a minimum be comprised of:

- service ID
- service name

The user at the organisation **SHALL** be able to:

- view the list
- add, delete and change the services in the list

{% include note.html content="The correct service IDs and names to use will be determined with assistance from the DOS leads" %}

The screenshot below shows an example service in Directory of Service (DOS) showing the service ID and name fields.

<img src="images/appointments/dos-screenshot.png" style="width: 500px; padding-bottom: 10px;" />

Changes to the list **SHALL** be audited, capturing:
- date/time of change
- user responsible for the change
- current and previous values

The list of services **SHALL** be maintained irrespective of the value of the enablement switch, so they can be set up prior to the local switch being ON.

Provider systems **MAY** make use of the DOS API to:
- validate that any service id code entered by the user appears on the DOS in is therefore a valid service
- pull back the service name which corresponds with the service id and display it on the screen

{% include todo.html content="Provide DOS API details" %}


### Session/rota-service linking ###

{% include todo.html content="TODO" %}




### Enablement switch ###

The service ID filtering enablement switch controls the enablement of the service ID filtering feature at a provider organisation.  It allows a user at a provider organisation to enable or disable service ID filtering for their organisation, after they have set up their list of service IDs.

The organisation enablement switch **SHALL**:

- control service ID filtering enablement for the current organisation
- only be controlled by appropriate staff logged on at the provider organisation
- allow two states (ON and OFF), and be initially defaulted to OFF
- take effect immediately
- be audited, capturing:
	- date/time of change
	- user responsible for the change
	- current and previous state of the switch

{% include note.html content="The purpose of the enablement switch is so that organisations can set up their list of service IDs before slots are filtered by service ID.  If the feature was deployed in the enabled state without the list of service IDs set up, no slots would be returned to consumers that requested free slots for a specific service.
<br/>In addition, some organisations may not wish to or need to use service ID filtering, such as those with a single DOS service. " %}


#### Enablement switch set to OFF ####

When the organisation's enablement switch is set to OFF:

- service ID filtering in the API **SHALL NOT** take effect
	- `schedule.actor:healthcareservice` parameter on [Search for free slots](appointments_use_case_search_for_free_slots.html#search-parameters) **SHALL** be ignored
  - **TBC**

#### Enablement switch set to ON ####

When the organisation's enablement switch is set to ON:

- service ID filtering in the API **SHALL** take effect
  - **TBC**

#### Changing the enablement switch ####

When a user attempts to change the enablement switch from OFF to ON the user **SHALL**:

- be prevented from doing so if:
  - [GP Connect, or GP Connect Appointment Management are disabled](development_api_non_functional_requirements.html#enablement) at the organisation
  - the service list is empty.  The user **SHALL** be prompted to set up their service list
- be prompted to confirm their decision when the service list is not empty using the text below:

> Have you completed the list of your services and linked them to sessions/rotas? Please refer to the guidance at **TBC** for more information
