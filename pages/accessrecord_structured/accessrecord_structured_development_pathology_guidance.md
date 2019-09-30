---
title: Investigations guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_pathology_guidance.html
summary: "Guidance on the representation of EDIFACT messaging in GP Connect"
---

## Investigations scope in GP Connect

For this version of the specification the scope of investigations is considered to be making available any investigations results contained in GP systems that have been received from the lab by an EDIFACT message.

As such, there are a number of items that are **NOT** currently in scope. These are as follows:

* investigations results that have been entered in a GP system using a code as an individual item (these may have a value and other qualifiers associated with them)
* test results that are received as documents or images
* making available any test requests
* providing the original test report document as it was provided to the practice
* any other numeric results that do not form part of an EDIFACT message (blood pressure

These may be addressed in future versions or within different areas of GP Connect - for example, manually entered results will be dealt with when we curate the uncategorised data in GP systems contained in the journal or care history areas.

## Use of language to describe investigation reports

When describing investigation reports, different regions and professions sometimes use different words to describe the same entities. Therefore, for avoidance of confusion there are a couple of terms that we need to define.

* Test group - is the phrase we are using to describe any group of tests that has been created by the laboratory or other providing organisation. These are often referred to as batteries, panels and profiles.

* Test result - this is the result that has been provided by the laboratory or other provider. These may be standalone results or may be a part of a 'Test group'. They are also sometimes referred to as test analytes.

## Investigation reporting in GP practices

Currently GP practices receive the majority of the results of investigations which they have requested in the form of the EDIFACT message. These are received into a workflow by the GP system and remain there until they are filed into the patient record by a user.

### EDIFACT

The EDIFACT message was defined by the Pathology Messaging Enabling Project and the specification can be found here listed as [EDIFact Pathology Messaging](https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections).

It is a detailed specification and although it does contain some coding the majority of the fields contain text. Some of the text is also heavily formatted. See below example taken from a GP2GP HL7v3 message:

{: .center-image }
![Structured text example](images/access_structured/Pathology_structured_text_example_2.png)

GP systems are required to maintain the text formatting in order to preserve the meaning. This will also be true of the GP Connect messaging, any structured text from the EDIFACT report imported into the GP system **MUST** be maintained as they are in the GP2GP HL7 message.

### Filing results into the patient record

When results are filed by the user it is possible to file the entire report or a 'test group'.

Results may not always be filed on the day they were received. However, in most GP systems the date the report is filed is the date against which it will appear in the patient record. As such, this date is an important date when moving records between GP systems.

At the point at which the record is filed, there is opportunity for the user to provide comments against the report or part of the report that they are filing.

## Report structure

The following entity diagram describes the logical model for investigations in GP Connect:

{: .center-image }
![Pathology logical model](images/access_structured/Pathology_Logical_Model.png)

In the image we have made the key entities more prominent. Entities representing organizations and practitioners sit in the background but are still part of the exported data.

|Entity Name |Description |
|------------|--------------|
|Test Report |	The summary data from the test report including the clinical interpretation|
|Test Group	|Output from a group of tests including the clinical interpretation|
|Test Result|Output from a single test including the clinical interpretation|
|Specimen	|Information on the specimen tested|
|Test Report Filing	|Information recorded by the general practice clinician when they file the test report|
|Test Request Summary	|A summary of the original test request that is returned with the test report|
|Test Report Document	|The test report in the format it was received by the GP practice|
|Test Result Document	|Documents that form part of the test results (for example, images and charts)|

The 'Test Report Document' and 'Test Result Document' are out of scope for the current iteration, but are represented in the diagram.

We have modelled the investigations report in such a way that it will be able to support any data that is currently sent in the EDIFACT message and also leaves room to send further data items as and when providing systems are able to support them. The model is also intended to be flexible enough to support the many different patterns and types of result that can be sent so it can be easily adapted to support other test results stored in the GP system.

### Available FHIR resources

There are a number of resources available in FHIR to represent the different entities that exist in investigation reporting. The resources that we are concerned with in order to represent our model are in the following table.

| Resource name       | Description |
|---------------------|-------------------|
| [`ProcedureRequest`](accessrecord_structured_development_ProcedureRequest.html) | For requesting investigations to be performed by a laboratory |
| [`DiagnosticReport`](accessrecord_structured_development_DiagnosticReport.html) | A reporting structure that contains results and any relevant data such as specimen details or attribution |
| [`Specimen`](accessrecord_structured_development_Specimen.html) | For carrying details about the specimen that was collected and the investigations were performed on |
| [`Observation`](accessrecord_structured_development_observation_testgroup.html) |Represents details related to the test group header, test result and details of when a report or group of results was filed into the patient record|

There are other resources that may be relevant in the future, such as imagingStudy, imagingManifest and sequence, but currently we are only utilising the resources listed in the table.

### Using the FHIR profiles to represent the logical model

We have mapped these resources on to the logical model in the diagram below:

{: .center-image }
![Pathology logical model with FHIR resource names](images/access_structured/Pathology_Logical_Model_with_FHIR_resource_names.png)

DiagnosticReport is at the centre of the model and all the other entities are linked to from there.

The `Observation` resource is used for three different entities within the model. The test group header, test results and to contain any filing comments. Although we have used this resource in different settings, there will be only one FHIR profile that can then be populated appropriately for each individual use.

There are detailed notes about how to populate each of these resources in the individual resource pages.

## Using the `List` resource for investigations queries

The results of a query for investigations **MUST** return a `List` containing references to all the `DiagnosticReport` resources to represent each investigation report that is returned. The list code **MUST** be set to `887191000000108` for `Investigations and results`.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason` with the value `noContent`.
