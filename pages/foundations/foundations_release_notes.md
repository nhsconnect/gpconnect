---
title: Foundations Release Notes
keywords: foundations, release notes
tags: []
sidebar: foundations_sidebar
permalink: foundations_release_notes.html
summary: "Release notes for the various versions of the Foundations capability."
---

#### [1.0.0-rc.4 (Released: 28/11/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_rc.3_Foundations_rc.4_GP_Connect_rc.1)

{% include important.html content="Release 1.0.0-rc.4 contains a change of FHIR version from DSTU2 to STU3 as the base fhir version for the GP Connect API Capbility." %}

- [Get the FHIR CapabilityStatement](foundations_use_case_get_the_fhir_capability_statement.html) - Conformance statment page has been updated to reflect the change in STU3 to a CapabilityStatement resource.
- [Foundation Resources](datalibraryfoundation.html) - Updated the resources to be the new GP Connect profiled STU3 resources.
- [Design Decisions](foundations_design.html#definition-of-organisation-and-location-entities), [Book an appointment](appointments_use_case_book_an_appointment.html#payload-request-body) - Added additional detail around the expected use of the Location and Organization where there specific meaning within the Appointment resource and the Patient resource.
- [Information Governance](foundations_ig.html) - Added business rule for application of PDS S-Flag

#### [1.0.0-rc.3 (Released: 06/10/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_rc.1_and_Foundations_rc.3_release)
- [Register a patient](foundations_use_case_register_a_patient.html#payload-request-body) - Additional fields in patient profile which are marked with Must-Support flag 
- [Foundations Design](foundations_design.html#definition-of-organisation-and-location-entities) - Added design decision to clarify how GP practice organisations and practice sites are represented in the FHIR Organization and Location resources.
- [Foundation Resources](datalibraryfoundation.html#register-a-patient), [Register a patient](foundations_use_case_register_a_patient.html#payload-response-body) - Changed "Register a patient" response to use "gpconnect-searchset-bundle-1" profiled bundle resource rather than the "gpconnect-registerpatient-bundle-1" profiled bundle resource.
- [Register a Patient](foundations_use_case_register_a_patient.html#payload-response-body) - registrationStatus extension element has been removed. Active status can be indicated through Patient.active element.
- [Find a patient](foundations_use_case_find_a_patient.html), [Read a patient](foundations_use_case_read_a_patient.html), [Register a patient](foundations_use_case_register_a_patient.html) - Update patient resource examples to conform to structured definition.
- [Find a Location]() - the API Use Case for "Find a Location" has been removed from the specification
- [Register a patient](foundations_use_case_register_a_patient.html) - Added guidance on Register patient around consumer providing and storage expectaions for patient telecom and address information.

#### [1.0.0-rc.2 (Released: 08/09/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Appointment_beta.2_and_Foundations_rc.2_release)
- Updated the system identifier uri's for Patient (https://fhir.nhs.uk/Id/nhs-number), Practitioner (https://fhir.nhs.uk/Id/sds-user-id), Organization (https://fhir.nhs.uk/Id/ods-organization-code) and Location (https://fhir.nhs.uk/Id/ods-site-code), this affects all the "Find" foundation API Use Cases. (Pages - development_fhir_operation_guidance.html, foundations_design.html, foundations_use_case_find_a_patient.html, foundations_use_case_find_a_practitioner.html, foundations_use_case_find_an_organisation.html, foundations_use_case_find_a_location.html)
- [Read Organization](foundations_use_case_read_an_organisation.html), [Conformance Profile](foundations_use_case_get_the_fhir_capability_statement.html), [Read Location](foundations_use_case_read_a_location.html), [Register Patient](foundations_use_case_register_a_patient.html) - Updated examples to conform to Care Connect profile uplifts.
- [Glossary](overview_glossary.html#active-patient) - updated glossary to make definition of Active Patient clear, used in [Find a Patient](foundations_use_case_find_a_patient.html) API Use Case.
- [Register Patient](foundations_use_case_register_a_patient.html) - Updated register patient example response to include the registration details extension.

#### [1.0.0-rc.1 (Released: 01/09/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Foundations_1.0.0-rc.1)
- Updated datalibrary to be capability specific, moving it to reside under the "Development" menu within the capability. This is to allow the Profiled FHIR Resources to be referenced per capability and updated independantly. For foundations we have updated specification to reference FHIR profiles stored on FHIR reference server rather than those on the old DMS capability pack.
- Updated Api Use Case pages to make clear the expectations around the Fhir Resource Metadata Profile element, along with updates to examples to show new profile definitions.
- Added information around what GP Connect considers as an Active Patient and use of Active Patient within the "Find a patient" capability (Page - foundations_use_case_find_a_patient.html, overview_glossary.html).
- Added additional information for "Register Patient" capability around re-activating inactive patients instead of registering new patient each time. (Page - foundations_use_case_register_a_patient.html)
- Removed the Practitioner and Organization as mandatory resources within the response bundle for the "Register Patient" interaction (Page - foundations_use_case_register_a_patient.html)
- Added clarification around the use of the "registrationDetails" extension for the "Register patient" interaction (Page - foundations_use_case_register_a_patient.html)
- Removed ODS-Site-Code as a search parameter and identifier from the Organization resource for "Find Organization" and "Organization Read"

#### [1.0.0-beta.2 (Released: 11/08/2017)](https://github.com/nhsconnect/gpconnect/releases/tag/Foundations1.0.0-beta.2)
- Updated example conformance profile to include GP Connect profile information (Page - [Get the FHIR Conformance Statement](foundations_use_case_get_the_fhir_capability_statement.html)).
- Clarified use of [Register a patient](foundations_use_case_register_a_patient.html) API is only to support local-only temporary patient registrations to support federated appointment booking
- Added additional clarification around use of identifiers for all foundation search capabilities (Pages - Find a practitioner, Find a patient, Find an organisation, Find a location).
- Clarity on mandatory data items for [Register a patient](foundations_use_case_register_a_patient.html#payload-request-body) API
- Moved VRead to out of scope (Pages - [Get the FHIR Conformance Statement, Common API Guidance](foundations_use_case_get_the_fhir_capability_statement.html))
- Added java example code to specification for Read capabilities (Pages - Read a practitioner, Read a patient, Read an organisation, Read a location).
- Updated example code to bring in line with [FHIR Server Root URL format](development_fhir_api_guidance.html#fhir-api-versioning) guidance.
- Updates to [Register a patient](foundations_use_case_register_a_patient.html) to include latest operation definition XML, and provide clarity on profiles used on response.

#### 1.0.0-beta.1
- Initial release of the Foundations capability pack on GitHub in early August 2016.
  
#### 1.0.0-alpha.1
- Initial release for feedback/comments as part of the late May 2016 release.
