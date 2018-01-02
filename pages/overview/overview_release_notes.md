---
title: GP Connect release notes
keywords: GP Connect, release notes
tags: [release]
sidebar: overview_sidebar
permalink: overview_release_notes.html
summary: "Release notes for the GP Connect"
---

#### GP Connect 1.0.0-rc.2 (Released: )

- [FHIR API guidance](development_fhir_api_guidance.html)
  - Updated the must support requirements section to indicate that if an element is marked as must support then all sub elements of that element should also be considered must support.

- [General API guidance](development_general_api_guidance.html)
  - Updated requirements for support of XML and JSON.
  - [Content types](development_general_api_guidance.html#content-types) - Added additional guidance of what to do if no `Accept` header or `_format` parameter is receieved as part of the request.
  
- [Glossary](overview_glossary.html)
  - Updated definition of active patient to include specific wording for the requirement that a patient must have been traced and verified.

#### [GP Connect 1.0.0-rc.1 (Released: 28/11/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_rc.3_Foundations_rc.4_GP_Connect_rc.1)

- [Security guidance](development_api_security_guidance.html) - updated security guidance around the protocols that suppliers should implement
- [Cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html) - updated JSON Web Tokens (JWT) specification examples to use the new profile and value sets and included requirement for patient demographic cross-checking
- [Operation guidance](development_fhir_operation_guidance.html#foundations-capability-interactions) - corrected 'Example URL pattern' for searches so that `System` and `Code` are in the correct order
- [Error handling guidance](development_fhir_error_handling_guidance.html) - updated page to reflect move from 'gpconnect-error-or-warning-code-1' to 'spine-error-or-warning-code-1'
- [Security guidance](development_api_security_guidance.html) - removed contradiction within specification for cache-control headers
- [Common API guidance](development_fhir_api_guidance.html#resource-metadata) - uplifted guidance around the inclusion of profile details within the FHIR resource metadata element when a consumer performs a create or amend interaction
- [Common API guidance](development_fhir_api_guidance.html#update-resource) - added clarification on use of PUT to make clear an update should not create a resource if the resource being updated does not already exist
- [Common API guidance](development_fhir_api_guidance.html) - added guidance on the behaviour of consumer and provider systems where Must-Support flag is present 
- [Common API guidance](development_fhir_api_guidance.html) - split this page into 'General API guidance' and 'FHIR implementation guidance' pages
- [Cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html#population-of-requested_record) - added section to clarify the expected use of the `requested_record` claim within the JWT
- [Information governance principles](designprinciples_ig_principles.html) - updated teminology around the consumer responsibilities in regards to NHS Codes of Practice and Legal Obligations related to the use of GP Connect API;  additionally added reference to the ongoing review of the information governance (IG) model, particularly in the light of General Data Protection Regulation (GDPR);  additionally added more Access Record capability links to 'Patient dissent to share' and indicated that this was not applicable to Appointment Management capability
- [Fhir library guidance](development_fhir_open_source_guidance.html) - the FHIR library guidance page has been updated to improve GP Connect guidance around using existing FHIR libraries to aid its development
- [Error handling guidance](development_fhir_error_handling_guidance.html) - updated error handling guidance to include expectations around a resource not found, provide details of Spine error codes expected and restructured to clarify differing error condition types. 
- [FHIR API guidance](development_fhir_api_guidance.html) - corrected in scope search prefixes to be consistent with other pages
- [Cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html#population-of-requesting_organization) - added additional guidance around the population of the requesting_organization claim within the JWT
- [General API guidance](development_general_api_guidance.html#demographic-cross-checking) - added details relating to the expectations around demographic cross checking of patient details when retrieving patient information
- [Clinical terminologies](design_clinical_terminologies.html) - added wording around inclusion of SNOMED DescriptionID and ConceptID
- [Cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html) - added guidance around temporary support for deprecated values and elements within the JWT
- [General API guidance](development_general_api_guidance.html#fhir-api-versioning) - updated the URL requirements on the API page with the addition of an optional routing segment

#### [GP Connect 1.0.0-alpha.5 (Released: 17 July 2017)](https://github.com/nhsconnect/gpconnect/releases/tag/GPConnect1.0.0-alpha.5)

- updated [Common API guidance](development_fhir_api_guidance.html)
	- clarification on API versioning and FHIR server root URL formats
	- more detail of the principles of resource identity
	- removed references to superceded RFC 2616, replacing with the updated references
- updated [Personal Demographics Service](integration_personal_demographic_service.html)
	- note regarding the use of PDS trace sequence number to enable efficient caching
- updated [Spine Security Policy implementation guide](integration_spine_security_proxy_implementation_guide.html)
	- requirement that FHIR root server URL SHALL contain practice level identifier
	- addition of HTTP status code 599 error which can in some circumstances be returned from the Spine Security Proxy
- updated [Security guidance](development_api_security_guidance.html)
	- clarification of provider responsibilities for HTTP header validation
- updated [Cross organisation audit and provenance](integration_cross_organisation_audit_and_provenance.html)
	- clarification of the usage of JWT token for consumers and providers
- updated [Error handling guidance](development_fhir_error_handling_guidance.html)
	- addition of 501 HTTP Status code to guidance
- updated [Clinical terminologies](design_clinical_terminologies.html)
	- clearer statement on case sensitivity of terminologies in FHIR
