---
title: Linkages and Search Criteria
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_linkages.html
summary: "Introduction to linkages between data items in GP Connect"
---
## Linkages ##
One of the purposes in developing the FHIR&reg; profiles is to ensure that clinical data is, as much as possible, presented the same way regardless of the provider system. This ensures the consuming system (and clinician) will always know where to look for each type of information.

However, information about the patient is not just held within the profiles but in how those profiles are linked together. 

For example, linking a medication to a problem means that as well as the record showing what the patient is taking, it also explains why they are taking it.

For a consuming system to be able to interpret this linkage information correctly, it needs to be presented in the same way regardless of the providing system.

### GP Connect FHIR&reg; model ###
To support this, GP Connect has developed a FHIR model that identifies all the GP Connect FHIR profiles and how they are related together to store the patient record.

The model currently covers consultations, problems, medications and medical devices, allergies, immunisations and uncategorised data. Other clinical areas will be added as they are developed.

<img src="images/access_structured/GP_Connect_FHIR_Model.png" alt="GP Connect FHIR Model" style="max-width:100%;max-height:100%;">

The relationships between two FHIR resources are defined in only one of the linked FHIR resources (similar to in a relational database management system). This is shown by the direction of the arrow in the FHIR model. 

For example, the `MedicationStatement` resource contains a field that can be used to look up the linked `Medication`. There is no field in the `Medication` resource that can be used to look up the linked `MedicationStatement`.

## FHIR profiles returned on query ##
When a consumer system requests data on a clinical area the information is returned across a number of FHIR profiles. Choosing which FHIR profiles to return is a balancing act between including enough linked profiles to give the consumer system a comprehensive response to their query but not including so many linked profiles as to swamp the consumer system with data.

The three main considerations used to decide which data to return for each clinical area were:
* include all the FHIR profiles required to fully describe the requested clinical area
* include the FHIR profiles required to define all the linkages from the requested clinical area
* include the FHIR profiles from linked clinical areas where they are key to understanding the requested clinical area 

### Consultations ###
When GP Connect returns a consultation it will supply the metadata of the consultation and all the clinical data that was recorded during the consultation.

The response to the query includes:
* A `List` profile containing references to `Encounter` for every Consultation that met the search criteria

For each `Encounter` referenced in the `List` profile:
*  The `Encounter` profile of the Consultation
*	The `List` profiles that describe the structure of the Consultation
*	The `ProblemHeader` profile of any directly linked Problems
*	The `MedicationRequest`, `MedicationStatement` and `Medication` profiles of any linked Medications or Medical Devices
    * Always include the `MedicationStatement`, `MedicationRequest` (intent = plan) and `Medication` profiles
    * Only include `MedicationRequest` (intent = order) for directly linked issues
    *	Include the `ProblemHeader` profile of any Problems linked to the returned Medications and Medical Devices
*	The `AllergyIntolerance` profile of any linked Allergies
    *	Include the `ProblemHeader` profile of any Problems linked to the returned Allergies
*	The `Immunization` profile of any linked Immunisations
    *	Include the `ProblemHeader` profile of any Problems linked to the returned Immunisations
