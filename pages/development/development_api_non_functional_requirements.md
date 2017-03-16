---
title: Non-Functional Requirements
keywords: development non-functional requirements NFRs
tags: [development]
sidebar: overview_sidebar
permalink: development_api_non_functional_requirements.html
summary: "Details of NFRs that describe system attributes such as security, reliability, maintainability, scalability, and usability (often referred to as the “ilities”)."
---

## Non-Functional Requirements ##

### Security ###

Provider systems SHALL resist unauthorised, accidental or unintended usage and provide access only to legitimate users.

Please refer to the [Security Guidance](development_api_security_guidance.html) page for technical details.

### Volume & Performance ###

#### Volumetric ####

Provider systems MUST meet the agreed volumetric performance targets.

Please refer to the [Volumetric Guidance](development_api_volume_and_performance.html#volumetrics) page for technical details.

#### Performance ####

Provider systems MUST meet the agreed response time performance targets.

Please refer to the [Performance Guidance](development_api_volume_and_performance.html#performance) page for technical details.

### Capacity ###

Provider systems MUST meet the agreed capacity requirements.

### Scalability ###

Provider systems SHALL be designed to accomodate increased volumes, workloads and users.

### Availability ###

Provider systems SHALL meet the agreed availability targets (service time and/or hours and planned downtime) as defined in the Operational Level Agreement (OLA).

### Recoverability ###

Provider systems SHALL meet the agreed recoverability targets as documented in the Operational Level Agreement (OLA).

### Audit & Provenance ###

Provider systems SHALL audit all API access and actions.

Please refer to the [Cross Organisation Audit & Provenance](integration_cross_organisation_audit_and_provenance.html) page for technical details.

Provider systems SHALL record audit & provenance data inline with existing GPSoC framework agreements, including relevant IM1 requirements for interfacing mechanisms.

### Maintainability ###

Provider systesms SHALL be designed to optimise the ability of maintenance personnel to revise or enhance it.

### Serviceability ###

Provider systems SHALL be designed so that technical support personnel are able to monitor and manage it in operation.

### Data Retention ###

Provider systems SHALL retain data inline with existing GPSoC framework agreements.

### Usability ###

Provider and Consumer systems SHOULD follow the [ISO 13407](https://www.iso.org/standard/21197.html) / [ISO 9241-210](https://www.iso.org/standard/52075.html) to explain a user centred design process.

Please refer to the 'GPSoC Technical Standards' for details.

### Accessability ###

Provider and Consumer systems MUST maintain a compliance of minimum Double “A” of the WCAG 1.0 (or equivalent in WCAG 2.0), or as stipulated by UK Government Guidelines, for all user interfaces. Please see the [Web Accessibility Initiative](https://www.w3.org/WAI/) for more details.

Please refer to the 'GPSoC Technical Standards' for details.

### Deployment ###

Provider systems SHALL be deployed with the provider APIs enabled by default.

Provider systems MAY provide a mechanism for a data controller at an organisation to choose to globally disable/enable the provider APIs (i.e. turn on/off the overall GP Connect technical capability).

Provider systems MAY allow each assured capability to be globally disabled/enabled independently of each other (i.e. Access Record HTML vs. Appointments vs. Tasks).

## External Documents / Policy Documents ##

| Name | Author | Version | Updated |
| GPSoC Technical Standards | NHS Digital | v1.0 | ??/??/???? |
| GPSoC Non Functional Requirements | NHS Digital | v1.0 | ??/??/???? |
