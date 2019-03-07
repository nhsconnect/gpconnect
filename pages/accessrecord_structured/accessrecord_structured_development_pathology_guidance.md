---
title: Pathology guidance
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_pathology_guidance.html
summary: "Guidance on the representation of allergies and intolerances in GP Connect"
---

# Investigations Modeling

## Patholgy Reporting in GP Practices

Currently GP practices receive the majority of the results of investigations that they have requested in the form of the EDIFact message. These are recieved into a workflow by the GP system and remain there until they are filed into the patient record by a user.

It should be noted that in GP systems it is possible to manually enter pathology result codes as individual items that may have a value and other qualifiers associated with them

### EDIFact

The EDIFact message was defined by the Pathology Messaging Enabling Project and the specification can be found here listed as [EDIFact Pathology Messaging](https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections).

It is a detailed specification and although it does contain some coding the majority of the fields contain text. Some of the text is also heavily formatted,

**Include structured text table example**

Gp systems are required to maintian the text formatting in order to preserve the meaning. This will also be true of the GP Connect messaging, any structured text from the EDIFact report imported into the GP system **MUST** be maintained.

## Report structure

The following entity diagram describes the logical model for pathology in GP Connect, 

{: .center-image }
![Pathology logical model](images/access_structured/Pathology Logical Model.png)



## Available FHIR resources

| Resource name       | Description | Used in GP Connect |
|---------------------|-------------------| ----------|
| [`ProcedureRequest`](accessrecord_structured_development_ProcedureRequest.html) | For requesting investigations to be performed by a laboratory | Yes |
| ['DiagnosticReport'](accessrecord_structured_development_DiagnosticReport.html) | A reporting structure that contains results and any relevant data such as specimen details or attribution | Yes |
| [`Specimen`](accessrecord_structured_development_Specimen.html) | Used to carry details about the specimen that was collected and used to run the investigations on | Yes |
| `Observation` | Used to represent details related to the test group header, test result and details of when a report or group of results was filed into the patient record| No |

### Using the FHIR profiles to represent the logical model 

{: .center-image }
![Pathology logical model with FHIR resource names](images/access_structured/Pathology Logical Model with FHIR resource names.png)



## Filing Reports

It is possible to file 



