---
title: Search criteria
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_search.html
summary: "Introduction to search criteria in GP Connect"
---

## Search criteria ##

The consumer system can specify which clinical areas it wishes to retrieve and, within each clinical area, what search criteria it wants to apply.

### Medication and medical devices ###

* Search for all Medications and Medical Devices that were active on or after the specified date
  * The consumer system requests all items from a start date
  * The provider system returns all medication authorisations (MedicationStatement and MedicationRequest with intent set to 'plan') whose effective period end date is null or is on or after the start date
  * Where no date is supplied by the consumer, all medications and medical devices are returned
* Include all the prescriptions issued under the returned medication/medical device medication authorisations
  * The consumer system requests prescription issues
  * For each of the returned medication/medical device plans, the provider system includes data for all of its issues (MedicationStatement and MedicationRequest with intent set to 'plan').

### Allergies ###

* All active allergies will always be returned as it was considered clinically unsafe to only return a partial record of a patient's active allergies
* Include resolved allergies
  * The consumer system requests resolved allergies
  * The provider system returns all the resolved allergies along with the active allergies

### Problems ###

* Search for Problems with the specified combinations of significance and status
  * The consumer system requests combinations of significance and status
  * The consumer system can request Major Active, Minor Active, Major Inactive and/or Minor Inactive
  * The consumer system can request multiple combinations in a single query
  * The provider system returns all Problems that match the requested significance / status
  * Where no significance / status is supplied by the consumer, all Problems are returned

### Uncategorised data ###

* Search for all Uncategorised Data within the specified date range
  * The consumer system requests all items within a start and end date
  * The provider system returns all items whose effective date is within the start and end date (inclusive)
  * The provider system returns all items that have no effective date
  * Where no start date is supplied the search goes from the start of patient record
  * Where no end date is supplied the search goes to the end of patient record
  * Where no dates are supplied by the consumer, all uncategorised data items are returned

### Consultations ###

* Search for all Consultations within the specified date range
  * The consumer system requests all items within a start and end date
  * The provider system returns all items whose asserted date is within the start and end date (inclusive)
  * Where there is a start date but no end date, the search goes to the end of the patient record
  * Where there is an end date but no start date the search goes from the start of the patient record
* Search for the most recent x Consultations within the patient's record
  * The consumer system requests the last x consultations
  * The provider system returns the last x consultations
* Where a single filter is supplied by the consumer, it is applied as defined above
* The consumer **SHOULD NOT** include both filters, the provider **MUST NOT** return consultations and **MUST** return an error if both filters are included
* If no filters are supplied by the consumer, all Consultations are returned

### Immunisations ###

* All immunisations which have been given are always included.
* Include immunisations which were intended but were not given
  * The consumer requests immunisations which were not given
  * The provider returns all immunisation given and intended but not given
  * If no part parameters are included, the provider only returns given immunisations, related status and observations
* Include immunisation status and related observations
  * The consumer requests immunisation status records
  * The provider returns all immunisation given and consent and dissent observations
  * If no part parameters are included, the provider returns given immunisations, related status and observations

### Investigations ###

* Search for all Investigations within the specified date range
  * The consumer system requests all items within a start and end date
  * The provider system returns all items whose issued date is within the start and end date (inclusive)
  * Where there is a start date but no end date, the search goes to the end of the patient record
  * Where there is an end date but no start date, the search goes from the start of the patient record
  * Where no dates are supplied by the consumer, all investigations data items are returned

### Referrals ###

* Search for all Outbound Referrals within the specified date range
  * The consumer system requests all items within a start and end date
  * The provider system returns all items whose authoredOn date is within the start and end date (inclusive)
  * Where there is a start date but no end date, the search goes to the end of the patient record
  * Where there is an end date but no start date, the search goes from the start of the patient record
  * Where no dates are supplied by the consumer, all outbound referral data items are returned

### Diary entries ###

* Search for all Diary Entry data prior to a specified date
  * The consumer system requests all items prior to an end date
  * The provider system returns all items whose
    * occurrence period start date is on or prior to the consumer supplied end date or
    * occurrence date time is on or prior to the consumer supplied end date

### Full record

* This only applies to the migrate patient record interaction.
* Include all information from the patient's record
* where sensitive information has been requested, the provider system **MUST** return all information that would be included in a GP2GP record transfer.

## Following a linkage ##

For the majority of scenarios, the information required by the consumer can be retrieved through a single query. The consumer system identifies which clinical areas of the patient record it requires and which search criteria should be applied, then calls the GP Connect API. The provider system then returns all the requested information in a single bundle.

There are, however, scenarios where the information to the first query identifies additional information that is required.

For example:

* a retrieved medication is linked to a problem that the clinician wants to review
* a retrieved problem is linked to several consultations that the clinician wants to review
* a retrieved immunisation is linked to a consultation that the clinician wants to review

There may be a decision by the consuming system (or by a user of the consuming system) that they require additional information about the linked clinical item. To get these, the consumer system may wish to call the GP Connect API a second time.

This version of GP Connect does not allow a consumer to search for a specific item in the patient record by its identifier. Instead the consumer should use the supported filters to retrieve a larger dataset and then search for the required item(s) within that dataset.

For example:

* To display a specific consultation linked to a problem, the consumer system could request all the consultations that took place within the active period of the problem then search for the required consultation within the returned data.
