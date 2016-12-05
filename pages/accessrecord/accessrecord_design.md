---
title: Access Record Design Decisions
keywords: getcarerecord design
tags: [design,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_design.html
summary: "Overview of the design decisions made in relation to the Access Record capability."
---

## GP Organisation Location ##

- <span class="label label-success">SELECTED</span> NHS Number must be used to resolve the ODS Code for the patient's usual GP.
- Other mechanism.

### Scope of HTML View ###

What is the scope of what views we're aiming to deliver?

- Initially a set of views covering the majority of the primary care record have been included based on workshops with Principal suppliers to agree how the data can be most sensible sectioned.
	- Some desirable headings such as Procedures, Diagnosis, Symptoms have been amalgamated into the 'Clinical Items' heading because the underlying data structure of the GP systems cannot reliably extract these coded elements.
- The scope of the views will be reviewed and added to as future version of the API are produced.

<sup>1</sup> Provider SHALL return minimal Patient resource(s).

<span class="label label-info">DECISION</span> Remove the structured clinical data from the bundle until [Stage 2.](designprinciples_maturity_model.html) engagement.

### Record In Transit ###

Their is a risk around their being an incomplete GP record if the patient's record is undergoing a transfer.

- <span class="label label-success">SELECTED</span> Provider some warning that the record could be incomplete.
- Other.

## HTML Sections ##

### Delivery Mechanism ###

- <span class="label label-success">SELECTED</span> Desktop
- Web
- Mobile

### Render Guidance ###

- <span class="label label-success">SELECTED</span> Reuse Common User Interface (CUI) Guidance
- Roll our own.

### Patient Trace Handling ###

- <span class="label label-success">SELECTED</span> Consumer and Provider to have traced in both
- Consumer only.
- Provider only.

#### Timeliness of Trace ####

- Immediately prior to all API calls.
- Once per user session.
- <span class="label label-success">SELECTED</span> Once per multiple user sessions (i.e. monthly<sup>1</sup> etc.)

<sup>1</sup> period of renewal/rechecking to be determined by commissioning organization.

### Patient Identity Cross Check ###

Although a traced national identifier is initially mandated for use with the GP Connect APIs, there are edge case scenarios where the the patient record being retrieved from the GP system may have different patient details than the source system. The basic Patient resource has been bundled into the response so that a cross check may be performed in the consuming system.
   
- <span class="label label-success">SELECTED</span> Consumer system to cross-check.
- Provider system to cross-check. 
- Spine Security Proxy (SSP) to cross-check.

<span class="label label-info">DECISION</span> As per GP SoC requirements make minimal registration details mandatory (i.e. First Name, Surname, Gender, DOB) in the FHIR profile.

#### Minimum Patient Demographics  ####

- <span class="label label-success">SELECTED</span> Patient Banner as defined in the CUI guidance.
- Community driven (i.e. just add Gender).
- Absolute minimum (Name, DOB and NHS Number).

<span class="label label-info">DECISION</span> Consumer SHALL cross-check with demographics returned from the Provider system.

### View Non-Retrieval ###

Potential grounds for not returning an HTML view:

- Technical constraints
	- Generation from structured FHIR&reg; resources
	- Can't safely retrieve from GP system
- Information Governance
	- Data Sharing Agreement not in place
	- Patient Dissent to record sharing
	
- PDS Status
	- Corrupt Record etc.

### Patient Consent ###

Patient Consent Preferences:

- <span class="label label-success">SELECTED</span> Patient consent enforced by the Provider system and cannot be overridden.
- Patient consent enforced by the Provider BUT can be overridden by Consumer.

### Patient Data Exclusions ###

<span class="label label-info">DECISION</span> Provider system SHALL enforce exclusion rules, either for the complete patient record, or sections/data-items.

These can be determined by two potential sets of exclusion settings:

- Manual exclusion (based on explicit patient preference).
	- <span class="label label-success">SELECTED</span> Provider system-based patient preferences.
	- SCR standard patient preferences (in addition).<sup>1</sup>
- Automatic exclusion (based on implied patient preference).<sup>2</sup>

<sup>1</sup> Providers are not initially expected to enforce SCR patient preferences in relation to returning API data. They SHALL only respect their own Principle patient preferences.

<sup>2</sup> Automatic or inferred exclusions are not supported as this would be technically impractical (i.e. it's not possible to filter out all free-text and other fields which could potentially contain data which should ideally be excluded).

### Legal Exclusion Sets ###

<span class="label label-info">DECISION</span> Provider API processing SHALL support the application of an exclusion set, which SHALL be configurable, including containing Null values.  The current RGCP Legal Exclusion Set SHALL be applied for Stage 1 FoT, for the complete patient record, or sections/data-items, but is likely to to amended pending the results of the current national review, expected February 2017 to be approved by the Joint GP IT Committee (JGPIT).
https://isd.hscic.gov.uk/trud3/user/guest/group/0/pack/9/subpack/97/releases;jsessionid=AB048FD7361740B3D3EB628337C188D5


### Data Sharing Agreements ###

- Data-Sharing Agreement must be in place between the consuming organisation and the providing organisation
- The Spine Security Proxy validates this requirement, therefore Provider Systems SHALL NOT apply or change locally-configured Data-Sharing validation

#### Exclusion Warnings ####

- No indication that data has been excluded.
- <span class="label label-success">SELECTED</span> Warning indication per section that data has been excluded (within the time frame).
- <span class="label label-success">SELECTED</span> In line with some information related to the data item.
	- i.e. encounter date/time but not the place or encounter details.

<span class="label label-info">DECISION</span> Warning needed that data supplied for a patient may be incomplete/withheld either due to patient preferences or as a result of the application of the Legal Exclusion set - to be displayed both within the Section Banner as well as at line item level.

#### SCR Consent Model ####

{% include roadmap.html content="Could potentially be brought into scope for Stage 2 or 3." %}

SCR model (between Consumer and Provider's who have an existing Data Sharing Agreement in place).

- No explicit consent (implied consent).
	- Core Data Set (Allergies, Adverse Reactions and Medications).
- Given explicit consent.
	- Diagnosis, Immunisations, Problems, Procedures and End of Life Preferences.
- Explicit consent needed (exclusion set).
	- Sexually Transmitted Infections, Terminations, Gender Reassignment.

### Section-by-section Time Frames for data ###

#### Summary Time Frames ####

Date range handling in the summary per section:

 - No date range due to clinical safety.
 - <span class="label label-success">SELECTED</span> Date range to match workshop agreements.
	 - Current XYZ (what does it mean for each section)
	 - Last 3 Months Recent Investigations.
	 - Last 3 Encounters
	 - etc.
 - Date range to match SCR time-frames for all sub sections.

#### Section Time Frames ####

Date range handling in the HTML view per section:

- No date range, return all data always for all sections.
- Fixed date ranges for sections.
- <span class="label label-success">SELECTED</span> Default date ranges to match SCR time-frames per section (e.g. always return all allergies) with clinical sign off.

#### HTML Section Ordering ####

<span class="label label-info">DECISION</span> Consumer systems SHALL provide access to record sections in the order agreed in the workshops, which is captured in the ordering of the HTML Composition sections with-in the FHIR `gpconnect-carerecord-composition-1` data model.

### Per Section Minimum Free Text For Display ###

{% include todo.html content="Free-text population guidance details to be added in [Stage 2.](designprinciples_maturity_model.html)" %}

Providers SHALL populate the free-text details field as follows:

| Section Code | Section Name | Mandatory Data Items | 
| ------------ | ------------ | -------------------- |
| ENC | Encounters | - |
| CLI | Clinical Items | - |
| ADM | Administrative Items | - |
| REF | Referrals | - |
| IMM | Immunisations | - |
| PRB | Problems | - |
| MED | Medications | - |
| OBS | Observations | - |
| INV | Investigations | - |
| ALL | Allergies and Sensitivities | - |

## Operation Definition ##

### Requesting A Section ###

- [0..N] Return a variety of views.
- [0..1] Return everything vs. Return summary.
- <span class="label label-info">SELECTED</span> [1] Only return a single section at a time.

- <span class="label label-info">DECISION</span> The ability to return multiple or all HTML care record sections in one request will not be provided.
