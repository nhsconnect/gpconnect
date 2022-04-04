---
title: Non-functional requirements
keywords: development non-functional requirements NFRs
tags: [development]
sidebar: overview_sidebar
permalink: development_api_non_functional_requirements.html
summary: "Details of non-functional requirements (NFRs) that describe system attributes such as security, reliability, maintainability, scalability, and usability (often referred to as the “ilities”)"
---

## Non-functional requirements ##

### Security ###

Provider systems **SHALL** resist unauthorised, accidental or unintended usage and provide access only to legitimate users.

Please refer to the [Security guidance](development_api_security_guidance.html) page for technical details.

### Volume and performance ###

#### Volumetric ####

Provider systems **MUST** meet the agreed volumetric performance targets. 

Please refer to the [Volumetric guidance](development_api_volume_and_performance.html#volumetrics) page for technical details.

#### Performance ####

Provider systems **MUST** meet the agreed response time performance targets.

Please refer to the [Performance guidance](development_api_volume_and_performance.html#performance) page for technical details.

### Capacity ###

Provider systems **MUST** meet the agreed capacity requirements.

### Scalability ###

Provider systems **SHALL** be designed to accommodate increased volumes, workloads and users.

### Availability ###

Provider systems **SHALL** meet the agreed availability targets (service time and/or hours and planned downtime) as defined in the operational level agreement (OLA).

### Recoverability ###

Provider systems **SHALL** meet the agreed recoverability targets as documented in the Operational Level Agreement (OLA).

### Audit and provenance ###

Provider systems **SHALL** audit all API access and actions.

Please refer to the [cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html) page for technical details.

Provider systems **SHALL** record audit and provenance data in line with existing GPSoC framework agreements, including relevant IM1 requirements for interfacing mechanisms.

### Maintainability ###

Provider systems **SHALL** be designed to optimise the ability of maintenance personnel to revise or enhance it.

### Serviceability ###

Provider systems **SHALL** be designed so that technical support personnel are able to monitor and manage it in operation.

### Data retention ###

Provider systems **SHALL** retain data in line with existing GPSoC framework agreements.

### Usability ###

Provider and consumer systems **SHOULD** follow the [ISO 13407](https://www.iso.org/standard/21197.html) / [ISO 9241-210](https://www.iso.org/standard/52075.html) to explain a user-centred design process.

Please refer to the 'GPSoC Technical Standards' for details.

### Accessibility ###

Provider and consumer systems **MUST** maintain a compliance of minimum Double “A” of the WCAG 1.0 (or equivalent in WCAG 2.0) or, as stipulated by UK Government guidelines, for all user interfaces. Please see the [Web Accessibility Initiative](https://www.w3.org/WAI/) for more details.

Please refer to the 'GPSoC Technical Standards' for details.

### Deployment ###

Provider systems **SHALL** release a new major version of their GP Connect API alongside a previous major version, until such time as consumers have migrated to the new major version.

Provider systems **SHOULD** release a new minor or patch version, replacing the previous the previous minor or patch version.

### Enablement ###

Provider systems **SHALL** provide a mechanism for a data controller at a practice to choose to globally disable/enable the GP Connect provider APIs (that is, turn on/off the overall GP Connect technical capability at the practice), and this **SHALL** be deployed as disabled by default.

In addition, provider systems **SHALL** allow each assured GP Connect capability to be disabled/enabled independently of each other (Access Record HTML / Appointment Management / Access Record Structured / Access Document), and each capability **SHALL** be deployed as disabled by default.

Provider systems **SHALL** audit when GP Connect is globally enabled or disabled, or a GP Connect capability is enabled or disabled; in line with the [audit and provenance](#audit-and-provenance) requirements above.
