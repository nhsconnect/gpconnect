---
title: Multi area searches
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_searchMultiAreaSearches.html
summary: "Searching for multiple clinical areas"
---

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

## Searching for more than one clinical area ##

When searching for data for more than one clinical area there are several factors to consider,

 - Clincal safety
 - Information governance
 - Scale of search required
 - The volume and complexity of the data that may be returned
 
These factors are all related and finding the best approach for a consumers use case requires the developers/commisioners of the system to understand, prioritise and balance them. In doing so they will need to mitigate any clinical risks by using levers such as design, testing and end user training recording these in the clinical safety case and hazard log that they produce. 

There are resources on the GP Connect consumer test hub that are available in order support this proccess,

 - GP Connect stuctured test data records
 - test data definitions
 - a list of known clinical risks and possible mitigations 
 - guidance for clinical safety officers

[GP Connect consumer support hub](https://github.com/nhsconnect/gpc-consumer-support/wiki).

### Restrictions on query parameters when making searches ##

We have included some rules to limit which query part parameters can be used at the same time. These rules are documented on [the API page](accessrecord_structured_development_retrieve_patient_record.html#not-permitted-parameter-combinations). In addition to this predefined queries with details of their advantages, clinical risks and mitigations are included further down this page.

This is to mitigate the following risk.

#### Clinical risk when querying more than one clinical area ###

When requesting data for more than one clinical area at the same time and also using part parameters, e.g. medicationSearchFromDate, then it is important to be cautious when processing the results.
In this situation, it is possible that the different parts of the query will return items that may be misleading to a user of a consuming system.

Consider the example where a consuming system requests the medications from the last six months and all active problems. It is possible that one of the active problems links to a medication that is from longer than a year ago. The data held in the GP system is represented in the table below along with what the two parts of the query may contain.

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

In this situation, the medications returned by the two separate parts of the query may be misleading to a user of a consuming system. From the data in the table we can clearly see that the warfarin would not be returned by either part of the query. However, the paracetamol which is from before the warfarin was prescribed would be returned.
The clinical risk here is that a user of the consumer system may believe they have all the medications from the date of the 05/01/2019 when the paracetamol was prescribed but they are actually missing a medication that exists in the GP system but is older than 6 months but more recent than the medication returned that was linked to the problem.

#### Restrictions on parameters to mitigate the risk ###

In order to mitigate this risk and emphasise the separation of data in the different parts of certain queries, we have introduced rules around which filters can be used at the same time. For example, problem filters and medication date filters can't be used while requesting consultations. This will prevent data with these sorts of gaps being returned in a single bundle.

The technical details of these rules are detailed in the 'Not permitted parameter combinations' section of the [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html) page.

This data can still be requested with the same restrictions by using two calls and how this is done is detailed in the [Search examples](accessrecord_structured_development_searchExamples.html) page.

The search example above is shown as example number 2 on that page.

## Predefined searches multi area searches for common use cases

In order to help consuming systems manage the risk of multiple area searches and to help providers by minimising calls to the API and the volume of data returned we have decided to introduce some predefined searches.

These searches are exceptions to the rules that we have imposed on search parameters and will use combinations of filters that are not available to consumers when building their own searches. These have been created to reduce the burden on suppliers from an API and volume of data perspective while also giving us the opportunity to highlight the clinical risks that are present when these queries are used. 

This will mean we will provide the code needed to request these queries so consuming systems can pick up and use efficient queries that will pull back a set of data that they are likely to need in one call. While doing this it will be possible for us to highlight to them the precise risks involved in the query and offer advice to help them mitigate these risks.

As consumers build and use the API we will gather feedback about the queries we have defined and change or add to them as necessary. In time we may build a library of searches depending on the demand and how useful suppliers find them.

### Pre-defined search 1 - Last 3 consultations, last 1 years medications, allergies and problems

We have included this search as the last 3 consultations and problems are areas we have had feedback are the most in demand pieces of information after medications and allergies. It is intended to give a good picture of the patients recent GP record without having to return all the data for their medications.

#### Request

A skeleton request is included below consumers just need to insert the correct date and NHS number.

```json
{
"resourceType": "Parameters",
"parameter": [
	{
		"name": "patientNHSNumber",
		"valueIdentifier": {
			"system": "https://fhir.nhs.uk/Id/nhs-number",
			"value": "9999999999"
		}
	},
	{
		"name": "includeConsultations",
		"part": [
			{
				"name": "includeNumberOfMostRecent",
				"valueInteger": 3
			}
		]
	},
	{
		"name": "includeProblems"
	},
	{
		"name": "includeAllergies"
	},
	{
		"name": "includeMedication",
	        "part": [
			{
			  "name": "medicationSearchFromDate",
			  "valueDate": "today()-one year"
			}
	      ]
	}
    ]
}
```

### Pre-defined search 2 - Last 3 consultations, last 1 years medications, allergies, immunisations, problems and uncategorised data

This query covers all the same data returned in rep-defined search 1 with the addition of immunisations and uncategorised data. 

This search is intended to cover common use cases relating to peadiatric care where childhood vaccinations and observations may often be required.

#### Request

```json
{
  "resourceType": "Parameters",
  "parameter": [
    {
      "name": "patientNHSNumber",
      "valueIdentifier": {
        "system": "https://fhir.nhs.uk/Id/nhs-number",
        "value": "9999999999"
      }
    },
    {
	"name": "includeConsultations",
	"part": [
		{
			"name": "includeNumberOfMostRecent",
			"valueInteger": 3
		}
	]
    },
    {
      "name": "includeAllergies"
    },
    {
      "name": "includeMedication",
      "part": [
        {
          "name": "medicationSearchFromDate",
          "valueDate": "today()-one year"
        }
      ] 
    },
    {
      "name": "includeProblems"
    },
    {
      "name": "includeImmunisations"
    },
    {
      "name": "includeUncategorisedData"
    }
  ]
}
```
### Clinical risk

The clinical risks that are associated with these 2 queries are the same as the risk outlined above. 

It can occur if a medication either contained in a consultation or linked to a problem is returned that is more than a year old. 

### Mitigations

When processing data that is recieved consuming systems should exercise caution when processing medication data that is returned as part of a problem or consultation.

If additional medication data than that included in the primary medications list is returned by the query, for instance as a part of a problem or consultation. Then the consuming system **MUST** consider how this is processed and/or displayed to the user. 

 - It may be best to display the secondary list medication data separately to the medications returned in the main medications list. 
 - Consumers should consider if there are appropriate places to display prominent/disruptive warnings to their users to ensure that they are aware of any possible gaps in the data.