*	The `Observation` profile of any linked Uncategorised Data
    *	Include the `ProblemHeader` profile of any Problems linked to the returned Uncategorised Data
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above.
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`.


Where a Consultation links to a profile that is not yet supported by the provider system then it is not included in the response. Details on how this is done can be found in the [Consultation Guidance](accessrecord_structured_development_consultation_guidance.html).


Clinical items within the Consultation are always included in the response regardless of their inclusion/exclusion in other parts of the query. So, for example, if a consumer requests a Consultation that contains a Medication but does not explicitly request Medications in the query, the provider will still include the Medication contained in the Consultation as part of its response.

<img src="images/access_structured/Consultation_Return.png" alt="Consultation Returned FHIR profiles" style="max-width:100%;max-height:100%;">

### Problems ###
When GP Connect returns a problem it will supply the metadata and description of the problem and all the clinical data that has been linked to the problem.

The response to the query includes:
* A `List` profile containing references to `ProblemHeader` for every Problem that met the search criteria

For each `ProblemHeader` referenced in the `List` profile:
*	The `ProblemHeader` profile of the Problem
*	The `ProblemHeader` profiles of any directly linked Problems
*	The `MedicationRequest`, `MedicationStatement` and `Medication` profiles of any linked Medications or Medical Devices
    *	Always include the `MedicationStatement`, `MedicationRequest` (intent = plan) and `Medication` profiles
    *	Only include `MedicationRequest` (intent = order) for directly linked issues
*	The `AllergyIntolerance` profile of any linked Allergies
    *	Include the `ProblemHeader` profile of any Problems linked to the returned Allergies
*	The `Immunization` profile of any linked Immunisations
    *	Include the `ProblemHeader` profile of any Problems linked to the returned Immunisations
*	The `Observation` profile of any linked Uncategorised Data
    *	Include the `ProblemHeader` profile of any Problems linked to the returned Uncategorised Data
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clincal profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

Where a Problem links to a profile that is not yet supported by the provider system, then it is not included in the response. Details on how this is done can be found in the [Problem Guidance](accessrecord_structured_development_problems_guidance.html).

Clinical items linked to the Problem are always included in the response regardless of their inclusion/exclusion in other parts of the query. So, for example, if a consumer requests a Problem that links to a Medication but does not explicitly request Medications in the query, the provider will still include the Medication linked to the Problem as part of its response.

<img src="images/access_structured/Problem_Return.png" alt="Problem Returned FHIR profiles" style="max-width:100%;max-height:100%;">

### Medications and medical devices ###
When GP Connect returns a medication or medical device it will supply the prescription plan information. If asked for by the consumer, GP Connect will also return all the prescription issues made under the plan.

The response to the query includes:
* A `List` profile containing references to `MedicationStatement` for every Medication and Medical Device that met the search criteria

For each `MedicationStatement` referenced in the `List` profile:
*  The `MedicationStatement` profile of the Medication or Medical Device
*  The `MedicationRequest` (intent = plan) profile of the Medication or Medical Device
*	The `Medication` profile of the Medication and Medical Device
*	Where requested, the `MedicationRequest` (intent = order) profile for every issue
*	The `ProblemHeader` profiles of any directly linked Problems
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<img src="images/access_structured/Medication_Return.png" alt="Medication and Medical Device Returned FHIR profiles" style="max-width:100%;max-height:100%;">

### Allergies ###
When GP Connect returns an allergy it will supply all the allergy data.

The response to the query includes:
* A `List` profile containing references to `AllergyIntolerance` for every active Allergy
* Where requested, a `List` profile containing references to `AllergyIntolerance` for every ended Allergy

For each `AllergyIntolerance` referenced in either of the `List` profiles:
*	The `AllergyIntolerance` profile of the Allergy
*	The `ProblemHeader` profiles of any directly linked Problems
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`
    
<center>
<img src="images/access_structured/Allergy_Return.png" alt="Allergy Returned FHIR profiles" style="max-width:70%;max-height:70%;">
</center>

### Immunisation ###
When GP Connect returns an immunisation it will supply all the immunisation data.

The response to the query includes:
* A `List` profile containing references to `Immunization` for every Immunisation

For each `Immunization` referenced in the `List` profile:
*	The `Immunization` profile of the Immunisation
*	The `ProblemHeader` profiles of any directly linked Problems
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<center>
<img src="images/access_structured/Immunisation_Return.png" alt="Immunisation Returned FHIR profiles" style="max-width:70%;max-height:70%;">
</center>

### Uncategorised data ###
When GP Connect returns uncategorised data it will supply all the data about the uncategorised data.

The response to the query includes:
* A `List` profile containing references to `Observation` for every Uncategorised Data that met the search criteria

