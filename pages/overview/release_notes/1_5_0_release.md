---
title: GP Connect API 1.5.0-beta release notes
keywords: GP Connect, release notes
tags: [release]
sidebar: overview_sidebar
permalink: overview_release_notes_1_5_0_release.html
summary: "GP Connect API 1.5.0-beta released on 27th February 2020"
toc: true
---

## Introduction ##

The GP Connect API 1.5.0-beta release contains:

- The Access Document capability, which was previously published separately, has been added into this specification.
- Access Record Structured:
  - Support for diary entries
  - Support for immunisations not given

Changes may affect more than one capability.  Please see the **Affects** label for details of the capabilities changed.

This release also contains updates from the following releases:

- [1.2.6](overview_release_notes_1_2_6.html)
- [1.3.2](overview_release_notes_1_3_2.html)




## 1.5.0 changes ##

These release notes now incorporate entries from the 1.4.0, 1.4.1, Access Documents 1.0.0 and Access Documents 1.0.1 specifications that were merged into 1.5.0

### Access Document ###

#### Added Access Record Documents link to Implement a capability menu ####

**Description:**

- A new sub-menu item for Access Record Documents has been added to the Implement a capability menu. The Access Record Documents specification includes retrieval of a structured list of documents or retrieval of individual documents.
- The menu item links to the GP Connect versions page so the appropriate version of the new Access Record Documents specification can be selected as versions of the specifications may change independently.

**Page added:**

- [Access Record Documents](access_documents.html)

---

#### Added Send Document link to Implement a capability page and menu ####

