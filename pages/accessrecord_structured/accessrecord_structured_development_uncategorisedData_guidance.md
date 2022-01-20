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

The volume of this categorisation varies between provider systems. 
For the majority of provider systems, the following types of information are explicitly categorised when they are recorded.
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
There is data that a clinician/user will enter without identifying what type of information they are recording. 
This information is usually entered as a combination of clinical code(s), values, qualifiers and text.

For example:
* the clinician records the patient’s resting pulse by recording the resting pulse clinical code followed by a value of the patient’s pulse.
* the clinician records that a patient has a sore throat by recording the sore throat clinical code

Consideration was given to attempting to categorise data using the recorded clinical codes. 
It was decided not to progress this based on a clinical review of its risks and benefits.

## Uncategorised data definition ##
Uncategorised data will include the following 
* data items in the patient record that do not fit into one of the existing or planned clinical areas defined by GP Connect
* inbound referrals (GP Connect referral resource is defined as outbound referrals only) 

Where text is entered freely into a consultation without being associated with a clinical code it will not be returned as an item of uncategorised data. 
This free text will ONLY be returned as part of the consultation and will be returned in an `Observation` with the SNOMED code `37331000000100 Comment note`.

## Observation profile ##

Uncategorised data can contain many different types of clinical information. As the type is not known it is not possible to determine which is the correct FHIR&reg; profile to use for the information. Therefore, uncategorised data will always be contained in an `Observation` profile.

## Qualifiers ##

Qualifiers are used to refine the meaning of the coded element of the record.

Each provider system supports a different set of qualifiers. However, there are three key qualifiers that are common across all provider systems:

* Laterality - for example, a patient record may have a fracture of the left femur
* Severity - for example, a patient record may have a severe asthmatic attack
* Episodicity - for example, this is the patient's first episode of an asthmatic attack

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

This approach **MUST** be used for blood pressure readings where the systolic and diastolic values were taken together.

## Hierarchical uncategorised data ##
There are cases where several pieces of uncategorised data are related to each other in a hierarchical structure.

For example:
* Alcohol Consumption
    * Breath alcohol level 15mmol/L
    * O/E - spleen just palpable

Where this occurs, the data is supplied in a format where the hierarchical information is made available to the consumer system if they want to rebuild the hierarchical structure or if not they can consume each of the resources individually flattening out the structure if it is not of benefit to their users.

### Modelling ###

Each item of uncategorised data in the hierarchy is recorded in its own FHIR resource, this may be an `observation`, `immunization` or any other that is defined in GP Connect . The structure is represented using the `questionnaireResponse` resource.

* The top-level item will contain an `observation` in the `questionnaireResponse.parent` element. 
* The child items will be pointed to as references to the relevant resources within the `questionnaireResponse.item.answer` field(s). 

### Consultations and problem ###

Being in a hierarchy has no impact on the linkage between an item of uncategorised data and a consultation or problem. 
If the item is recorded in a consultation it will be directly referenced by the consultation. 
If the item is linked to a problem it will be directly referenced by the problem.

For example, if four items of uncategorised data are recorded under the investigation heading in a consultation with one of the items acting as a parent to the other three items. 
Direct references to all four items will be populated in the `List(Heading)` profile. 
If all four items are linked to a problem then all four items will be populated in the `ProblemHeader (Condition)` profile.

<a href="images/access_structured/Uncategorised_Structure_v2.png"><IMG src="images/access_structured/Uncategorised_Structure_v2.png" alt="Uncateogirsed Structure" style="max-width:100%;max-height:100%;"></a>

### Hierarchical data involving different clinical areas

If the hierarchical data contains items from other clinical areas that are not held in an observation resource, then these should always be included by referencing them from the questoinnaireResponse as for any other uncategorised 'observation' resource.

<a href="images/access_structured/Uncategorised_Structure1_v2.png"><IMG src="images/access_structured/Uncategorised_Structure1_v2.png" alt="Uncategorised structure with items from different clinical areas" style="max-width:100%;max-height:100%;"></a>

Where an item from a different clinical area that is not in an observation resource but is the header element in the native system, then the provider system **MUST** include them as an item in the questionnaireResponse and create an observation to act as the header with the rubric from the code of the original element in the text field of the codable concept. 
This **MUST** be done in accordance with the [uncategorised observation guidelines](accessrecord_structured_development_observation_uncategoriseddata) and populate the performer and issued elements in line with who recorded the original data and when it was recorded.

### Different clinical areas against an uncategorised data request only
   
The above example demonstrate the structure for the hierachical date and the relationship with consultations.
The same principles apply if consultations are not requested.
This example shows where only uncategorised data has been requested but the hierarchical data includes resources from a different clinical area, an allergy in this case.
The questionnaireResponse is populated identical to the example above.
However, only resources which satisfy the criteria of the request are included.
The diagram therefore shows the response for uncategorised data only, thus the items in grey boxes (encounter and allergyIntolerance resources) are referenced but not included.
   


## Representing inbound referrals ##

As noted above, inbound referrals are to be returned using `observation` resources as per this guidance.
The following additions / exceptions apply to the population of elements, otherwise populate as per the [uncategorised data profile](accessrecord_structured_development_observation_uncategoriseddata) implementation guidance. 

