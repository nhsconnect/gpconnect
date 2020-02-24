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
     * The provider system returns all plans whose effective period end date is null or is on or after the start date
     * Where no date is supplied by the consumer, all medications and medical devices are returned
* Include all the prescriptions issued under the returned medication/medical device plans
     * The consumer system requests prescription issues
     * For each of the returned medication/medical device plans, the provider system includes data for all of its issues

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

* All Immunisations will always be returned.

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

## Scale of search ##

It is the responsibility of the consuming system to decide what data to request from the provider systems. When determining how wide to make the search criteria, the consumer system must consider the following guidelines:

* Always apply the [Caldicott Principles](https://www.igt.hscic.gov.uk/Caldicott2Principles.aspx) 
* The first API query on a patient should aim to retrieve the amount of data required to support the majority of queries that their clinician/user will make whilst avoiding the retrieval of large quantities of unnecessary data
* Where a follow-up query is required it should aim to retrieve sufficient data to support any other queries that their clinician/user will make
* The consumer system should aim to avoid scenarios where more than two queries are required on the same patient as part of the same local interaction with a clinician/user. This does NOT preclude the consumer system from making further queries where necessary to support patient care.
* It is acceptable for the consumer system to request and retrieve a large proportion of the patient's record from the provider system and filter out the unnecessary data before presenting it to their clinicians/users where the consumer organisation: 
     * has determined it is necessary to support patient care
     * has met all of the GP Connect information governance (IG) requirements including data sharing agreements, confidentiality and auditing

The details on how this is implemented in an API can be found in the [API definition](accessrecord_structured_development_retrieve_patient_record.html).
<a name="clinicalrisk"></a>


## Restrictions on query parameters when making searches ##

We have introduced some rules to limit which query parameters can be used at the same time. This is to mitigate 
the following risk.

### Clinical risk when querying more than one clinical area ###

When requesting data for more than one clinical area at the same time and also using filters - for example, the medicationSearchFromDate, then it is important to be cautious when processing the results. 
In this situation, it is possible that the different parts of the query will return items that may be misleading to a user of a consuming system.

Consider the example where a consuming system requests the medications from the last six months and all active problems. It is possible that one of the active problems links to a medication that is from longer than a year ago. In this case, there is a risk that the consuming system may present the data to the user in a way that may lead them to believe they have the entire medication record from over a year ago until the current time. In the table below there is a summary of how the data from the example may exist in the GP system and what the two parts of the query may contain.

For the example we will assume the query was made on the 1st February 2020:

<table class='resource-attributes' border='1'>
  <tr>
    <td>Date</td>
    <td>Medications in the GP system</td>
    <td>Included in medications query return</td>
    <td>Included in problems query return</td>
  </tr>
  <tr>
    <td>03/01/2020</td>
    <td>Paracetamol</td>
    <td>Y</td>
    <td></td>
  </tr>
  <tr>
    <td>05/12/2019</td>
    <td>Ibuprofen</td>
    <td>Y</td>
    <td></td>
  </tr>
  <tr>
    <td>12/11/2019</td>
    <td>Amoxicillin</td>
    <td>Y</td>
    <td></td>
  </tr>
  <tr style="background-color:Orange">
    <td>01/04/2019</td>
    <td>Warfarin</td>
    <td></td>
    <td></td>
  </tr> 
  <tr>
    <td>05/01/2019</td>
    <td>Paracetamol</td>
    <td></td>
    <td>Y</td>
  </tr>
</table>

From the data in the table we can clearly see that the warfarin would not be returned by either part of the query. However, the paracetamol which is from before the warfarin was prescribed would be returned.
The clinical risk here is that a user of the consumer system may believe they have all the medications from the date of the 05/01/2019 when the paracetamol was prescribed but they are actually missing a medication that exists in the GP system but is older than 6 months but more recent than the medication returned that was linked to a problem.

### Restrictions on parameters to mitigate the risk ###

In order to mitigate this risk and emphasise the separation of data in the different parts of certain queries, we have introduced some rules around which filters can be used at the same time. This will prevent data with these sorts of gaps being returned in a single bundle.

The technical details of these rules are detailed in the 'Not permitted parameter combinations' section of the [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html) page.

These can be summarised by the following two rules:

1. When requesting consultations, problem filters, medication date filter or uncategorised date filter **MUST NOT** be used.
2. When requesting problems, date filters for medications and uncategorised data **MUST NOT** be used.

This data can still be requested with the same restrictions by using two calls and how this is done is detailed in the [Search examples](accessrecord_structured_development_searchexamples.html) page.
The search example relevant to the example given here is number 2 on the page where it details two different ways that you could query for the data.

