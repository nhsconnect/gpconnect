---
title: Linkages
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_linkages.html
summary: "Introduction to linkages between data items in GP Connect"
---

## Linkages ##

One of the purposes in developing the FHIR&reg; profiles is to ensure that clinical data is, as much as possible, presented the same way regardless of the provider system.
This ensures the consuming system (and clinician) will always know where to look for each type of information.
However, information about the patient is not just held within the profiles but in how those profiles are linked together.
For example, linking a medication to a problem means that as well as the record showing what the patient is taking, it also explains why they are taking it.

For a consuming system to be able to interpret this linkage information correctly, it needs to be presented in the same way regardless of the providing system.

### GP Connect FHIR&reg; model ###

To support this, GP Connect has developed a FHIR model that identifies all the GP Connect FHIR profiles and how they are related together to store the patient record.

The model currently covers Consultations, Problems, Medications and Medical Devices, Allergies, Immunisations, Uncategorised Data, Referrals, Investigations, Documents and Diary Entries.
Other clinical areas will be added as they are developed.

<a href="images/access_structured/GP_Connect_FHIR_Model_v3.png"><img src="images/access_structured/GP_Connect_FHIR_Model_v3.png" alt="GP Connect FHIR Model" style="max-width:100%;max-height:100%;"></a>

<img src="images/access_structured/FHIR_model_key.png" alt="Key for GP Connect FHIR Model" style="max-width:50%;max-height:50%;">

The relationships between two FHIR profiles are recorded in only one of the linked FHIR profiles (similar to in a relational database management system).
This is shown by the direction of the arrow in the FHIR model.
For example, the `MedicationStatement` profile contains a field that can be used to look up the linked `Medication`.
There is no field in the `Medication` profile that can be used to look up the linked `MedicationStatement`.

## FHIR profiles returned on query ##
When a consumer system requests data on a clinical area the information may be returned across a number of FHIR profiles.
Choosing which FHIR profiles to return is a balancing act between including enough linked profiles to give the consumer system a comprehensive response to their query but not including so many linked profiles as to swamp the consumer system with data.

The three main considerations used to decide which data to return for each clinical area were:
* include all the FHIR profiles required to fully describe the requested clinical area
* include the FHIR profiles required to define all the linkages from the requested clinical area
* include the FHIR profiles from linked clinical areas where they are key to understanding the requested clinical area

For each clinical area in a query that returns data a list should be generated that contains links to all data items returned for that clinical area.
Some query responses will contain more than one list for a clinical area.
The nature of the list can be determined from the list elements, see [Using lists to return data](accessrecord_structured_development_lists_for_message_structure.html) for details.

### Consultations and problems containing unsupported clinical items

Depending on the GP Connect version supported by the provider system it can be possible for the consultation or problem to link to a clinical item that the provider system is not yet able to export with GP Connect. For example, if the consultation contains a link to a referral record, but the provider system does not yet support exporting referrals.

Where a provider system is not able to export a linked clinical item, it will create a section.section.entry (or section.entry) entry with the:

-   `List.entry.item.display` set to “[Clinical area] items are not supported by the provider system.”

       Where [Clinical area] identifies the type of the clinical item that is not supported.

The example below shows references to two items, one for an observation and another for referrals that aren't supported by the provider system:

```json
{
  "item": {
    "reference": "Observation/6734572634"
  }
},
{
  "item": {
    "display": "Referral items are not supported by the provider system"
  }
}
```

### Consultations ###

When GP Connect returns a consultation it will supply the metadata of the consultation and all the clinical data that was recorded during the consultation.

The response to the query includes:
* A `List` profile containing references to `Encounter` for every Consultation that met the search criteria
* A `List` profile for each clinical area that data exists in the bundle

