---
title: Access Record HTML design decisions
keywords: getcarerecord design
tags: [design,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_design.html
summary: "Overview of the design decisions made in relation to the Access Record capability"
---

## GP organisation location ##

- <span class="label label-success">SELECTED</span> NHS Number must be used to resolve the ODS code for the patient's usual GP.
- Other mechanism.

### Scope of HTML view ###

What is the scope of what views we're aiming to deliver?

- Initially a set of views covering the majority of the primary care record have been included based on workshops with principal suppliers to agree how the data can be most sensible sectioned.
	- Some desirable headings such as Procedures, Diagnosis, Symptoms have been amalgamated into the 'Clinical Items' heading because the underlying data structure of the GP systems cannot reliably extract these coded elements.
- The scope of the views will be reviewed and added to as future versions of the API are produced.

<sup>1</sup> Provider **SHALL** return minimal patient resource(s).

<span class="label label-info">DECISION</span> Remove the structured clinical data from the bundle until Access Record Structured delivery.

## HTML sections ##

### Delivery mechanism ###

- <span class="label label-success">SELECTED</span> Desktop
- Web
- Mobile

### Render guidance ###

- <span class="label label-success">SELECTED</span> Reuse Common User Interface (CUI) Guidance
- Define our own.

### Patient trace handling ###

- <span class="label label-success">SELECTED</span> Consumer and provider to have traced in both.
- Consumer only.
- Provider only.

#### Timeliness of trace ####

- Immediately prior to all API calls.
- Once per user session.
- <span class="label label-success">SELECTED</span> Once per multiple user sessions (for example, monthly<sup>1</sup>, and so on.)

<sup>1</sup> period of renewal/rechecking to be determined by commissioning organization.

### Patient identity cross check ###

Although a traced national identifier is initially mandated for use with the GP Connect APIs, there are edge case scenarios where the patient record being retrieved from the GP system may have different patient details than the source system. The basic patient resource has been bundled into the response so that a cross check may be performed in the consuming system.
   
- <span class="label label-success">SELECTED</span> Consumer system to cross-check.
- Provider system to cross-check. 
- Spine Security Proxy (SSP) to cross-check.

<span class="label label-info">DECISION</span> As per GPSoC requirements make minimal registration details mandatory (for example, First Name, Surname, Gender, DOB) in the FHIR profile.

#### Minimum patient demographics  ####

- <span class="label label-success">SELECTED</span> Patient banner as defined in the CUI guidance.
- Community driven (that is, just add Gender).
- Absolute minimum (Name, DOB and NHS Number).

<span class="label label-info">DECISION</span> Consumer **SHALL** cross-check with demographics returned from the provider system.

### View non-retrieval ###

Potential grounds for not returning an HTML view:

- Technical constraints
	- Generation from structured FHIR&reg; resources
	- Can't safely retrieve from GP system
- Information governance
	- Data sharing agreement not in place
	- Patient dissent to record sharing
	
- PDS status
	- Corrupt record, etc.

### Record locking ###

Behaviour when Access Record query/request received while patient record being updated in provider system:

- <span class="label label-success">SELECTED</span> Return the requested record section, only including data that has been successfully committed to the database and is available to all users.  [As agreed in workshops]
- Return error message in lieu of record section. 
- Return snapshot of record as-is at the time of request including any non-committed changes.

### Patient consent ###

Patient consent preferences:

- <span class="label label-success">SELECTED</span> Patient consent enforced by the provider system and cannot be overridden.
- Patient consent enforced by the provider but can be overridden by consumer.

### Patient data exclusions ###

<span class="label label-info">DECISION</span> Provider system **SHALL** enforce exclusion rules, either for the complete patient record, or sections/data-items.

These can be determined by two potential sets of exclusion settings:

- Manual exclusion (based on explicit patient preference).
	- <span class="label label-success">SELECTED</span> Provider system-based patient preferences.
	- Summary Care Record (SCR) standard patient preferences (in addition).<sup>1</sup>
- Automatic exclusion (based on implied patient preference).<sup>2</sup>

<sup>1</sup> Providers are not initially expected to enforce SCR patient preferences in relation to returning API data. They **SHALL** only respect their own principal patient preferences.

<sup>2</sup> Automatic or inferred exclusions are not supported as this would be technically impractical (it's not possible to filter out all free-text and other fields which could potentially contain data which should ideally be excluded).

### 'Confidential' (GP practice-designated) data exclusions ###

<span class="label label-info">DECISION</span> Provider system **SHALL** enforce exclusion rules, either for the complete patient record, or sections/data-items.

Items designated by the practice as confidential **SHALL NOT** be provided, and processed in the same way as patient data exclusions.


### Sensitive data exclusion set ###

<span class="label label-info">DECISION</span> Provider API processing **SHALL** support the application of an exclusion set, which **SHALL** be configurable, including containing null values.  The current Royal College of General Practitioners (RCGP) sensitive exclusion set **SHALL** be applied for Stage 1 First of Type (FoT), for the complete patient record, or sections/data-items, but is likely to amended pending the results of the current national review, expected February 2017 to be approved by the Joint GP IT Committee (JGPIT).
<br>[GP summary exclusion code Lists](https://isd.hscic.gov.uk/trud3/user/guest/group/0/pack/1/subpack/141/releases)

{% include note.html content="You will need to register for an account on TRUD (the NHS Terminology Reference Data Update Distribution Service) in order to view the above link." %}


### Data sharing agreements ###

- Data-sharing agreement must be in place between the consuming organisation and the providing organisation.
- The Spine Security Proxy validates this requirement. Therefore, provider systems **SHALL NOT** apply or change locally-configured data-sharing validation.

### Exclusion warnings ###

- No indication that data has been excluded.
- <span class="label label-success">SELECTED</span> Warning indication per section that data has been excluded (within the time frame).
- <span class="label label-success">SELECTED</span> In line with some information related to the data item.
	- that is, encounter date/time but not the place or encounter details.

<span class="label label-info">DECISION</span> Warning needed that data supplied for a patient may be incomplete/withheld due to patient preferences, GP practice designation of 'Confidential' or as a result of the application of the sensitive exclusion set - to be displayed both within the section banner as well as at line item level.

### Record 'In-transit' as a result of GP transfer ###

If the patient's record is indicated in the provider system as not fully-integrated following a GP to GP transfer, then only data which has been entered to the current GP record should be returned, and NOT the contents of the previous GP record. Where data is excluded according to this, a warning should be included in the section banner indicating that some data has been excluded as a result of the transfer.    

- <span class="label label-success">SELECTED</span> Provider to supply a warning that the record could be incomplete.
- Other.


### Section-by-section time frames for data ###

#### Summary time frames ####

Date range handling in the summary per section:

 - No date range due to clinical safety.
 - <span class="label label-success">SELECTED</span> Date range to match workshop agreements.
	 - Current XYZ (what does it mean for each section)
	 - Last 3 Encounters
	 - etc.
 - Date range to match SCR time-frames for all subsections.

#### Section time frames ####

Date range handling in the HTML view per section:

- No date range, return all data always for all sections.
- Fixed date ranges for sections.
- <span class="label label-success">SELECTED</span> Date ranges to be applied as indicated in the relevant section implementation guidance (for example, always return all allergies) with clinical sign off.

#### HTML section ordering ####

<span class="label label-info">DECISION</span> Consumer systems **SHALL** provide access to record sections in the order agreed in the workshops, which is captured in the ordering of the HTML composition sections with-in the FHIR `gpconnect-carerecord-composition-1` data model.

### Per section minimum free text for display ###

Providers **SHALL** populate the free-text details field as follows:

| Section code | Section name | Mandatory data items | 
| ------------ | ------------ | -------------------- |
| ENC | Encounters | - |
| CLI | Clinical Items | - |
| ADM | Administrative Items | - |
| REF | Referrals | - |
| IMM | Immunisations | - |
| PRB | Problems | - |
| MED | Medications | - |
| OBS | Observations | - |
| ALL | Allergies and Sensitivities | - |

## Operation definition ##

### Requesting a section ###

- [0..N] Return a variety of views.
- [0..1] Return everything vs. Return summary.
- <span class="label label-info">SELECTED</span> [1] Only return a single section at a time.

- <span class="label label-info">DECISION</span> The ability to return multiple or all HTML care record sections in one request will not be provided.
