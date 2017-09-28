---
title: GP Connect Overview Release Notes
keywords: GP Connect Overview, release notes
tags: [release]
sidebar: overview_sidebar
permalink: overview_release_notes.html
summary: "Release notes for the various versions of the GP Connect overview."
---

#### GP Connect 1.0.0-beta.1

- [Specification Versioning Guidance](development_fhir_versioning_specification_guidance.html), [FHIR Capability Versioning Guidance](development_fhir_versioning_capability_guidance.html), [Provider API Versioning Guidance](development_fhir_versioning_provider_guidance.html), [Consumer Versioning Guidance](development_fhir_versioning_consumer_guidance.html) - Added additional information around versioning.
- [Security Guidance](development_api_security_guidance.html) - Updated Security guidance around the protocols suppliers should implement.
- [Cross Organisation Audit & Provenance](integration_cross_organisation_audit_and_provenance.html) - Updated JWT spcification examples to use the new profile and valuesets.
- [Operation Guidance](development_fhir_operation_guidance.html#foundations-capability-interactions) - Corrected "Example URL Pattern" for searches to have correct format of [System]|[Code].
- [Error Handling Guidance](development_fhir_error_handling_guidance.html) - Updated page to reflect move from "gpconnect-error-or-warning-code-1" to "spine-error-or-warning-code-1"


#### GP Connect 1.0.0-alpha.5 (Released: 17 July 2017)

- Updated [Common API Guidance](development_fhir_api_guidance.html)
	- Clarification on API Versioning and FHIR Server Root URL formats.
	- More detail of the principles of resource identity.
	- Removed references to superceded RFC 2616, replacing with the updated references.
- Updated [Personal Demographics Service](integration_personal_demographic_service.html)
	- Note regarding the use of PDS Trace Sequence Number to enable efficient caching.
- Updated [Spine Security Policy Implementation Guide](integration_spine_security_proxy_implementation_guide.html)
	- Requirement that FHIR Root Server URL SHALL contain practice level identifier.
	- Addition of HTTP Status Code 599 error which can in some circumstances be returned from the Spine Security Proxy.
- Updated [Security Guidance](development_api_security_guidance.html)
	- Clarification of provider responsibilities for HTTP header validation.
- Updated [Cross Organisation Audit and Provenance](/integration_cross_organisation_audit &amp; provenance.html)
	- Clarification of the usage of JWT token for consumers and providers.
- Updated [Error Handling Guidance](development_fhir_error_handling_guidance.html)
	- Addition of 501 HTTP Status code to guidance
- Updated [Clinical Terminologies](design_clinical_terminologies.html)
	- Clearer statement on case sensitivity of terminologies in FHIR
