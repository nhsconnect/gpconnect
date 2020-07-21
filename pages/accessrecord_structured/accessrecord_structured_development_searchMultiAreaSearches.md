---
title: Multi area searches
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_searchMultiAreaSearches.html
summary: "Searching for multiple clinical areas"
---

## Searching for more than one clinical area ##

When searching for data for more than one clinical area there are a number of factors to consider,

 - Clincal safety
 - Information governance
 - Scale of search required
 - The volume and complexity of the data that may be returned
 
These factors are all to some extent related and finding the approach that best suits a consumers use case will require the developers of the system to understand, prioritise and balance them. As they do this they will need to mitigate any clinical risks by using levers such as design, testing and end user training. 

There are resources on the GP Connect consumer test hub including how to access GP Connect test data and definitions and the consumer version of the GP Connect Hazard log. 

****Insert consumer hub link here****

In addition to this predefined queries with details of their advantages, clinical risks and mitigations are included further down this page.

## Restrictions on query parameters when making searches ##

We have included some rules to limit which query part parameters can be used at the same time. These rules are documented on [the API page](accessrecord_structured_development_retrieve_patient_record.html#not-permitted-parameter-combinations).

This is to mitigate the following risk.

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

In order to mitigate this risk and emphasise the separation of data in the different parts of certain queries, we have introduced some rules around which filters can be used at the same time. For example, problem filters and medication date filters can't be used while requesting consultations. This will prevent data with these sorts of gaps being returned in a single bundle.

The technical details of these rules are detailed in the 'Not permitted parameter combinations' section of the [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html) page.

This data can still be requested with the same restrictions by using two calls and how this is done is detailed in the [Search examples](accessrecord_structured_development_searchExamples.html) page.
The search example relevant to the example given here is number 2 on the page where it details two different ways that you could query for the data.

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

## Predefined searches multi area searches for common use cases

In order to help consuming systems manage the risk of multiple area searches and to help providers by minimising calls to the API and the volume of data returned we have decided to introduce some predefined searches.

These searches break some of the rules that we have imposed on our search parameters and will use combinations of filters that are not available to consumers when building their own searches. The reason we have decided to do this is to try and reduce the burden on suppliers from an API and volume of data perspective while also giving us the opportunity to highlight the clinical risks that are present when these queries are used. 

This will mean we will provide the code needed to request these queries so consuming systems can pick up and use effiecent queries that will pull back all the data they are likely to need in one call. While doing this it will be possible for us to highlight to them the precise risks involved in the query and offer advice to help them mitigate these risks.

Currently we have defined 2 queries that we believe will be the most useful. As consumers begin build to and use the API we will look to gather feedback about the queries we have defined and either change or add to them as necessary. In time it may be that we build a library of searches for consumers to pick from but it will depend on the demand and how useful suppliers find them.

### Last 3 consultations, last 1 years medications, allergies and problems

Description and advantages, possible use cases

#### Request

The request would be similar to the below but with the correct date and NHS number.

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
		"name": "includeAllergies",
	},
	{
		"name": "includeMedication"
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

#### Clinical risk

#### Mitigations

### Last 3 consultations, last 1 years medications, allergies, immunisations, problems and uncategorised data
Description and advantages, possible use cases

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
      "name": "includeAllergies",
      "part": [
        {
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeMedication"
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

#### Clinical risk

#### Mitigations
