---
title: Design decisions
keywords: getcarerecord design
tags: [design,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_design.html
summary: "Overview of the design decisions made in relation to the Access Record capability"
---

<a href="#" class="back-to-top">Back to Top</a>

## Scope ##

### Scope of HTML view ###

What is the scope of what views we're aiming to deliver?

- <span class="label label-info">DECISION</span> initially a set of views covering the majority of the primary care record have been included based on workshops with principal suppliers to agree how the data can be most sensible sectioned <br/>
	- some desirable headings such as Procedures, Diagnosis, Symptoms have been amalgamated into the 'Clinical Items' heading because the underlying data structure of the GP systems cannot reliably extract these coded elements <br/>
- <span class="label label-info">DECISION</span> the scope of the views will be reviewed and added to as future versions of the API are produced <br/>
- <span class="label label-info">DECISION</span> provider **MUST** return minimal patient resource(s) <br/>
- <span class="label label-info">DECISION</span> remove the structured clinical data from the bundle until Access Record Structured delivery


### View non-retrieval ###

Potential grounds for not returning an HTML view?

- <span class="label label-info">DECISION</span> technical constraints
	- generation from structured FHIR&reg; resources
	- can't safely retrieve from GP system
- <span class="label label-info">DECISION</span> information governance
	- data sharing agreement not in place
	- patient dissent to record sharing
- <span class="label label-info">DECISION</span> PDS status
	- corrupt record, etc.


## General ##

### Record 'In-transit' as a result of GP transfer ###

If the patient's record is indicated in the provider system as not fully-integrated following a GP to GP transfer, then only data which has been entered to the current GP record should be returned, and NOT the contents of the previous GP record. Where data is excluded according to this, a warning should be included in the section banner indicating that some data has been excluded as a result of the transfer.    

- <span class="label label-success">SELECTED</span> provider to supply a warning that the record could be incomplete
- other

<span class="label label-info">DECISION</span> The provider **MUST** display a banner message when a record is in-transit.

### Deceased patient's record ###

Behaviour when a deceased patient's record is requested:

- <span class="label label-info">DECISION</span> The provider **MUST** allow access to a deceased patient's record for a period of 28 days after the patient's death. The provider **MUST** allow for the period to be configurable. If the request is made after this period, provider **MUST** return an error.
- <span class="label label-info">DECISION</span> The provider **MUST** return a deceased patient's record only if the patient was a main GMS registered patient prior to being de-registered due to death.

### Record locking ###

Behaviour when Access Record query/request received while patient record being updated in provider system:

- <span class="label label-success">SELECTED</span> return the requested record section, only including data that has been successfully committed to the database and is available to all users
- return error message in lieu of record section.
- return snapshot of record as-is at the time of request including any non-committed changes

<span class="label label-info">DECISION</span> The provider **MUST** return the most recently committed record for the patient.

### Requesting a section ###

How can the HTML sections be requested?

- [0..N] return a variety of views
- [0..1] return everything vs. Return summary
- <span class="label label-success">SELECTED</span> [1] only return a single section at a time

<span class="label label-info">DECISION</span> The ability to return multiple or all HTML care record sections in one request will not be provided.

#### HTML section ordering ####

How should the HTML sections be ordered?

<span class="label label-info">DECISION</span> Consumer systems **MUST** provide access to record sections in the order specified, which is captured in the ordering of the HTML composition sections with-in the FHIR `gpconnect-carerecord-composition-1` data model.



## User Interface ##

### Platform support ###

Which platforms will be supported?

- <span class="label label-success">SELECTED</span> desktop
- <span class="label label-success">SELECTED</span> web
- mobile

<span class="label label-info">DECISION</span> Mobile platforms will not be supported.

### Render guidance ###

What UI guidance should be followed?

- <span class="label label-success">SELECTED</span> reuse Common User Interface (CUI) Guidance
- define our own

<span class="label label-info">DECISION</span> The CUI guidance supported by the NHS will be followed.


## Patient tracing and verification ##

### GP organisation location ###

How will the patient's usual GP practice be identified?

- <span class="label label-success">SELECTED</span> NHS Number **MUST BE** be used to resolve the ODS code for the patient's usual GP
- other mechanism

<span class="label label-info">DECISION</span> The patient's NHS Number **MUST BE** used to identify their associated ODS code.

### Patient trace handling ###

Is the consumer or provider responsible for running a trace?

- <span class="label label-success">SELECTED</span> ideally the consumer and provider to have traced in both
- consumer only
- provider only

<span class="label label-info">DECISION</span> Consumers **MUST** perform a trace.

#### Timeliness of trace for consumers ####

How often should the trace be run by consumers?

- immediately prior to all API calls
- once per user session
- once per multiple user sessions (meaning, monthly etc.)
- <span class="label label-success">SELECTED</span> within the last 24 hours

<span class="label label-info">DECISION</span> The trace **MUST** have be performed within the last 24 hours.

### Patient identity cross check ###

Although a traced national identifier is initially mandated for use with the GP Connect APIs, there are edge case scenarios where the patient record being retrieved from the GP system may have different patient details than the source system. The basic patient resource has been bundled into the response so that a cross check may be performed in the consuming system.

- <span class="label label-success">SELECTED</span> consumer system to cross-check
- provider system to cross-check
- Spine Security Proxy (SSP) to cross-check

<span class="label label-info">DECISION</span> Consumer **MUST** cross-check with demographics returned from the provider system.

#### Minimum patient demographics  ####

What are the minimum patient demographics that must be returned?

- <span class="label label-success">SELECTED</span> patient banner as defined in the CUI guidance
- community driven (that is, just add Gender)
- absolute minimum (Name, DOB and NHS Number)

<span class="label label-info">DECISION</span> As per GPSoC requirements make minimal registration details mandatory (meaning, First Name, Surname, Gender, DOB) in the FHIR profile.


## Consent and exclusions ##

### Patient consent ###

How are patient consent preferences dealt with?

- <span class="label label-success">SELECTED</span> patient consent enforced by the provider system and cannot be overridden
- patient consent enforced by the provider but can be overridden by consumer

<span class="label label-info">DECISION</span> Patient consent enforced by the provider system **MUST** be adhered to when returning a patient record.


### Patient data exclusions ###

What patient data exclusions are associated with Access Record HTML?

These can be determined by two potential sets of exclusion settings:

- manual exclusion (based on explicit patient preference)
	- <span class="label label-success">SELECTED</span> provider system-based patient preferences
	- Summary Care Record (SCR) standard patient preferences (in addition) <sup>1</sup>
- automatic exclusion (based on implied patient preference) <sup>2</sup>

<sup>1</sup> Providers are not initially expected to enforce SCR patient preferences in relation to returning API data. They **MUST** only respect their own principal patient preferences.

<sup>2</sup> Automatic or inferred exclusions are not supported as this would be technically impractical (it's not possible to filter out all free-text and other fields which could potentially contain data which should ideally be excluded).

<span class="label label-info">DECISION</span> Provider system **MUST** enforce exclusion rules, either for the complete patient record, or sections/data-items.

### 'Confidential' (GP practice-designated) data exclusions ###

How are 'confidential' data items dealt with?

- <span class="label label-info">DECISION</span> provider system **MUST** enforce exclusion rules, either for the complete patient record, or sections/data-items
- <span class="label label-info">DECISION</span> items designated by the practice as confidential **MUST NOT** be provided, and processed in the same way as patient data exclusions


### Sensitive data exclusion set ###

How are sensitive data items dealt with?

<span class="label label-info">DECISION</span> Provider API processing **MUST** support the application of an exclusion set, which **MUST** be configurable, including containing null values. The current Royal College of General Practitioners (RCGP) sensitive exclusion set **MUST** be applied, for the complete patient record, or sections/data-items, but is likely to amended pending future guidance and review (to be approved by the Joint GP IT Committee (JGPIT)).
<br>[GP summary exclusion code Lists](https://isd.hscic.gov.uk/trud3/user/guest/group/0/pack/1/subpack/141/releases)

{% include custominfocallout.html content="**Information:** You will need to register for an account on TRUD (the NHS Terminology Reference Data Update Distribution Service) in order to view the above link." type="info" %}


### Data sharing agreements ###

What data sharing agreements need to be in place?

- <span class="label label-info">DECISION</span> data-sharing agreement must be in place between the consuming organisation and the providing organisation
- <span class="label label-info">DECISION</span> the Spine Security Proxy validates this requirement

Therefore, provider systems **MUST NOT** apply or change locally-configured data-sharing validation.

### Exclusion warnings ###

How are exclusion warnings identified within Access Record HTML?

- no indication that data has been excluded
- <span class="label label-success">SELECTED</span> warning indication per section that data has been excluded (within the time frame)
- <span class="label label-success">SELECTED</span> in line with some information related to the data item
	- that is, encounter date/time but not the place or encounter details

<span class="label label-info">DECISION</span> Warning needed that data supplied for a patient may be incomplete/withheld due to patient preferences, GP practice designation of 'Confidential' or as a result of the application of the sensitive exclusion set - to be displayed both within the section banner as well as at line item level.


## Date handling ##

### Summary time frames ###

Date range handling in the summary per section:

 - <span class="label label-success">SELECTED</span> no date range due to clinical safety
 - date range to match requirements identified on each HTML view page
	 - Active problems and issues
	 - Current medications issues
	 - Last 3 encounters
	 - etc.
 - date range to match SCR time-frames for all subsections

<span class="label label-info">DECISION</span> No date ranges are applied to the summary section.

### Section time frames ###

Date range handling in the HTML view per section:

- no date range, return all data always for all sections
- fixed date ranges for sections
- <span class="label label-success">SELECTED</span> date ranges to be applied as indicated in the relevant section implementation guidance (for example, always return all allergies) with clinical sign off

<span class="label label-info">DECISION</span> Date ranges are applied, where permitted, throughout Access Record HTML, please see each HTML view page for details.
