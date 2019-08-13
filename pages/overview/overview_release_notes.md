---
title: GP Connect Overview Release Notes
keywords: GP Connect Overview, release notes
tags: [release]
sidebar: overview_sidebar
permalink: overview_release_notes.html
summary: "Release notes for the various versions of the GP Connect overview"
---

#### GP Connect 1.0.0-alpha.5 (Released: 20 July 2017)

- updated [Common API Guidance](development_fhir_api_guidance.html)
	- clarification on API Versioning and FHIR Server Root URL formats
	- more detail of the principles of resource identity
	- removed references to superseded RFC 2616, replacing with the updated references
- updated [Personal Demographics Service](integration_personal_demographic_service.html)
	- note regarding the use of PDS Trace Sequence Number to enable efficient caching
- updated [Spine Security Policy Implementation Guide](integration_spine_security_proxy_implementation_guide.html)
	- requirement that FHIR Root Server URL **SHALL** contain practice level identifier
	- addition of HTTP Status Code 599 error which can in some circumstances be returned from the Spine Security Proxy
- updated [Security Guidance](development_api_security_guidance.html)
	- clarification of provider responsibilities for HTTP header validation
- updated [Cross Organisation Audit and Provenance](/integration_cross_organisation_audit_and_provenance.html)
	- clarification of the usage of JWT token for consumers and providers
- updated [Error Handling Guidance](development_fhir_error_handling_guidance.html)
	- addition of 501 HTTP Status code to guidance
- updated [Clinical Terminologies](design_clinical_terminologies.html)
	- clearer statement on case sensitivity of terminologies in FHIR

	




