---
title: Returning data in lists
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_lists_for_message_structure.html
summary: "Guidance for using lists to construcat a query response"
div: resource-page
---
## Using lists to return data in GP Connect ##

The `List` resource in FHIR is used to manage collections of resources.

In GP Connect it is used to organise data returned by a query into groups of resources that can then be processed more easily. For each clinical area query, GP Connect will return a list that identifies the data returned for that query.

When either problems or consultations are requested then it will contain further lists which detail resources that are contained in the requested consultations or have been linked to the the problems that are returned.

- When an API call returns data for more than one clinical area, the list will identify which data has been returned for which clinical area.
- Where problems or consultations are requested lists will be supplied for each clinical area that has data contained in/linked to the conultations or problems returned
- Where there are no items returned, the list will be empty.
- Where the return includes warning messages (for example, when clinical data is excluded), those messages will be in the list profile.manage negation where no resources are present in a system to be returned by a query. An attribution that is common to the resources it references will be returned, differentiating between items at different stages of a workflow, providing a mechanism to deal with warnings that can be applied to the group of resources.

In this version of the GP Connect specifiaction there are 19 types of lists containing data that can be returned and that are listed in the table below. NB lists are also used to structure consultations, how this works is detailed here 

| Purpose | SNOMED Code |SNOMED Preferred Term / List.title|
| ------ | ------ |
|Allergies and adverse reactions | 886921000000105| Allergies and adverse reaction  |
|Allergies that have been ended | 1103671000000101| Ended allergies |
|Consultations | 1149501000000101 | List of consultations |
|Consultations - medications contained in Consultations |0000000|Meds related to Consultations|
|Consultations - allergies contained in Consultations |0000000|Allergies related to Consultations|
|Consultations - ended allergies contained in Consultations |0000000|Ended allergies related to Consultations|
|Consultations - immunisations contained in Consultations |0000000|Immunisations to Consultations|
|Consultations - uncategorised data contained in Consultations |0000000|Miscalaneous data related to Consultations|
|Consultations - Problems contained in Consultations |0000000|Miscalaneous data related to Consultations|
|Medications and medical devices | 933361000000108| Medications and medical devices |
|Immunisations | 1102181000000102| Immunisations |
|Problems | 717711000000103| Problems |
|Problems - medications related to problems |0000000|Meds related to problems|
|Problems - allergies related to problems |0000000|Allergies related to problems|
|Problems - ended allergies related to problems |0000000|Ended allergies related to problems|
|Problems - immunisations related to problems |0000000|Immunisations to problems|
|Problems - uncategorised data related to problems |0000000|Miscalaneous data related to problems|
|Problems - consultations related to problems |0000000|Consultations related to problems|
|Uncategorised data | 826501000000100| Miscellaneous record |

## Warning codes

The following table provides details of the warning codes that are to be used in the warningCode extension in GP Connect. More guidance for each code follows in the subsequent sections.

<table class='resource-attributes' border='1'>
  <tr>
    <td>Display</td>
    <td>Code</td>
    <td>Associated text</td>
  </tr>
  <tr>
    <td>Confidential Items</td>
    <td>confidential-items</td>
    <td>Items excluded due to confidentiality and/or patient preferences.</td>
  </tr>
  <tr>
    <td>Data in Transit</td>
    <td>data-in-transit</td>
    <td>Patient record transfer from previous GP practice not yet complete; information recorded before dd-Mmm-yyyy may be missing.</td>
  </tr>
</table>

### Confidential items

Where items have been excluded from the returned resources due to patient consent preferences or as they are part of the exclusion dataset this **MUST** be indicated at the list level. If an item that would have been an entry in a list is excluded the warningCode field **MUST** be populated using the confidential items warning code from the above table. The associated text **MUST** also be added into the note field when the code is used.

Note: If the results of a search contained only confidential items, it would present as an `List` with no entries, an `emptyReason` and the Confidential Items warning code.

### Data in transit

This only refers to data transmitted from GP to GP when a patient moves GP practice. This is where a patient is registered at their new GP practice but their medical records from their previous GP practice have not yet been received and/or incorporated into their new GP practice system. When this takes place all the lists returned **MUST** be populated using the data in transit warning code from the above table. The associated text **MUST** also be added into the note field when the code is used. Set dd-mmm-yyyy to the date the patient registered at their new GP practice.

## Data awaiting filing

When a GP Clinical system receives electronic data about a patient it will go through filing process during which the information is reviewed by a user and if suitable integrated into the patient's medical record. The details on how this process is managed vary between different GP Clinical Systems and GP Practices.

GP Connect will not return electronic data that has been received by the GP Clinical System but has not yet been through the filing process. The data will only become available through GP Connect once it has integrated into the patient's medical record.
