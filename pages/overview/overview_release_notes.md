---
title: GP Connect Overview release notes
keywords: GP Connect Overview, release notes
tags: [release]
sidebar: overview_sidebar
permalink: overview_release_notes.html
summary: "Release notes for the GP Connect Overview"
---

#### [GP Connect 1.0.0-rc.1 (Released: 28/11/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_rc.3_Foundations_rc.4_GP_Connect_rc.1)

- [Security Guidance](development_api_security_guidance.html) - Updated Security guidance around the protocols suppliers should implement.
- [Cross Organisation Audit & Provenance](integration_cross_organisation_audit_and_provenance.html) - Updated JWT spcification examples to use the new profile and valuesets and included requirement for Patient Demographic cross-checking.
- [Operation Guidance](development_fhir_operation_guidance.html#foundations-capability-interactions) - Corrected "Example URL Pattern" for searches so that `System` and `Code` are in the correct order.
- [Error Handling Guidance](development_fhir_error_handling_guidance.html) - Updated page to reflect move from "gpconnect-error-or-warning-code-1" to "spine-error-or-warning-code-1"
- [Security Guidance](development_api_security_guidance.html) - Removed contradiction within specificaiton for Cache-Control headers
- [Common API Guidance](development_fhir_api_guidance.html#resource-metadata) - Uplifted guidance around the inclusion of profile details within the fhir resource meta data element when a consumer performs a create or amend interaction.
- [Common API Guidance](development_fhir_api_guidance.html#update-resource) - Added clarification on use of PUT to make clear an update should not create a resource if the resource being updated does not already exist.
- [Common API Guidance](development_fhir_api_guidance.html) - Added guidance on the behaviour of consumer and provider systems where Must-Support flag is present. 
- [Common API Guidance](development_fhir_api_guidance.html) - Split this page into "General API guidance" and "FHIR implementation guidance" pages.
- [Cross Organisation Audit & Provenance](integration_cross_organisation_audit_and_provenance.html#population-of-requested_record) - Added section to clarify the expected use of the `requested_record` claim within the JWT.
- [Information governance principles](designprinciples_ig_principles.html) - Updated teminology around the consumer responsibilities in regards to NHS Codes of Practice & Legal Obligations related to the use of GP Connect API;  additionally added reference to the ongoing review of the IG model, particularly in the light of GDPR;  additionally added more Access Record capability link to Patient Dissent to Share, and indicated that this was not applicable to Appointment Management Capability
- [Fhir library guidance](development_fhir_open_source_guidance.html) - the Fhir library guidance page has been updated to improve GP Connect guidance around using existing fhir libraries to aid it development.
- [Error handling guidance](development_fhir_error_handling_guidance.html) - Updated error handling guidance to include expectations around a resource not found, provide details of spine error codes expected and also restructured to clarify differing error condition types. 
- [FHIR API guidance](development_fhir_api_guidance.html) - Corrected in scope search prefixes to be consistent with other pages
- [Cross Organisation Audit & Provenance](integration_cross_organisation_audit_and_provenance.html#population-of-requesting_organization) - Added additional guidance around the population of the requesting_organization claim within the JWT.
- [General API guidance](development_general_api_guidance.html#demographic-cross-checking) - Added details relating to the expectations around Demographic Cross Checking of patient details when retrieving patient information.
- [Clinical terminologies](design_clinical_terminologies.html) - Added wording around inclusion of SNOMED DescriptionID and ConceptID.
- [Cross Organisation Audit & Provenance](integration_cross_organisation_audit_and_provenance.html) - Added guidance around temporary support for deprecated values and elements within the JWT.
- [General API guidance](development_general_api_guidance.html#fhir-api-versioning) - Updating the URL requirements on the API page with the addition of an optional routing segment.

#### [GP Connect 1.0.0-alpha.5 (Released: 17 July 2017)](https://github.com/nhsconnect/gpconnect/releases/tag/GPConnect1.0.0-alpha.5)

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
- Updated [Cross Organisation Audit and Provenance](integration_cross_organisation_audit_and_provenance.html)
	- Clarification of the usage of JWT token for consumers and providers.
- Updated [Error Handling Guidance](development_fhir_error_handling_guidance.html)
	- Addition of 501 HTTP Status code to guidance
- Updated [Clinical Terminologies](design_clinical_terminologies.html)
	- Clearer statement on case sensitivity of terminologies in FHIR
