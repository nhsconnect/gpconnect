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
2. organisation-controlled configuration, incorporating an enablement switch ("organisation configuration" and "enablement switch")

The supplier switch allows the service ID filtering configuration to be made available to selected (or all) organisations using the supplier's provider system.

Once the service ID configuration screens are made available to an organisation, a user at the organisation can configure service ID filtering, and once configuration is completed, enable service ID filtering on so that the configuration takes effect upon the API, for their organisation.

## Supplier switch ##

The availability of the service ID filtering configuration in a provider system **SHALL** be controlled by a global supplier system switch, with three states:

1. OFF
2. ON AT SELECTED ORGANISATIONS - this state requires an associated selected organisation list
3. ON

{% include note.html content="The supplier switch allows service ID filtering configuration to be made available to provider organisations in a controlled manner, and not before Directory of Services changes have been made to support them." %}

The supplier switch, and associated selected organisation list **SHALL**:

- control service ID functionality as described in the sub-sections below
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
  - the organisation-controlled service ID configuration screen(s) **SHALL** be visible
  - the effect of Service ID filtering upon the API **SHALL** be dependent on the organisation-controlled service ID configuration
- For organisations NOT held in the selected organisation list:
	- the organisation-controlled service ID configuration screen(s) **SHALL NOT** be visible, or take effect upon the API

### Supplier switch set to ON ###

When the service ID supplier switch is set to ON:

- For ALL organisations in the supplier's system that are eligible to use GP Connect:
	- the organisation-controlled service ID configuration UI **SHALL** be visible
	- the effect of Service ID filtering upon the API **SHALL** be dependent on the organisation-controlled service ID configuration

{% include note.html content="This state has been included so that when service ID filtering configuration can be made available to all organisations using the supplier's system, there is no need to continue to maintain the selected organisation list." %}

