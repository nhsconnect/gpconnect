---
title: Linkages and Search
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_linkages.html
summary: "Introduction to linkages between data items in GP Connect"
---
## Linkages ##
The purpose in developing the FHIR&reg; profiles is to ensure that clinical data is, as much as possible, presented the same way regardless of the provider system. This ensures the consuming system (and clinician) will always know where to look for each type of information.

However, information about the patient is not just held within the profiles but in how those profiles are linked together. 

For example, linking a medication to a problem means that as well as the record showing what the patient is taking, it also explains why they are taking it.

For a consuming system to be able to interpret this linkage information correctly, it needs to be presented in the same way regardless of the providing system.

### GP Connect FHIR&reg; model ###
To support this, GP Connect has developed a FHIR model that identifies all the GP Connect FHIR profiles and how they are related together to store the patient record.

The model currently covers consultations, problems, medications and medical devices, allergies, immunisations and uncategorised data. Other clinical areas will be added as they are developed.

<img src="images/access_structured/GP_Connect_FHIR_Model.png" alt="GP Connect FHIR Model" style="max-width:100%;max-height:100%;">

The relationships between two FHIR resources are defined in only one of the linked FHIR resources (similar to in a relational database management system (RDBMS). This is shown by the direction of the arrow in the FHIR model. 

For example, the MedicationStatement resource contains a field that can be used to look up the linked medication. There is no field in the Medication resource that can be used to look up the linked MedicationStatement.

## FHIR profiles returned on query ##
There are three main considerations when determining which data is returned by a query on each clinical area:
* include all the FHIR profiles required to fully describe the requested clinical area
* include the FHIR profiles required to define all the linkages from the requested clinical area
* include the FHIR profiles from linked clinical areas where they are key to understanding the requested clinical area 

### Consultations ###
When GP Connect returns a consultation it will supply the metadata of the consultation and all the clinical data that was recorded during the consultation.

Include the following FHIR profiles:
* the Encounter profile of the consultation
*	the List profiles of the consultation
*	the ProblemHeader profile of any directly linked Problems
*	the MedicationRequest, MedicationStatement and Medication profiles of any linked Medications or Medical Devices
    * Always include the MedicationStatement, MedicationRequest (intent = plan) and Medication profiles
    * Only include MedicationRequest (intent = order) for directly linked issues
    *	Include the ProblemHeader profile of any Problems linked to the returned MedicationRequests
*	the AllergyIntolerance profile of any linked Allergies
    *	Include the ProblemHeader profile of any Problems linked to the returned Allergies
*	the Immunization profile of any linked Immunisations
    *	Include the ProblemHeader profile of any Problems linked to the returned Immunisations
*	the Observation profile of any linked Uncategorised Data
    *	Include the ProblemHeader profile of any Problems linked to the returned Uncategorised Data

<img src="images/access_structured/Consultation_Return.png" alt="Consultation Returned FHIR profiles" style="max-width:100%;max-height:100%;">

### Problems ###
When GP Connect returns a problem it will supply the metadata and description of the problem and all the clinical data that has been linked to the problem.

Include the following FHIR profiles:
*	The ProblemHeader profile of the Problem
*	The ProblemHeader profiles of any directly linked Problems
*	The MedicationRequest, MedicationStatement and Medication profiles of any linked Medications or Medical Devices.
    *	Always include the MedicationStatement, MedicationRequest (intent = plan) and Medication profiles.
    *	Only include MedicationRequest (intent = order) for directly linked issues.
*	The AllergyIntolerance profile of any linked Allergies
    *	Include the ProblemHeader profile of any Problems linked to the returned Allergies
*	The Immunization profile of any linked Immunisations
    *	Include the ProblemHeader profile of any Problems linked to the returned Immunisations
*	The Observation profile of any linked Uncategorised Data
    *	Include the ProblemHeader profile of any Problems linked to the returned Uncategorised Data
    
<img src="images/access_structured/Problem_Return.png" alt="Problem Returned FHIR profiles" style="max-width:100%;max-height:100%;">

### Medications and medical devices ###
When GP Connect returns a medication or medical device it will supply the prescription plan information. If asked for by the consumer, GP Connect will also return all the prescription issues made under the plan.

Include the following FHIR profiles:
*	The MedicationRequest (intent = plan), MedicationStatement and Medication profiles of the Medication and Medical Device
*	The ProblemHeader profiles of any directly linked Problems
*	Where requested, the MedicationRequest (intent = order) profile for every issue.

### Allergies ###
When GP Connect returns an allergy it will supply all the allergy data.

Include the following FHIR profiles:
*	The AllergyIntolerance profile of the Allergy
*	The ProblemHeader profiles of any directly linked Problems

### Immunisation ###
When GP Connect returns an immunisation it will supply all the immunisation data.

Include the following FHIR profiles:
*	The Immunization profile of the Immunisation
*	The ProblemHeader profiles of any directly linked Problems

### Uncategorised data ###
When GP Connect returns uncategorised data it will supply all the data about the uncategorised data.

Include the following FHIR profiles:
*	The Observation profile of the Uncategorised Data
*	The ProblemHeader profiles of any directly linked Problems

## Search ##

The GP Connect API allows the consumer system to specify what data it requires from the provider system about a specified patient.

### Search Criteria ###

The consumer system can specify which clinical areas it wishes to retrieve and within each clinical area what search criteria it wants to apply.

#### Medication and Medical Devices ####

* Search by date
     * The consumer system request all items after a start date
     * The provider system returns all plans whose effective period end date is null or after the start date
     * Where no date is supplied by the consumer, the date filter is not applied
* Include issues
     * The consumer system requests medication issues
     * The provider system returns the all issues information for each of the returned plans

#### Allergies ####

* All active allergies will always be returned as it was considered clinically unsafe to only return a partial record of a patient's active allergies.
* Include resolved allergies
     * The consumer system requests resolved allergies
     * The provider system returns all the resolved allergies along with the active allergies

#### Problems ####

* Search by Significance / Status
     * The consumer system requests combinations of significance and status
     * The consumer system can request Major Active, Minor Active, Major Inactive and/or Minor Inactive
     * The consumer system can request multiple combinations in a single query
     * The provider system returns all problems that match the requested Significance / Status
     * Where no significance / status is supplied by the consumer, the significance / status filter is not applied

#### Uncategorised Data ####

* Search by date
     * The consumer system request all items within a start and end date
     * The provider system returns all items whose asserted date is within the start and end date (inclusive)
     * Where no start date is supplied the search goes from the start of patient record
     * Where no end date is supplied the search goes to the end of patient record
     * Where no dates are supplied by the consumer, the date filter is not applied

#### Consultations ####

* Search by date
     * The consumer system request all items within a start and end date
     * The provider system returns all items whose asserted date is within the start and end date (inclusive)
     * Where no start date is supplied the search goes from the start of patient record
     * Where no end date is supplied the search goes to the end of patient record
     * Where no dates are supplied by the consumer, the date filter is not applied
* Search by most recent
     * The consumer system request the last x consultations
     * The provider system returns the last x consultations
* Where both the date and most recent filters are supplied the results returned are all the consultations that match either the date or the most recent filters.

#### Allergies ####

* All allergies will always be returned.

### Following a linkage ###
For the majority of scenarios, the information required by the consumer can be retrieved through a single query. The consumer system identifies which clinical areas of the patient record it requires and which search criteria should be applied, then calls the GP Connect API. The provider system then returns all the requested information in a single bundle.

There are however scenarios where the information to the first query identifies additional information that is required.

For example:
* a retrieved medication is linked to a problem that the clinician want to review
* a retrieved problem is linked to several consultations that the clinician wants to review
* a retrieved immunisation is linked to a consultation that the clinician wants to review

There may be a decision by the consuming system (or by a user of the consuming system) that they require additional information about the linked clinical item. To get these, the consumer system may wish to call the GP Connect API a second time.

This version of GP Connect does not allow a consumer to search for a specific item in the patient record by its identifier. Instead the consumer should use the supported filters to retrieve a larger dataset and then search for the required item(s) within that dataset.

For example:
* To display a specific consultation linked to a problem, the consumer system could request all the consultations that took place within the active period of the problem then search for the required consultation within the returned data. 

### Scale of Search ###

It is the responsibility of the consuming system to decide what data to request from the provider systems. When determining how wide to make the search criteria, the consumer system must consider the following guidelines:

* The first API query on a patient should aim to retrieve the amount of data required to support the majority of queries that their clinician / user will make whilst avoiding the retrieval of large quantities of unnecessary data.
* Where a follow-up query is required it should aim to retrieve sufficient data to support any other queries that their clinician / user will make.
* The consumer system should aim to avoid scenarios where more than two queries are required on the same patient as part of the same local interaction with a clinician / user. This does NOT preclude the consumer system from making further queries where necessary to support patient care.
* While the consumer system should aim to avoid the retrieval of large quantities of unnecessary data, it is acceptable for the consumer system to request and retrieve a large proportion of the patient's record from the provider system and filter out the unnecessary data before presenting it to their clinicians / users where the consumer organisation has determined it is necessary to support patient care. 

The details on how this is implemented in a API can be found in the [API definition](accessrecord_structured_development_retrieve_patient_record.html)