**Tickets:** [#895](https://github.com/nhsconnect/gpconnect/issues/895)

**Affects:**&nbsp; Core

**Impacts:** No impact

**Description:**

- Added Send DOcument to the capabilities page
- Added a sub-menu item for Send Document to the Implement a capability menu.
- These new items link to a Send Document page which references the GP Connect versions page so the appropriate version of the Send Document specification can be selected as versions of the specifications may change independently.

**Page added:**

- [Capabilities](overview_priority_capabilities.html)
- [Send Document](send_document.html)



#### Merge separate Access Document 1.0.1 specification into this GP Connect API 1.5.0 specification ####

**Tickets:** [#933](https://github.com/nhsconnect/gpconnect/issues/933)

**Affects:**&nbsp; Access Document

**Impacts:** Provider and consumer systems

**Description:**

- The Access Document specification will no longer be published independently of this specification (GP Connect API 1.x.x).
- An Access Document capability has been created under this specification and the content of the previously separate Access Document has been merged in.
- The release notes from before the merge can be viewed here:
  - [GP Connect API - Access Document 1.0.1](overview_release_notes_documents_1_0_1.html)
  - [GP Connect API - Access Document 1.0.0](overview_release_notes_documents_1_0_0.html)

---



#### Add Investigations

**Tickets:** [#902](https://github.com/nhsconnect/gpconnect/issues/902)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Added general guidance page for Investigations
- Added description of populating the profiles for Diary Entries
- Updated pages referring to clinical areas to include Investigations
- Added `includeInvestigations` and `investigationSearchPeriod` part parameter to [`GPConnect-GetStructuredRecord-Operation-1`](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1)
- added error handling guidance for `investigationSearchPeriod`
- updated bundle population diagram to include Investigations

#### Add Outbound Referrals

**Tickets:** [#902](https://github.com/nhsconnect/gpconnect/issues/902)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Added general guidance page for Outbound Referrals
- Added description of populating the profiles for Outbound Referrals
- Updated pages referring to clinical areas to include Outbound Referrals
- Added `includeReferrals` and `referralSearchPeriod` part parameter to [`GPConnect-GetStructuredRecord-Operation-1`](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1)
- added error handling guidance for `referralSearchPeriod`
- updated bundle population diagram to include Outbound Referrals

#### Add Diary Entries

**Tickets:** [#902](https://github.com/nhsconnect/gpconnect/issues/902)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Added general guidance page for Diary Entries
- Added description of populating the ProcedureRequest profile for Diary Entries
- Added example for Diary Entries
- Updated pages referring to clinical areas to include Diary Entries
- added `includeDiaryEntries` parameter and `diaryEntriesSearchDate` part parameter to [`GPConnect-GetStructuredRecord-Operation-1`](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1)
- added error handling guidance for `diaryEntriesSearchDate`
- updated bundle population diagram to include diary entries

**Pages changed:**

- [Access Record Structured](accessrecord_structured.html)
- [Business requirements](accessrecord_structured_requirements.html)
- [Development Introduction](accessrecord_structured_development.html)
- [Resource population fundamentals](accessrecord_structured_development_resources_overview.html)
- [Linkages](accessrecord_structured_development_linkages.html)
- [Search Criteria](accessrecord_structured_development_search.html)
- [List](accessrecord_structured_development_list.html)
- [Consultation guidance](accessrecord_structured_development_consultation_guidance.html)
- [Problem guidance](accessrecord_structured_development_problems_guidance.html)
- [Diary Entry guidance](accessrecord_structured_development_diaryentry_guidance.html)
- [Diary Entry](accessrecord_structured_development_diaryentry.html)
- [Diary Entry FHIR&reg; examples](accessrecord_structured_development_fhir_examples_diaryentries.html)
- [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html)

---



#### Correction to Consultation List guidance

**Tickets:**&nbsp; [#983](https://github.com/nhsconnect/gpconnect/issues/983)

**Affects:**&nbsp; Access Record Structured

**Impacts:**&nbsp; Providers and consumers

**Description:**&nbsp;

- the `problemReference` extension has been corrected to be `relatedProblemHeader`

**Pages changed:**

- [Guidance for populating and consuming the List profile for Consultations](accessrecord_structured_development_list_consultation.html)

---



#### Updates to investigations examples

**Tickets:**

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Removed includeMedication and includeAllergies parameters from both requests
- Corrected duplicate id being used across multiple Observation resources
- added type to Observation.related
- removed use of Bundle.identifier

**Pages changed:**

- [FHIR&reg; Investigations examples](accessrecord_structured_development_fhir_examples_pathology.html)

---

## Update issued on 31st July 2020

The following changes were made to clarify and correct issues in the GP Connect 1.5.0 specification

<div class="alert alert-warning" role="alert">
  <i class="fa fa-warning"></i> <b>Important: Outstanding specification issues</b><br/>

  <p>Some profiles still require updates to bring them in line with the guidance in this specification:</p>

  <ul>
    <li>https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1/</li>
    <li>https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DocumentReference-1</li>
    <li>https://fhir.hl7.org.uk/STU3/ValueSet/CareConnect-ListCode-1</li>
    <li>https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Encounter-1</li>
  </ul>

  <p>Other known issues with the specification are documented on the <a href="accessrecord_structured_known_issues.html">Known issues page</a></p>

</div>

### Core ###

**Tickets:**

**Affects:**&nbsp; Core

**Impacts:** Provider and consumer systems

**Description:**

- The statement saying that all references **SHALL** be relative has been removed due to `DocumentReference` resources using full URLs for document locations

**Pages changed:**

- [FHIR&reg; implementation](development_fhir_api_guidance.html#resource-references)

---

### Access Document ###



#### Example updates

**Tickets:**

**Affects:**&nbsp; Access Document

**Impacts:** Provider and consumer systems

**Description:**

- An error was fixed with the date in the example of searching for a patient's documents

**Pages changed:**

- [FHIR&reg; examples](access_documents_development_fhir_examples_documents.html)

---


### Access Record Structured ###



#### Updates to examples

**Tickets:**

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Issues in the diary entry example have been fixed
- Updates were made to the investigations examples in the Access Record Structured capability
- The consultations example has been updated to use the new Lists guidance

**Pages changed:**

- [FHIR&reg; (Diary Entry) ProcedureRequest examples](accessrecord_structured_development_fhir_examples_diaryentries.html)
- [FHIR&reg; Investigations examples](accessrecord_structured_development_fhir_examples_pathology.html)
- [FHIR&reg; Consultations and Problems examples](accessrecord_structured_development_fhir_examples_consultations.html)

---

#### Updates to Consultation List profile guidance

**Tickets:**

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Guidance for the List profile for Consultations has been updated, the `problemReference` extension has been corrected to `relatedProblemHeader` to match the profile

**Pages changed:**

- [List - consultation structure](accessrecord_structured_development_list_consultation.html)

---

#### Update to multiple search parameters guidance

**Tickets:**&nbsp; [#1004](https://github.com/nhsconnect/gpconnect/issues/1004)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Guidance has been extended for requests using multiple search parameters
- Common search definitions have been added

**Pages changed:**

- [Multi area searches](accessrecord_structured_development_searchmultiareasearches)

---

#### Update to Lists guidance

**Tickets:**&nbsp; [#1007](https://github.com/nhsconnect/gpconnect/issues/1007)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- The definition of Lists has been extended to introduce secondary lists to describe the bundle content
- Guidance for populating lists with warning codes has been updated to reflect the additional lists
- A new page has been created to incorporate the extended List guidance with some content moved from the resource population fundamentals page
- The linkages page has been updated and extended to reflect these changes

**Pages changed:**

- [Using lists to return data](accessrecord_structured_development_lists_for_message_structure.html)
- [Linkages](accessrecord_structured_development_linkages.html)
- [Resource population fundamentals](accessrecord_structured_development_resources_overview.html)

---

#### Update to Problems guidance

**Tickets:**&nbsp; [#1008](https://github.com/nhsconnect/gpconnect/issues/1008), [#1010](https://github.com/nhsconnect/gpconnect/issues/1010)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- The list of clinical item references has been updated to include consultations / encounters
- Guidance for out of scope items (complete diary entries and test requests outside of investigations) which are linked to problems

**Pages changed:**

- [Problem guidance - clinical items](accessrecord_structured_development_problems_guidance.html#clinical-item-references)
- [Problem guidance - out of scope items](accessrecord_structured_development_problems_guidance.html#problems-linking-to-out-of-scope-clinical-items)

---

#### Update to Problem Header profile guidance

**Tickets:**&nbsp; [#1012](https://github.com/nhsconnect/gpconnect/issues/1012)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Update to the actualProblem extension guidance to include all clinical areas for this specification
- Update to the relatedClinicalItems extension guidance to include all clinical areas for this specification

**Pages changed:**

- [Problem Header profile guidance](accessrecord_structured_problems.html)

---

#### Update to Consultation guidance

**Tickets:**&nbsp; [#1009](https://github.com/nhsconnect/gpconnect/issues/1009)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Detail on returning out of scope items from clinical areas as text has been added

**Pages changed:**

- [Consultation guidance](accessrecord_structured_development_consultation_guidance.html#coded-clinical-items-returned-as-text)

---

#### Update to include Inbound Referrals in Uncategorised Data

**Tickets:**&nbsp; [#1013](https://github.com/nhsconnect/gpconnect/issues/1013)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Inbound referrals referenced in scope of uncategorised data
- Referrals guidance references inbound referrals covered by uncategorised data

**Pages changed:**

- [Uncategorised data guidance](accessrecord_structured_development_uncategoriseddata_guidance#uncategorised-data-definition)
- [Referrals guidance](accessrecord_structured_development_referralrequest_guidance.html#what-is-an-outbound-referral)

---

#### Update to documents returned in Access Record Structured

**Tickets:**&nbsp;

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- A note has been added to the linkages page to state that consumers must have implemented the Access Document capability to retrieve documents linked from returned `DocumentReference` resources
- The documents guidance page has been updated to state that consumers must have implemented the Access Document capability to retrieve documents linked from returned `DocumentReference` resources

**Pages changed:**

- [Linkages](accessrecord_structured_development_linkages.html)

---

## Update issued on 1st October 2020

The following changes were made to clarify and correct issues in the GP Connect 1.5.0 specification

Known issues with the specification are documented on the <a href="accessrecord_structured_known_issues.html">Known issues page</a>

---

### Access Record Structured ###

#### Update to Investigations diagrams

**Tickets:**&nbsp; [#1021](https://github.com/nhsconnect/gpconnect/issues/1021)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Diagrams changed to reflect filling comments are referenced from the diagnostic report and not the other direction

**Pages changed:**

- [Linkages](accessrecord_structured_development_linkages.html)
- [Problem guidance](accessrecord_structured_development_problems_guidance.html)

---

#### Empty list guidance

**Tickets:**&nbsp; [#900](https://github.com/nhsconnect/gpconnect/issues/900)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Corrected the empty reason code for investigations and referrals

**Pages changed:**

- [Investigations guidance](accessrecord_structured_development_pathology_guidance.html)
- [Referrals guidance](accessrecord_structured_development_referralrequest_guidance.html)

---

#### Filing comments for a test result

**Tickets:**&nbsp; [#1024](https://github.com/nhsconnect/gpconnect/issues/1024)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Guidance for the filling comments observation profile has been updated to reference population of elements where the comments relate to a single test result

**Pages changed:**

- [Observation - Filing Comments](accessrecord_structured_development_observation_filingcomments)

---


#### Confidential items in consultations

**Tickets:**&nbsp; [#1029](https://github.com/nhsconnect/gpconnect/issues/1029)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Updated the description for confidential items in consultations to reference secondary lists

**Pages changed:**

- [Consultation guidance](accessrecord_structured_development_consultation_guidance.html)

---

#### Fixed issue in requests in multi area searches page

**Tickets:**&nbsp; [#1030](https://github.com/nhsconnect/gpconnect/issues/1030), [#1023](https://github.com/nhsconnect/gpconnect/issues/1023)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Example requests have been updated to be valid requests. The example now says 365 days instead of 1 year.

**Pages changed:**

- [Multi area searches](accessrecord_structured_development_searchmultiareasearches,html)

---

#### Updated the guidance around blood pressure following the curation outcomes

**Tickets:**&nbsp; [#1027](https://github.com/nhsconnect/gpconnect/issues/1027), [#1028](https://github.com/nhsconnect/gpconnect/issues/1028)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Updated to describe how bp's are recorded in GP systems and include details of which blood pressures should be exported as a triple.

**Pages changed:**

- [Uncategorised data](accessrecord_structured_development_uncategoriseddata_guidance.html)

---
#### Updated the guidance around fasting status in investigations specimens

**Tickets:**&nbsp; [#1018](https://github.com/nhsconnect/gpconnect/issues/1018)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Updated to describe how to populate the fasting status with data from EDIFACT.

**Pages changed:**

- [IInvestigations specimen](accessrecord_structured_development_specimen)

---

#### Updated the guidance on how and when to populate list.date

**Tickets:**&nbsp; [#1014](https://github.com/nhsconnect/gpconnect/issues/1014)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Updated to describe how to populate the list.date field.

**Pages changed:**

- [Sturctural resources list page](accessrecord_structured_development_list.html)

---


#### Updated the guidance on using lists to return data

**Tickets:**&nbsp; [#1022](https://github.com/nhsconnect/gpconnect/issues/1022)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Following curation this has been updated to reflect the new secondary list codes

**Pages changed:**

- [Returning data in lists](accessrecord_structured_development_lists_for_message_structure.html)

---

#### Uncategorised data value units

**Tickets:**&nbsp; [#754](https://github.com/nhsconnect/gpconnect/issues/754)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Added a note to the Uncategorised data observation page that suppliers MUST use the units from the FHIR spec vital signs page.

**Pages changed:**

- [Uncategorised data observation](accessrecord_structured_development_observation_uncategoriseddata.html)

---

#### Immunisations not given

**Tickets:**&nbsp; [#977](https://github.com/nhsconnect/gpconnect/issues/977), [#987](https://github.com/nhsconnect/gpconnect/issues/987)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- Updated guidance and profile definition following addition of 'not done' situation codes to the valueset for the vaccination procedure

**Pages changed:**

- [Immunisation guidance](accessrecord_structured_development_immunization_guidance.html)
- [Immunization](accessrecord_structured_development_immunization.html)

---


## Updates following last release

The following changes were made to clarify and correct issues in the GP Connect 1.5.0 specification:





### Change to document type refset

**Affects:**&nbsp; Access Documents

**Impacts:** Provider and consumer systems

**Description:**

- The refset to use for the document type is changed

**Pages changed:**

- [DocumentReference](access_documents_development_documentreference.html#type)

---



### Updated guidance for immunisations

**Tickets:**&nbsp; [#1036](https://github.com/nhsconnect/gpconnect/issues/1036), [#1053](https://github.com/nhsconnect/gpconnect/issues/1053), [#987](https://github.com/nhsconnect/gpconnect/issues/987),

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Medication records for immunisations are treated as medications and returned against medication not immunisation requests
- Guidance on notes population updated to remove reference to free text manufacturer
- Extended scope from inclusion of consent and dissent information to cover any coded information recorded within an immunisation module or categorised as immunisation data in the GP system

**Pages changed:**

- [Immunisations guidance](accessrecord_structured_development_immunization_guidance.html)

---


### Updated link for secondary list CodeSystem

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Link to CodeSystem has been updated to [https://fhir.hl7.org.uk/STU3/CodeSystem/GPConnect-SecondaryListValues-1](https://fhir.hl7.org.uk/STU3/CodeSystem/GPConnect-SecondaryListValues-1)

**Pages changed:**

- [Using lists to return data](accessrecord_structured_development_lists_for_message_structure.html)

---




### Updated the profile description of uncategorised data observation

**Tickets:**&nbsp; [#1052](https://github.com/nhsconnect/gpconnect/issues/1052), [#1040](https://github.com/nhsconnect/gpconnect/issues/1040), [#1037](https://github.com/nhsconnect/gpconnect/issues/1037)

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Updated to reflect the range of data that can be used to populate the component element
- Updated the performer element to include organization in reference types
- Minor re-word for code for free text

**Pages changed:**

- [Observation - uncategorised data)](accessrecord_structured_development_observation_uncategoriseddata.html)

---

### Added guidance for inbound referrals

**Tickets:** [#1066](https://github.com/nhsconnect/gpconnect/issues/1066)

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Section added with additional guidance for populating the observation resource for an inbound referral and updated the profile guidance

**Pages changed:**

- [Uncategorised data guidance](accessrecord_structured_development_uncategoriseddata_guidance)
- [Observation - uncategorised data](accessrecord_structured_development_observation_uncategoriseddata)

---

### Updates to Investigations guidance

**Tickets:** [#1051](https://github.com/nhsconnect/gpconnect/issues/1051), [#1061](https://github.com/nhsconnect/gpconnect/issues/1061), [#1063](https://github.com/nhsconnect/gpconnect/issues/1063)

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Add a line to say to use \n to keep line breaks in textual results. Updated pathology guidance page to specify use of \n to maintain line breaks.
- Note added regarding linkage between investigations and problems
- DiagnosticReport guidance for result element expanded to be explicit that only test result which are not part of a test group should be referenced from this element

**Pages changed:**

- [Investigations guidance](accessrecord_structured_development_pathology_guidance.html)
- [DiagnosticReport](accessrecord_structured_development_diagnosticreport#result)

---

### Remove warning codes from resource pop fundamentals

**Tickets:** #1050

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Removed and replaced with a link to the returning data in lists page.

**Pages changed:**

- [Resource population fundamentals)](accessrecord_structured_development_resources_overview.html)and [Using lists to return data](accessrecord_structured_development_lists_for_message_structure.html)

---

### Investigations - How to handle Confidential items inside a report

**Tickets:** #1047

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Users in providing systems can flag reports results and headers as confidential within a diagnosticReport. Updated confidential items text to reflect this.

**Pages changed:**

- [Using lists to return data](accessrecord_structured_development_lists_for_message_structure.html)

---

### Updated diagrams for linkages between resources

**Tickets:** &nbsp; [#1042](https://github.com/nhsconnect/gpconnect/issues/1042), [#1044](https://github.com/nhsconnect/gpconnect/issues/1044), [#1060](https://github.com/nhsconnect/gpconnect/issues/1060)

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Diagrams updated to show correct relationship of linkages for filing comments
- Diagrams updated to show additional problem and consultation linkages
- Note added that diagrams do not include all possible linkages

**Pages changed:**

- [Linkages](accessrecord_structured_development_linkages.html)
- [Problem guidance](accessrecord_structured_development_problems_guidance.html)

---

### Change how to deal with split plans due to a change in dose

**Tickets:** #1046

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Add detail to the spec that describes how to split plans.

  Also detail how it applies to a date filter. Details about the repeatInformation. Details of how to change the ids. Use of priorPrescription element.

  Updated the medication guidance with example and removed dosageLastChanged extension from Med Statement page

**Pages changed:**

- [Medication guidance](accessrecord_structured_development_medication_guidance.html)

---

### Updated medication request profile guidance

**Tickets:** [#993](https://github.com/nhsconnect/gpconnect/issues/993)

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Removed acute-handwritten from list of supported prescription types

**Pages changed:**

- [medicationRequest](accessrecord_structured_development_medicationrequest.html)

---

### List of Lists - Path header/result as a problem

**Tickets:** #1043

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

-  it is possible to flag test result headers/results as Problems.

  Currently the specification states that only the DiagnosticReport can be linked to a Problem, should this be updated to state that the child resources can also be linked

  Updated the linkages page to say the DiagnosticReport must be linked as a related clinical item when any containing element is made a problem.

**Pages changed:**

- [Linkages page - problem section](accessrecord_structured_development_linkages.html)

---

### Corrected allergies example

**Tickets:** #1038

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

-  Corrected third allergies example to use correct value for `note` field
- Updated descriptions for examples two and three to reflect content of example

**Pages changed:**

- [Allergies FHIR examples](accessrecord_structured_development_fhir_examples_allergies.html)

---


### Diary Entries Search

**Tickets:** &nbsp; [#1062](https://github.com/nhsconnect/gpconnect/issues/1062)

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- Note added regarding search criteria to be explicit about inclusion of historic, active diary entries

**Pages changed:**

- [Diary entry guidance](accessrecord_structured_development_diaryentry_guidance.html#diary-entry-planned-date)

---


### Update to guidance on free text records

**Tickets:** &nbsp; [#1037](https://github.com/nhsconnect/gpconnect/issues/1037)

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

Minor changes to the text to clarify that free text recorded in consultation use the observation resource as defined under uncategorised data, but free text which is not associated with a c;linical code must only be returned in the context of a consultation (and problem when linking a consultation topic items) and not in response to only an uncategorised data request.

**Pages changed:**

- [Uncategorised data guidance](accessrecord_structured_development_uncategoriseddata_guidance#uncategorised-data-definition)
- [Consultation guidance](accessrecord_structured_development_consultation_guidance.html#consultation-notes)

---

### Updated List guidance 

**Tickets:** &nbsp; [#1115](https://github.com/nhsconnect/gpconnect/issues/1115)

**Affects:**&nbsp; Access Structured

**Impacts:** Provider systems

**Description:**

Updated the guidance for the title element, so that it referenced using the titles defined in the 'Using lists to return data' guidance.

**Pages changed:**

- [List](accessrecord_structured_development_list.html#title)

---

## NEW NOTES FOR RELEASE

Notes under here for the published version

### Access Document

---

#### Added Access Document capability to 1.5.0 ####

**Affects**&nbsp; Access Documents

**Description:**

- Access Document has been moved from a separate specification into 1.5.0
- Update service root URL definition to accommodate the Access Document capability API being defined as its own FHIR server
- Add explicit error handling response for Access Document calls

**Pages changed:**

- [Search for a patient's documents](access_documents_development_search_patient_documents.html)
- [Retrieve a patient's documents](access_documents_development_retrieve_patient_documents.html)
- [Consumer sessions illustrated](access_documents_development_api_session.html)
- [Interaction IDs](integration_interaction_ids.html)
- [General API guidance](development_general_api_guidance.html#service-root-url)
- [Find a patient](access_documents_use_case_find_a_patient.html)

---

#### Document search API updates ####

**Tickets:** [#941](https://github.com/nhsconnect/gpconnect/issues/941)

**Affects:**&nbsp; Access Document

**Impacts:** Provider and consumer systems

**Description:**

- Change search for patient documents to use a patient compartment based URL
-   Previously: `/DocumentReference?patientId=111&queryParam=`
-   Now: `/Patient/111/DocumentReference?queryParam=`
- The syntax of the Patient `_include` parameter for Search for a patient's documents was incorrect and has been updated
- the facility parameter now uses a token instead of an identifier as its datatype
- Updated examples to include all search parameters
- The facility parameter was updated to use a token instead of an identifier when searching for a patient's documents.
- Practitioner and PractitionerRole resources for supplementary actors have been added to the response payload
- The `type` and `facility` search parameters have been removed from the search API in the Access Documents capability
- The `description` parameter has been updated to state it's a keyword based search and that `DocumentReference.type` and `DocumentReference.title` will be searched.
- Corrected description of `author` parameter to be a `token` in line with the rest of the specification

**Pages changed:**

- [Search for a patient's documents](access_documents_development_search_patient_documents.html)
- [FHIR&reg; examples](access_documents_development_fhir_examples_documents.html)
- [Get the FHIR&reg; capability statement (Access Document)](access_documents_use_case_get_the_fhir_capability_statement.html)

---

#### Find Patient API updates ####

**Tickets:** [#938](https://github.com/nhsconnect/gpconnect/issues/938)

**Affects:**&nbsp; Access Document

**Impacts:** Provider and consumer systems

**Description:**

- Find Patient is Access Document should return only return patients who have a Regular/GMS registration type (i.e. patients where this is their registered practice)
- Temporary, emergency and other non regular registration types must be excluded from the results
- This behaviour applies only to Find Patient in the Access Document capability
- The error condition for an `INVALID_IDENTIFIER_SYSTEM` in Find a patient has been changed to `INVALID_PARAMETER`

**Pages changed:**

---

#### Error response when a capability is disabled by the practice ####

**Tickets:** [#943](https://github.com/nhsconnect/gpconnect/issues/943)

**Affects:**&nbsp; Access Document

**Impacts:** Provider and consumer systems

**Description:**

- Add error handling behaviour for each API endpoint when GP Connect as a whole or the Access Document capability is disabled

**Pages changed:**

- [Get the FHIR&reg; capability statement (Access Document)](access_documents_use_case_get_the_fhir_capability_statement.html#error-handling)
- [Find a patient (Access Document)](access_documents_use_case_find_a_patient.html#error-handling)
- [Search for a patient's documents](access_documents_development_search_patient_documents.html#error-handling)
- [Retrieve a document](access_documents_development_retrieve_patient_documents.html#error-handling)

---

#### Clarification of Bundle.fullUrl ####

**Tickets:** [#967](https://github.com/nhsconnect/gpconnect/issues/967)

**Affects:**&nbsp; Access Document

**Impacts:** Provider and consumer systems

**Description:**

- Clarification has been added on use of URLs in Bundle.fullUrl. They **MUST** be used even when not resolvable as these are intended for use by consumers when resolving references in the bundle and not for retrieving resources..

**Pages changed:**

- [Search for a patient's documents](access_documents_development_search_patient_documents.html)
- [FHIR&reg; examples](access_documents_development_fhir_examples_documents.html)

---


#### Updates to CapabilityStatement

**Tickets:**

**Affects:**&nbsp; Access Document

**Impacts:** Provider and consumer systems

**Description:**

- version number has been set to 1.5.0
- CapabilityStatement for Access Document has been updated so that correct types are used for search parameters
- subject, type and facility have been removed from search parameters
- the read interaction has been removed from Patient.
- Add minor version numbers to profiles listed in the capability statement

**Pages changed:**

- [Get the FHIR&reg; capability statement](access_documents_use_case_get_the_fhir_capability_statement.html)

---

#### Updates to DocumentReference population guidance

**Tickets:**

**Affects:**&nbsp; Access Document

**Impacts:** Provider and consumer systems

**Description:**

- Guidance for the DocumentReference profile has been updated, the MIME type for the document is now recorded in `content.attachment.contentType`. This replaces the use of `content.format`.
- DocumentReference.context.practiceSetting guidance updated so text can be used where code is outside of refset
- DocumentReference.identifier guidance has been updated in line with use of identifier attributes in Access Record Structured
- DocumentReference.content.attachment.title SHOULD be populated with a reason when a document is unavailable

**Pages changed:**

- [DocumentReference](access_documents_development_documentreference.html)

---

### Document retrieval file size limit

**Affects:**&nbsp; Access Documents

**Impacts:** Provider and consumer systems

**Description:**

- A file size limit has been introduced to the Access Documents capability, documents over 5mb will not be retrievable.
- An error will be returned by the provider system if a document larger than 5mb is requested
- Clarification on how to set file size for documents that aren't available

**Pages changed:**

- [Guidance for the representation and consumption of documents](access_documents_development_documents_guidance.html#file-size-of-the-document)
- [Retrieve a document](access_documents_development_retrieve_patient_documents.html)

---

### Access Record Structured ###

#### Add immunisations not given

**Tickets:** [#849](https://github.com/nhsconnect/gpconnect/issues/849)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- added `includeNotGiven` part parameter to [`GPConnect-GetStructuredRecord-Operation-1`](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1) with a default value of `false`
- added `includeDissentConsent` part parameter to [`GPConnect-GetStructuredRecord-Operation-1`](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1) with a default value of `false`
- updated bundle population diagram to include `includeNotGiven` and `includeStatus` part parameters and `QuestionnaireResponse`
- Updated immunisation guidance to include details of inclusion of immunisation not given for providers
- Added guidance for consumers for handling immunisations not given
- Updated immunization profile to include additional guidance and valuesets
- Observations representing the status of a patient's immunisations will be returned
- includeImmunisations.includeStatus has a default value of `true`
- Added QuestionnaireResponse to uncategorised data response


**Pages changed:**

- [Search Criteria](accessrecord_structured_development_search.html)
- [Immunisations guidance](accessrecord_structured_development_immunization_guidance.html)
- [Immunization](accessrecord_structured_development_immunization.html)
- [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html)

---


#### API Updates ####

**Tickets:**&nbsp; [#904](https://github.com/nhsconnect/gpconnect/issues/914)

**Affects:**&nbsp; Access Record Structured

**Impacts:**&nbsp; Providers and consumers

**Description:**&nbsp;

- An error condition has been added that states part parameters must not be included without a value
- Clarification stating that it is valid to include an empty Parameters.parameter in the case where it has only specified with optional part parameters.
- Part parameters have been added to the mot permitted parameter combinations
  - `includeReferrals.referralSearchPeriod`
  - `includeDiaryEntries.diaryEntriesSearchDate`
  - `includeImmunisations.includeNotGiven`
  - `includeImmunisations.includeDissentConsent`
- The error code for access denied has been updated to use the value from the value set, `ACCESS DENIED`
- Clarification has been added around how information with partial or unknown dates should be returned for clinical areas which have date search parameters

**Pages changed:**&nbsp;

- [Retrieve a patient's record - error handling](accessrecord_structured_development_retrieve_patient_record.html#error-handling)

---

#### Updates to profiles

**Affects:**&nbsp; Access Record Structured

**Impacts:**&nbsp; Providers and consumers

**Description:**&nbsp;

- The `crossCareSettingIdentifier` slice on `identifier` has been removed from the following profiles:
  - [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DiagnosticReport-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-DiagnosticReport-1/_history/1.3)
  - [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ProcedureRequest-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ProcedureRequest-1/_history/1.3)
  - [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Immunization-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Immunization-1/_history/1.5)
  - [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Observation-1/_history/1.4)
  - [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-ReferralRequest-1/_history/1.2)
  - [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Specimen-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Specimen-1/_history/1.3)

**Pages changed:**&nbsp;

- [DiagnosticReport](accessrecord_structured_development_DiagnosticReport.html)
- [ProcedureRequest](accessrecord_structured_development_ProcedureRequest.html)
- [DiaryEntry - ProcedureRequest](accessrecord_structured_development_diaryentry.html)
- [Immunization](accessrecord_structured_development_immunization.html)
- [Observation - Filing Comments](accessrecord_structured_development_observation_filingcomments.html)
- [Observation - Narrative](accessrecord_structured_development_guidance_observation_narrative.html)
- [Observation - Test Group Header](accessrecord_structured_development_observation_testGroup.html)
- [Observation - Test Result](accessrecord_structured_development_observation_testResult.html)
- [ReferralRequest](accessrecord_structured_development_referralrequest.html)
- [Specimen](accessrecord_structured_development_specimen.html)

---


#### Updates to structured capability statement

**Affects:**&nbsp; Access Record Structured

**Impacts:**&nbsp; Providers and consumers

**Description:**&nbsp;

- update version number in CapabilityStatement to 1.5.0
- update minor version numbers in profile listing
- update OperationDefinition minor version number
- HealthcareService has been added to the CapabilityStatement

**Pages changed:**

- [Get the FHIR&reg; capability statement (Access Record Structured)](accessrecord_structured_get_the_fhir_capability_statement.html)

---

#### Configuration of supported clinical areas

**Tickets:**&nbsp; [#1026](https://github.com/nhsconnect/gpconnect/issues/1026)

**Affects:**&nbsp; Access Record Structured

**Impacts:** Provider and consumer systems

**Description:**

- A page has been added with guidance on how provider systems **MUST** be able to configure which clinical areas are available
- The API has been updated to state how unavailable clinical areas are returned
- Guidance on unavailable clinical areas has been added to the Linkages page
- Guidance on populating references has been added
- A list of configurable clinical areas has been added
- The warning has been updated for populating an `OperationOutcome`
- Empty lists with basic information are permitted to be returned for disabled clinical areas.
- Switching off a clinical are MUST be achieved via a single configuration item or action.
- Documents must be switched off when the Access Documents capability is switched off

**Pages changed:**

- [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html#unavailability-of-data)
- [Configuration for supported clinical areas](accessrecord_structured_development_clinical_area_config.html)
- [Linkages](accessrecord_structured_development_linkages.html)

---

### Bundle.id must now be populated

**Affects:**&nbsp; Access Structured, Access Document

**Impacts:** Provider and consumer systems

**Description:**

- Bundle.id must now be populated.

**Pages changed:**

- [Bundle](accessrecord_structured_development_bundle.html)
- [Bundle](access_documents_development_bundle.html)

---

### Updated examples for includeNumberOfMostRecent part parameter

**Affects:**&nbsp; Access Structured

**Impacts:** Provider and consumer systems

**Description:**

- All examples of `includeNumberOfMostRecent` have been updated to use valuePositiveInt inline with the specification

**Pages changed:**

- [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html)
- [FHIR&reg; Examples](accessrecord_structured_development_fhir_examples_consultations.html)
- [Search examples](accessrecord_structured_development_searchExamples.html)
- [Multi area searches](accessrecord_structured_development_searchmultiareasearches)

---
