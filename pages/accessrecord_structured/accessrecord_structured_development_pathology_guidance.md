---
title: Pathology guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_pathology_guidance.html
summary: "Guidance on the representation of allergies and intolerances in GP Connect"
---

# Investigations Modeling

### Pathology scope in GP Connect

For this version of the specification the scope of pathology is considered to be making available any pathology results contained in GP systems that have been received from the lab by an EDIFact message.

As such there are a number of items that are not currently in scope for the pathology area of this version of GP Connect. These are as follows,

* pathology results that have been entered in a GP system using a code as an individual item. These may have a value and other qualifiers associated with them. 
* test results that are received as documents or images
* making available any test requests
* providing the original test report document as it was provided the practice

### Use of lagnguage to describe pathology reports

When describing pathology reports different regions and professions sometimes use different words to decribe the same entities. Therefore for avoidance of confusion there are a couple of terms that we need to define.

* Test group - is the phrase we are using to describe any group of tests that has been created by the laboratory or other providing organisation. These are often referred to as batteries, panels and profiles.

* Test result - this is an the specific result that has been provided by the laboratory or other provider. These may be standalone results or may be a part of a 'Test group'. They are also sometimes referred to as test analytes.

## Patholgy reporting in GP practices

Currently GP practices receive the majority of the results of investigations that they have requested in the form of the EDIFact message. These are recieved into a workflow by the GP system and remain there until they are filed into the patient record by a user. 

### EDIFact

The EDIFact message was defined by the Pathology Messaging Enabling Project and the specification can be found here listed as [EDIFact Pathology Messaging](https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections).

It is a detailed specification and although it does contain some coding the majority of the fields contain text. Some of the text is also heavily formatted,

**Include structured text table example**

Gp systems are required to maintian the text formatting in order to preserve the meaning. This will also be true of the GP Connect messaging, any structured text from the EDIFact report imported into the GP system **MUST** be maintained.

### Filing results into the patient record

When results are filed by the user it is possible to file the entire report, a 'test group' or an individual test.

Results may not always be filed on the day they were received. However in most GP systems the date the report is filed is the date against which it will appear in the patient record. As such this date is an important date when moving records between GP systems. 

At the point at which the record is filed there is opportunity for the user to provide comments against the report or part of the report that they are filing.

## Report structure

The following entity diagram describes the logical model for pathology in GP Connect, 

{: .center-image }
![Pathology logical model](images/access_structured/Pathology Logical Model.png)

In the image we have made the key entities more prominent so entities representing organizations and practitioners sit in the background but are still present.

As mentioned previously the 'Test Report Document' and 'Test Result Document' are out of scope for the current iteration but are represented in the diagram. 

We have modelled the pathology report in such a way that it will be able to support any data that is currently sent in the EDIFact message but also leaves room to send further data items as and when providing systems are able to support them. The model is also intended to be flexible enough to support the may different patterns and types of result that can be sent in one model so as to ensure consistency of structure.

## Available FHIR resources

There are a number of resources available in FHIR to represent the different entities that exist in pathology reporting. The resources that we are concerned with in order to represent our model are in the following table.

| Resource name       | Description | Used in GP Connect |
|---------------------|-------------------| ----------|
| [`ProcedureRequest`](accessrecord_structured_development_ProcedureRequest.html) | For requesting investigations to be performed by a laboratory | Yes |
| ['DiagnosticReport'](accessrecord_structured_development_DiagnosticReport.html) | A reporting structure that contains results and any relevant data such as specimen details or attribution | Yes |
| [`Specimen`](accessrecord_structured_development_Specimen.html) | Used to carry details about the specimen that was collected and used to run the investigations on | Yes |
| `Observation` | Used to represent details related to the test group header, test result and details of when a report or group of results was filed into the patient record| No |

There are other resources that may be relevant in the future, such as imagingStudy, imagingManifest and sequence, but currently we are only utilising the resources listed in the table.

### Using the FHIR profiles to represent the logical model 

We have mapped these resources on to the logical model in the diagram below,

{: .center-image }
![Pathology logical model with FHIR resource names](images/access_structured/Pathology Logical Model with FHIR resource names.png)

From the diagram you can see that the DiagnosticReport is at the centre of the model and that all the other entities are linked to from there. 

It is also possible to see how we have used the Observation resource for three different entities within the model. the test group header, test results and to contain any filing comments. Although we have used this resource in different settings there will be only one FHIR profile that can then be populated appropriately for each individual use.

There are detailed notes about how to populate each of these resources in the individual resource pages.




