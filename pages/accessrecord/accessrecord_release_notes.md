---
title: Access Record Release Notes
keywords: getcarerecord, release notes
tags: []
sidebar: accessrecord_sidebar
permalink: accessrecord_release_notes.html
summary: "Release notes for the various versions of the Access Record capability."
---

#### 1.0.0-rc.3 (Released: 20th February)

- Updated [Access Record Design Decisions](accessrecord_design.html)
  - Wording uplifted to include GP-Practice designated Confidential Items 
  
-  Updated [Design_Principles](designprinciples_ig_principles.html)
-Wording uplifted to include Confidential Items Exclusion
    
- Updated [Allergies](accessrecord_view_allergies.html)
-Wording uplifted to reflect EMIS not providing Historical Allergies

#### 1.0.0-rc.3 (Released: 6th February)

- Updated [Access Record HTML Implementation Guide](accessrecord_development_html_implementation_guide.html)  
  - Added wording around 'In-transit' record to this page.
  - Added additional wording for Consumer Date-Ranges to include all times from the start date to the end of the end date.
  - Default Time-Frames -  Problems, removed footnote indicating that this section should not have time-frames applied;  time-frames are NOT applied for Active Probs, but are applied for 'Inactive Probs' sub-section
- Updated [Integration Cross Organisation Audit and Provenance](integration_cross_organisation_audit_and_provenance.html)
  - Added wording such that in the scenario where the user has a local role as well as a national role, then the national RBAC role shall be provided
  - Added a sentence to require the Spine RBAC role to be supplied where available and in preference to a local system role
- Updated [Access Record Design Decisions](accessrecord_design.html)
  - Improved wording to make more specific around Patient Record 'In-transit'
  - Corrected the reference to SCR timeframes 
  - Made more explicit the 'In-transit' record guidance
- Updated [Medications](accessrecord_view_medications.html)
  - Past Medications subsection to have consumer supplied date range applied
- Updated [Spine Security Proxy Implementation Guide](integration_spine_security_proxy_implementation_guide.html)
  - Step 6 in the Operating Principle table - Data-Sharing validation check - interim DSAR solution within SSP, strategic solution out of scope for FoT.


#### 1.0.0-rc.2 (Released: 6th December) 

- The elaboration of page(s) content to reflect the validation of data-sharing agreements by the Spine Security Proxy only, and the requirement that Provider Data-Sharing configuration should not be applied or changed for GP Connect interactions 
- The application of a configurable Legal Exclusion set - currently the RGCP set on TRUD -  which is being reviewed with amendments/changes expected Feb 2017
- The indication of withheld information, either arising from Patient preferences, or the application of the exclusion set to be at line item level as well as in Section Banner , as this provides more valuable information as to when and volume of exclusions
- Configurable Section Headings
- Configurable Section Default Date Ranges
- Section Content Messages for provider-specific description of how sections have been populated, or where content deviates from specification - eg Clinical/Administrative Items content; Problem 'Significance' values;  Patient withheld data indication;   see Section Pages
- Default section date range where relevant to be 'All' items, where Consumer date-range not supplied
- Section Heading Changes to: Current Repeat Medications, Problems and Issues, Allergies and Adverse Reactions
- Current Repeat Medications section - Last Issued Column to be first column in table
- Medication sections 'Drug' column heading to be 'Medication Item'
- Past Medications section - to include references to Discontinued Repeats, Cancelled Acutes, either as 'Type', or within Details column
- Investigations Section to be out of scope for Stage 1, pending further analysis
- Observations Section to include Investigation items
- Observations to be excluded from Clinical Items Section
- Medications Sections to be reviewed as part of Stage 2
- GP Name in Patient Banner (Details) to be the 'Usual' GP
  
#### 1.0.0-rc.1 (Released: September 2016)
- Beta version promoted to release candidate

#### 1.0.0-beta.1 (Release: August 2016)
- Initial release of the Access Record capability pack on GitHub in early August 2016.

#### 1.0.0-alpha.1 (Released: May 2016)
- Initial release for feedback/comments as part of the late May 2016 release. 