* Where known, the referrer details **MUST** be returned using the `performer` element
* The `performer` element **MAY** be absent, for example if the referrer is not recorded
* Additional fields capturing details of the referral in the source system **SHOULD** be returned in the `component`
   * Populate `component.code.text` with the data label
   * Populate `component.value` with the data item code / text
* Self referrals **MUST** be identified by including the text "Self referral" in the `comment` element

## Representing blood pressure readings from GP systems
Blood pressure is one of the most common observations that is recorded in GP records. There are over 70 million blood pressures recorded in general practice every year.
As this is the case there is a desire to represent the various blood pressure concepts that are recorded in a common format wherever possible.
In the majority of cases there are two components that comprise a blood pressure reading regardless of the type of reading. These are a systolic blood pressure reading and a diastolic blood pressure reading. In many cases these are also recorded as a triple with a heading or panel concept. 

### The FHIR vital sign blood pressure profile
This version of GP Connect does not support the 'vital signs' aspect of the FHIR specification as there is currently no consensus in the UK as to what is/isn't a vital sign. 

However, the way we have represented blood pressures is based on the FHIR vital signs blood pressure profile [http://hl7.org/fhir/STU3/bp.html](http://hl7.org/fhir/STU3/bp.html).
The profile uses a loinc 'magic code' to flag certain blood pressures as vital signs. We are not currently using this flag in GP Connect. 

Where possible blood pressures exported via GP Connect though will be exported using the same structure as the vital signs blood pressure profile. They **MUST** always use the same units, mm[Hg] whether exported in the triple structure or as individual observations. 

GP Connect has improved the consistency of the data that will be exported, it is however the responsibility of the consuming system to interpret the blood pressure codes they recieve regardless of whether they are in a triple structure or as individual observations.

### Standard blood pressure representation

The way standard blood pressures are recorded in different clinical systems varies. These can be described by the following 3 different patterns,

 - Recorded as the following triple in the below structure and using any of the codes from the table below,
 
<a href="images/access_structured/BP_Diagram.png"><IMG src="images/access_structured/BP_Triple.png"></a>   
 
 - Recorded as 2 individual readings that are grouped together with no panel code using any of the systolic and diastolic codes from the table below,
 
 <a href="images/access_structured/BP_Diagram.png"><IMG src="images/access_structured/BP_ComponentCodes.png"></a>   
 
   Where there is no panel code then '163020007 On examination - blood pressure reading (finding)' **MUST** be used in the GP Connect triple.
   
 - Recorded using a panel code with two readings but no systolic and diastolic codes. This may be recorded as either of the 2 panel codes from the table below,
 
 <a href="images/access_structured/BP_Diagram.png"><IMG src="images/access_structured/BP_HeaderCodeNoComponent.png"></a>   
 
   Where there is only a panel code the following codes **MUST** be used to complete the triple for export in GP Connect, 
      - 163020007 On examination - blood pressure reading (finding) and 386534000 Arterial blood pressure (observable entity)
 
In GP Connect we have decided that all of these variations will be represented using the triple structure in order to make the representation more uniform.

Following the guidance above to determine the appropriate codes for the triple will result in the following structure which may contain any of the codes from the table below, 
 
<a href="images/access_structured/BP_Diagram.png"><IMG src="images/access_structured/BP_Diagram.png"></a> 
 
The triple may contain any combination of the following SNOMED codes for the panel, systolic and diastolic components,
 
| Panel code | Systolic blood pressure code | Diastolic blood pressure code |
|---|---|---|
|163020007 On examination - blood pressure reading (finding)  | 72313002 Systolic arterial pressure (observable entity)  | 1091811000000102 Diastolic arterial pressure (observable entity) |
| 386534000 Arterial blood pressure (observable entity) | 271649006 Systolic blood pressure | 271650006  Diastolic blood pressure |
| 75367002 Blood pressure (observable entity) | | |

Where there is only a single component value recorded then the triple **MUST** still be represented using the relevant 3 codes with the component representing the missing reading containing the relevant dataAbsentReason code.

### Blood pressures that will be in the same structure

The table contains other blood pressure readings that **MUST** always be represented when exported from GP Connect as triples in line with the simple blood pressure format.

| Panel code | Systolic blood pressure code | Diastolic blood pressure code |
|---|---|---|
| 163034007 Standing blood pressure (observable entity) | 400974009 Standing systolic blood pressure | 400975005 Standing diastolic blood pressure |
| 163035008 Sitting blood pressure (observable entity) | 407554009 Sitting systolic blood pressure | 407555005 Sitting diastolic blood pressure |
| 163033001 Lying blood pressure (observable entity) | 407556006 Lying systolic blood pressure | 407557002 Lying diastolic blood pressure |

In addition to the triples that have been defined here any blood pressure that is recorded as a triple within the GP clinical system **MUST** always follow this structure.

### Blood pressure readings with no defined triples

Where the blood pressure reading has not been defined here and is not recorded in the local system as a triple then these will be exported as individual observations. These observations **MUST** be linked using the 'related' element with a value of 'has-member' where they are recorded as a pair but with no panel code.

## Using the `List` resource for uncategorised data queries

The results of a query for uncategorised data **MUST** return a `List` containing references to all `Observation` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason.code` with the value `no-content-recorded`. In this case, `List.note` **MUST** be populated with the text 'Information not available'.
