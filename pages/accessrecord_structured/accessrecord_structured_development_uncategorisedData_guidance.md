---
title: Uncategorised data guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_uncategorisedData_guidance.html
summary: "Guidance for populating and consuming the uncategorised data from GP systems using GP Connect"
---

## What is categorised data? ##
When a clinician/user of a GP clinical system records clinical data they may, as part of entering the information, identify what type of information they are recording.

For example, where the clinician uses a GP system's allergy function to record a patient’s allergy information it is explicitly identified in the system as an allergy.

The volume of this categorisation varies between provider systems. For the majority of provider systems, the following types of information are explicitly categorised when they are recorded.
* Allergy
* Appointment
* Consultation
* Demographics
* Diary Entry
* Document
* Flag/Alert
* Immunisation
* Investigation
* Medication and Medical Device
* Problem
* Referral
* Test Request

## What is uncategorised data? ##
There is data that a clinician/user will enter without identifying what type of information they are recording. This information is usually entered as either free text or a combination of clinical code(s), values, qualifiers and text.

For example:
* the clinician records the patient’s resting pulse by recording the resting pulse clinical code followed by a value of the patient’s pulse.
* the clinician records that a patient has a sore throat by recording the sore throat clinical code
* the clinician records that a patient reports being irritable with their family as a piece of free text

Consideration was given to attempting to categorise data using the recorded clinical codes. It was decided not to progress this based on a clinical review of its risks and benefits.

## Uncategorised data definition ## 

* Uncategorised data is any item of data in the patient record that does not fit into one of the existing or planned clinical areas defined by GP Connect.

## Observation profile ##

Uncategorised data can contain many different types of clinical information. As the type is not known it is not possible to determine which is the correct FHIR profile to use for the information. Therefore uncategorised data will always be contained in an `Observation` profile.

## Qualifiers ##

Qualifiers are used to refine the meaning of the coded element of the record.

Each provider system supports a different set of qualifiers. However, there are three key qualifiers that are common across all provider systems:

* Laterality - for example, a patient record may have a fracture of the left femur.
* Severity - for example, a patient record may have a severe asthmatic attack.
* Episodicity - for example, this is the patient's first episode of an asthmatic attack.

The provider system will translate all of the qualifiers included with the clinical code into human-readable text and concatenate them with the text entered by the recorder (placing the qualifiers first) and placing in `observation.comment`.

## Values ##

Values are any reading or result that is recorded with the uncategorised data. For example, the uncategorised data 50373000 (Body Height) may have a value of 156cm.

### Single values ###
The majority of uncategorised data that contains values will only have a single value. In these cases, the value will be exported in `observation.value`.

### Multiple values ###
There are cases where an item of uncategorised data may contain multiple values. This happens when:
* there is a single clinical code that describes the uncategorised data as a whole
and
* each recorded value in the uncategorised data is described by its own clinical code

In these cases, each value will be exported in an instance of `observation.component`.

This approach MUST be used for blood preasure readings where the systolic and diastolic values were taken together.

## Hierarchical Uncategorised Data ##
There are cases where several pieces of uncategorised data are be related to each other in a hierarchical structure. 

For example: 
* Alcohol Consumption
    * Breath alcohol level 15mmol/L
    * O/E - spleen just palapable

Where this occurs the data is supplied in a flattened format with the herachical information made available to the consumer system if they want to rebuild the hierarchical structure.

### Modeling ###

Each item of uncategorised data in the hierarchy is recorded is in its own `observation` profile. The structure is represented using the `observation.related` field.

* The top level item will contain `observation.related.target` pointing to each of the child items with an `observation.related.type` of `has-member` 
* The child items will contain `observation.related.target` pointing to the top level item with an `observation.related.type` of `derived-from`

Note: This follows the same model that will be used to represent Investigations and Pathology.

### Consultations and Problem ###

Being in a hierarchy has no impact on the linkage between an item of uncategorised data and a Consultation or Problem. If the item is recorded in a consultation it will be directly referenced by the consultation, if the item is linked to a problem it will be directly referenced by the problem.

For example, if four items of uncategorised data are recorded under the investigation heading in a consultation with one of the items acting as a parent to the other three items. Direct references to all four items will be populated in the `List(Heading)` profile. If all four items are linked to a problem then all four items will be populated in the `ProblemHeader (Condition)` profile.

<a href="images/access_structured/Uncategorised_Structure.png"><IMG src="images/access_structured/Uncategorised_Structure.png" alt="Uncateogirsed Structure" style="max-width:100%;max-height:100%;"></a>

### Heirarchical data involving different clinical areas

If the hierarchical data contains items from other clinical areas that are not held in an observation resource then these should always be included by referencing them from the header observation related element as a 'has-member' tpye. This will mean that unlike references to other observations references to these data items will be one directional as illustrated in the diagram below.

<a href="images/access_structured/Uncategorised_Structure.png"><IMG src="images/access_structured/Uncategorised_Structure1.png" alt="Uncateogirsed structure with items from different clinical areas" style="max-width:100%;max-height:100%;"></a>
   
Where an item from a different clinical area that is not in an observation resource but in the native system is the header element. Then the provider sytem **MUST** include them as a child element and create an observation to act as the header with the rubric from the code of the original element in the text field of the codable concept. This **MUST** be done in accordance with the [uncategorised observation guidelines] and populate the performer and issued elements in line with who recorded the original data and when it was recorded.

## Using the `List` resource for uncategorised data queries

The results of a query for uncategorised data **MUST** return a `List` containing references to all `Observation` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason` with the value `noContent`.