For each `Observation` referenced in the `List` profile:
*	The `Observation` profile of the Uncategorised Data
*	The `ProblemHeader` profiles of any directly linked Problems
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<center>
<img src="images/access_structured/Uncategorised_Return.png" alt="Uncategorised Data Returned FHIR profiles" style="max-width:70%;max-height:70%;"> 
</center>

### Duplicate returned profiles ###

Where the same instance of a profile is returned from multiple query responses (for example a medication is returned as part of the medication search and the consultation search), it will only be included once in the response message.

## Search ##

The GP Connect API allows the consumer system to specify what data it requires from the provider system about a specified patient.

### Search criteria ###

The consumer system can specify which clinical areas it wishes to retrieve and within each clinical area what search criteria it wants to apply.

#### Medication and medical devices ####

* Search for all Medications and Medical Devices that were active on or after the specified date
     * The consumer system requests all items from a start date
     * The provider system returns all plans whose effective period end date is null or is on or after the start date
     * Where no date is supplied by the consumer, all medications and medical devices are returned
* Include all the prescriptions issued under the returned medication/medical device plans
     * The consumer system requests prescription issues
     * For each of the returned medication/medical device plans, the provider system includes data for all of its issues

#### Allergies ####

* All active allergies will always be returned as it was considered clinically unsafe to only return a partial record of a patient's active allergies
* Include resolved allergies
     * The consumer system requests resolved allergies
     * The provider system returns all the resolved allergies along with the active allergies

#### Problems ####

* Search for Problems with the specified combinations of significance and status
     * The consumer system requests combinations of significance and status
     * The consumer system can request Major Active, Minor Active, Major Inactive and/or Minor Inactive
     * The consumer system can request multiple combinations in a single query
     * The provider system returns all Problems that match the requested significance / status
     * Where no significance / status is supplied by the consumer, all Problems are returned

#### Uncategorised data ####

* Search for all Uncategorised Data within the specified date range
     * The consumer system request all items within a start and end date
     * The provider system returns all items whose asserted date is within the start and end date (inclusive)
     * Where no start date is supplied the search goes from the start of patient record
     * Where no end date is supplied the search goes to the end of patient record
     * Where no dates are supplied by the consumer, all uncategorised data items are returned

#### Consultations ####

* Search for all Consultations within the specified date range
     * The consumer system request all items within a start and end date
     * The provider system returns all items whose asserted date is within the start and end date (inclusive)
     * Where there is a start date but no end date, the search goes to the end of the patient record
     * Where there is an end date but no start date the search goes from the start of the patient record
* Search for the most recent x Consultations within the patient's record
     * The consumer system request the last x consultations
     * The provider system returns the last x consultations
* Where a single filter is supplied by the consumer, it is applied as defined above
* Where both filters are supplied by the consumer, all the Consultations that match either of the filters are returned
* If no filters are supplied by the consumer, all Consultations are returned

#### Immunisations ####

* All Immunisations will always be returned.

### Following a linkage ###
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

### Scale of search ###

It is the responsibility of the consuming system to decide what data to request from the provider systems. When determining how wide to make the search criteria, the consumer system must consider the following guidelines:

* Always apply the [Caldicott Principles](https://www.igt.hscic.gov.uk/Caldicott2Principles.aspx) 
* The first API query on a patient should aim to retrieve the amount of data required to support the majority of queries that their clinician/user will make whilst avoiding the retrieval of large quantities of unnecessary data
* Where a follow-up query is required it should aim to retrieve sufficient data to support any other queries that their clinician/user will make
* The consumer system should aim to avoid scenarios where more than two queries are required on the same patient as part of the same local interaction with a clinician/user. This does NOT preclude the consumer system from making further queries where necessary to support patient care.
* It is acceptable for the consumer system to request and retrieve a large proportion of the patient's record from the provider system and filter out the unnecessary data before presenting it to their clinicians / users where the consumer organisation: 
     * has determined it is necessary to support patient care
     * has met all of the GP Connect information governance (IG) requirements including data sharing agreements, confidentiality and auditing

The details on how this is implemented in an API can be found in the [API definition](accessrecord_structured_development_retrieve_patient_record.html).
