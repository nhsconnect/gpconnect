---
title: Search examples
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_searchExamples.html
summary: "Introduction to search criteria in GP Connect"
---

## Search examples ##

We have developed a number of example searches that demonstrate the possible different ways a consumer may request data in GP Connect. These have been created in conjunction with our clinical team to demonstrate different ways of requesting similar data that we anticipate consumers are likely to require.

The different approaches to requests that will return similar information have been chosen here to demonstrate the filter constraints that we have imposed to mitigate the risk described here in the search criteria page **LINK TORISK DETAIL**



	1. Summary Care Record Standard - include allergies, include Meds with fromDate of 1 year ago

	2. Enhanced SCR query - Would be above plus problems. Return all problems and recommend  display group by active/inactive and major/minor.  In the current build this would bring back all the medications not just the last years  worth of Meds but all Meds. 
	It would be possible to do the standard summary care record query and then have a separate query for the problems. 

	3. Ability to request the last 3 consultations.

	4. Last 3 consultations with Problems, Meds and allergies. Two options
		a. If done in one query then all Meds would be returned.
		b. Can do a 2 part query for all (Meds and allergies) and (problems and last 3 consultations)

	5. Query for children - Enhanced SCR with vaccinations and observations
		a. If done in one query will get all meds and all obs
		b. If done in 2 queries will get last year of Meds, all allergies, Problems, Imms and Observations
		c. If done in 2 queries could have (last year Meds and Obs) and all allergies, Problems, Imms

  6. Query everything in last 3 months