For each `Encounter` referenced in the `List` profile:
*   The `Encounter` profile of the Consultation
*	The `List` profiles that describe the structure of the Consultation
*	The `ProblemHeader (Condition)` profile of any directly linked Problems
*	The `MedicationRequest`, `MedicationStatement` and `Medication` profiles of any linked Medications or Medical Devices
    *   Always include the `MedicationStatement`, `MedicationRequest` (intent = plan) and `Medication` profiles
    *   Only include `MedicationRequest` (intent = order) for directly linked issues
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Medications and Medical Devices
*	The `AllergyIntolerance` profile of any linked Allergies, including resolved allergies
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Allergies
*	The `Immunization` profile of any linked Immunisations
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Immunisations
*	The `Observation` profile of any linked Uncategorised Data
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Uncategorised Data
*	The `ReferralRequest` profile of any linked Referrals
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Referrals
*	The `DocumentReference` profile of any linked Documents
    * Only include the document metadata in any returned `DocumentReference` profile, do not include the binary file
    * In order to retrieve the binary file, a consumer must have been assured for the Access Document capability
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Documents
*	The `DiagnosticReport`, `ProcedureRequest`, `Observation`, `Specimen` and `DocumentReference` profiles of any linked Investigations
    *   Only include the document metadata in any returned `DocumentReference` profile, do not include the binary file.
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Investigation    
*  The `ProcedureRequest`profile of any linked Diary Entries
    *   Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Diary Entries
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    *   Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`.

Where a Consultation links to a profile that is not yet supported by the provider system then it is not included in the response.
Details on how this is done can be found in the [Consultation Guidance](accessrecord_structured_development_consultation_guidance.html).

Clinical items within the Consultation are always included in the response regardless of their inclusion/exclusion in other parts of the query.
So, for example, if a consumer requests consultations then any medications that are contained in the consultations returned will be present in the bundle, regardless of the medications parameter being absent or set to false in the request.

<a href="images/access_structured/Consultation_Return_v3.png"><img src="images/access_structured/Consultation_Return_v3.png" alt="Consultation Returned FHIR profiles" style="max-width:100%;max-height:100%;"></a>

### Problems ###

When GP Connect returns a problem it will supply the metadata and description of the problem and all the clinical data that has been linked to the problem.

The response to the query includes:
* A `List` profile containing references to `ProblemHeader (Condition)` for every Problem that met the search criteria
* A `List` profile containing references to `ProblemHeader (Condition)` for every Problem not meeting the search critieria but directly linked to a Problem which does meet the search criteria
* A `List` profile for each clinical area that data exists in the bundle

For each `ProblemHeader (Condition)` referenced in the `List` profile:
*	The `ProblemHeader (Condition)` profile of the Problem
*	The `ProblemHeader (Condition)` profiles of any directly linked Problems
*	The `Encounter` profiles of any linked Consultations
*   The `MedicationRequest`, `MedicationStatement` and `Medication` profiles of any linked Medications or Medical Devices
    *	Always include the `MedicationStatement`, `MedicationRequest` (intent = plan) and `Medication` profiles
    *	Only include `MedicationRequest` (intent = order) for directly linked issues
*	The `AllergyIntolerance` profile of any linked Allergies
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Allergies
*	The `Immunization` profile of any linked Immunisations
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Immunisations
*	The `Observation` profile of any linked Uncategorised Data
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Uncategorised Data
*	The `ReferralRequest` profile of any linked Referrals
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Referrals
*	The `DocumentReference` profile of any linked Documents
    * Only include the document metadata in any returned `DocumentReference` profile, do not include the binary file.
    * In order to retrieve the binary file, a consumer must have been assured for the Access Document capability
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Documents
*	The `DiagnosticReport`, `ProcedureRequest`, `Observation`, `Specimen` and `DocumentReference` profiles of any linked Investigations
    * Only include the document metadata in any returned `DocumentReference` profile, do not include the binary file.
    *	Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Investigation    
*  The `ProcedureRequest`profile of any linked Diary Entries
    * Include the `ProblemHeader (Condition)` profile of any Problems linked to the returned Diary Entries
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

Where a Problem links to a profile that is not yet supported by the provider system, then it is not included in the response. Details on how this is done can be found in the [Problem Guidance](accessrecord_structured_development_problems_guidance.html).

Clinical items linked to the Problem are always included in the response regardless of their inclusion/exclusion in other parts of the query.
So, for example, if a consumer requests a Problem that links to a Medication but does not explicitly request Medications in the query, the provider will still include the Medication linked to the Problem as part of its response.

<a href="images/access_structured/Problem_Return_v3.png"><img src="images/access_structured/Problem_Return_v3.png" alt="Problem Returned FHIR profiles" style="max-width:100%;max-height:100%;"></a>

### Medications and medical devices ###

When GP Connect returns a medication or medical device it will supply the prescription plan information.
Unless excluded by the consumer request, GP Connect will also return all the prescription issues made under the plan.

The response to the query includes:
* A `List` profile containing references to `MedicationStatement` for every Medication and Medical Device that met the search criteria
* A `List` profile containing references to each `ProblemHeader` that is contained in the bundle

For each `MedicationStatement` referenced in the `List` profile:
* The `MedicationStatement` profile of the Medication or Medical Device
* The `MedicationRequest` (intent = plan) profile of the Medication or Medical Device
* The `Medication` profile of the Medication and Medical Device
* Where requested, the `MedicationRequest` (intent = order) profile for every issue
* The `ProblemHeader (Condition)` profiles of any directly linked Problems
* All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<a href="images/access_structured/Medication_Return_v2.png"><img src="images/access_structured/Medication_Return_v2.png" alt="Medication and Medical Device Returned FHIR profiles" style="max-width:100%;max-height:100%;"></a>

### Allergies ###

When GP Connect returns an allergy it will supply all the allergy data.

The response to the query includes:
* A `List` profile containing references to `AllergyIntolerance` for every active Allergy
* Where requested, a `List` profile containing references to `AllergyIntolerance` for every ended Allergy
* A `List` profile containing references to each `ProblemHeader` that is contained in the bundle

For each `AllergyIntolerance` referenced in either of the `List` profiles:
* The `AllergyIntolerance` profile of the Allergy
* The `ProblemHeader (Condition)` profiles of any directly linked Problems
* All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<center>
<a href="images/access_structured/Allergy_Return.png"><img src="images/access_structured/Allergy_Return.png" alt="Allergy Returned FHIR profiles" style="max-width:70%;max-height:70%;"></a>
</center>

### Immunisations ###
When GP Connect returns an immunisation it will supply all the immunisation data.

The response to the query includes:
* A `List` profile containing references to `Immunization` for every Immunisation and `Observation` for every consent / dissent to immunisation (referred to below as query response `List` profile)
* A `List` profile containing references to each `ProblemHeader` that is contained in the bundle

For each `Immunization` referenced in the query response `List` profile:
*	The `Immunization` profile of the Immunisation
*	The `ProblemHeader (Condition)` profiles of any directly linked Problems

For each `Observation` referenced in the query response `List` profile:
*	The `Observation` profile of the consent / dissent for immunisation
*	The `ProblemHeader (Condition)` profiles of any directly linked Problems

For each `Immunization` and `Observation` referenced in the query response `List` profile:
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<center>
<a href="images/access_structured/Immunisation_Return_2.png"><img src="images/access_structured/Immunisation_Return_2.png" alt="Immunisation Returned FHIR profiles" style="max-width:70%;max-height:70%;"></a>
</center>

### Uncategorised data ###
When GP Connect returns uncategorised data it will supply all the data about the uncategorised data.

The response to the query includes:
* A `List` profile containing references to `Observation` for every Uncategorised Data that met the search criteria
* A `List` profile containing references to each `ProblemHeader` that is contained in the bundle

For each `Observation` referenced in the `List` profile:
*	The `Observation` profile of the Uncategorised Data
*	The `ProblemHeader (Condition)` profiles of any directly linked Problems
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<center>
<a href="images/access_structured/Uncategorised_Return.png"><img src="images/access_structured/Uncategorised_Return.png" alt="Uncategorised Data Returned FHIR profiles" style="max-width:70%;max-height:70%;"></a>
</center>

### Referrals ###
When GP Connect returns a referral it will supply all the referral data.

The response to the query includes:
* A `List` profile containing references to `ReferralRequest` for every Referral that met the search criteria
* A `List` profile containing references to each `ProblemHeader` that is contained in the bundle

For each `ReferralRequest` referenced in the `List` profile:
*	The `ReferralRequest` profile of the Referral
*	The `ProblemHeader (Condition)` profiles of any directly linked Problems
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<center>
<a href="images/access_structured/Referral_Return_v2.png"><img src="images/access_structured/Referral_Return_v2.png" alt="Referral Returned FHIR profiles" style="max-width:70%;max-height:70%;"></a>
</center>

### Investigations ###
When GP Connect returns an investigation it will supply all the investigation information.

The response to the query includes:
* A `List` profile containing references to `DiagnosticReport` for every Investigation that met the search criteria
* A `List` profile containing references to each `ProblemHeader` that is contained in the bundle

For each `DiagnosticReport` referenced in the `List` profile:
*  The `DiagnosticReport` profile of the Investigation
*  The `ProcedureRequest` profile of the Investigation
*	The `Specimen` profiles of the Investigation
*	The `Observation` profiles of the Investigation
*	The `DocumentReference` profiles of the Investigation
    * Only include the document metadata in any returned `DocumentReference` profile, do not include the binary file.
*	The `ProblemHeader (Condition)` profiles of any directly linked Problems
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<a href="images/access_structured/Investigation_Return_v3.png"><img src="images/access_structured/Investigation_Return_v3.png" alt="Investigation Returned FHIR profiles" style="max-width:100%;max-height:100%;"></a>

### Diary entries ###
When GP Connect returns a diary entry it will supply all the diary entry data.

The response to the query includes:
* A `List` profile containing references to `ProcedureRequest` for every Diary Entry that met the search criteria
* A `List` profile containing references to each `ProblemHeader` that is contained in the bundle

For each `ProcedureRequest` referenced in the `List` profile:
*	The `ProcedureRequest` profile of the Diary Entry
*	The `ProblemHeader (Condition)` profiles of any directly linked Problems
*  All administrative profiles referenced directly (or via another administrative profile) by any of the clinical profiles included above
    * Include `Patient`, `Organization`, `PractitionerRole`, `Practitioner` and `Location`

<center>
<a href="images/access_structured/DiaryEntry_Return.png"><img src="images/access_structured/DiaryEntry_Return.png" alt="Diary Entry Returned FHIR profiles" style="max-width:70%;max-height:70%;"></a>
</center>

### Multiple clinical areas requests ###

The details above have described the response a request for a single clinical area.
The consumer may include more than one clinical area in a request.
The request must be compliant with the criteria for multiple parameters as described in [API Definition - Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html)

In responding to a valid multiple parameter request, the provider must return lists and resources as defined above for each clinical area included in the request.
In addition, the provider must return `List` resources as described in [Using lists to return data](accessrecord_structured_development_lists_for_message_structure.html)
This may result in consolidated or multiple `List` profiles for clinical areas.
The following models demonstrate this.

This model is an example of a request for medications and allergies.
It is included to show how related problem references are consolidated into a single `List` profile where more than one clinical area has been requested.
This applies regardles of which clincial areas or how many clinical areas are included in the request.

<center>
<a href="images/access_structured/Medications_Allergies_Return.png"><img src="images/access_structured/Medications_Allergies_Return.png" alt="Medications and Allergies Returned FHIR profiles" style="max-width:70%;max-height:70%;"></a>
</center>

This model is an example of a request for consultations, problems, medications and allergies.
It also includes a consolidated related problems `List` profile, but is included to show the multiple `List` profiles returned due to the inclusion of
* a primary list for each of the requested clinical areas
* secondary lists for all clinical areas contained in consultations or linked to problems, regardless of inclusion in the request

<center>
<a href="images/access_structured/Summary_Return_v2.png"><img src="images/access_structured/Summary_Return_v2.png" alt="Medications, Allergies, Problems and Consultations Returned FHIR profiles" style="max-width:70%;max-height:70%;"></a>
</center>

### Duplicate returned profiles ###

Where the same instance of a profile is returned from multiple query responses (for example a medication is returned as part of the medication search and the consultation search), it will only be included once in the response message.

The details on how this is implemented in an API can be found in the [API definition](accessrecord_structured_development_retrieve_patient_record.html).
