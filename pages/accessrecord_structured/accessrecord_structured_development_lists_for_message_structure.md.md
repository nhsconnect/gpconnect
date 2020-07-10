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

In GP Connect it is used to organise data returned by a query into groups of resources that can then be processed more easily. For each clinical area query, GP Connect will return a list that identifies the data returned for that query. This is considered to be the primary list relating to that area.

- When an API call returns data for more than one clinical area, the list will identify which data has been returned for which clinical area.
- Where there are no items returned, the primary list will be returned empty.
- Where the return includes warning codes for example, to indicate when clinical data is excluded, those codes will be included in any list profile the item would have been present in.

When either problems or consultations are requested then in addition to the primary list the response will contain further secondary lists which detail resources that are contained in the requested consultations or have been linked to the the problems that are returned.

The list containing resolved allergies is a special case as it is a list that is contained within the allergies list. This is a safetey precaution intended to reduce the risk of resolved allergies being confused with active allergies. Further details about how the allergies lists work can be found on the allergies guidance page. **insertlink to allergy page**

In this version of the GP Connect specifiaction there are 30 types of lists containing data that can be returned and that are listed in the table below. 

| Purpose | SNOMED Code |SNOMED Preferred Term / List.title|
| ------ | ------ |
|Allergies and adverse reactions | 886921000000105| Allergies and adverse reaction  |
|Allergies that have been ended | 1103671000000101| Ended allergies |
|Consultations | 1149501000000101 | List of consultations |
|Consultations - allergies contained in Consultations |0000000|Allergies contained in Consultations|
|Consultations - allergies that have been ended contained in Consultations |0000000|Ended allergies contained in Consultations|
|Consultations - Diary entries contained in Consultations |0000000|Diary entries contained in Consultations|
|Consultations - Documents contained in Consultations |0000000|Documents contained in Consultations|
|Consultations - immunisations contained in Consultations |0000000|Immunisations contained in Consultations|
|Consultations - investigations contained in Consultations |0000000|Investigations contained in Consultations|
|Consultations - medications contained in Consultations |0000000|Medications and medical devices contained in Consultations|
|Consultations - Outbound referrals in Consultations |0000000|Outbound referrals contained in Consultations|
|Consultations - Problems contained in Consultations |0000000|Miscalaneous data contained in Consultations|
|Consultations - uncategorised data contained in Consultations |0000000|Miscalaneous data contained in Consultations|
|Diary Entries | 714311000000108 | Patient recall administration |
|Immunisations | 1102181000000102| Immunisations |
|Investigations | 887191000000108| Investigations and Results |
|Medications and medical devices | 933361000000108| Medications and medical devices |
|Outbound Referrals | 792931000000107| Outbound referral 
|Problems | 717711000000103| Problems |
|Problems - allergies related to problems |0000000|Allergies related to problems|
|Problems - allergies that have been ended related to problems |0000000|Ended allergies related to problems|
|Problems - consultations related to problems |0000000|Consultations related to problems|
|Problems - diary entries related to problems |0000000|Diary entries related to problems|
|Problems - documents related to problems |0000000|Documents related to problems|
|Problems - immunisations related to problems |0000000|Immunisations related to problems|
|Problems - investigations related to problems |0000000|Investigations related to problems|
|Problems - medications related to problems |0000000|Medications and medical devices related to problems|
|Problems - outbound referrals related to problems |0000000|Outbound referrals related to problems|
|Problems - uncategorised data related to problems |0000000|Miscalaneous data related to problems|
|Uncategorised data | 826501000000100| Miscellaneous record |

NB lists are also used to structure consultations, how this works is detailed here **Add link to List use in consultations**

## Using lists to respond to queries for consultations and problems

Represnting data that is returned in relation to both consultations and problems requires a response that is able to return multiple types of data, a consultation may contain any type of clinical data that can be entered into a GP system and a problem can be linked to any type of data that can be entered into a GP system.

In GP Connect we use secondary lists to contain these contained or linked items. When either of these clinical areas is queried then up to 10 secondary lists may be returned. Each of these list is detailed in the above table. These lists will only be returned where data exists in the clinical system that is returned as part of the query. If no data suitable to populate a list is present in the record that is being sent then the list will not be included in the response. For example if a query was made to GP Connect for all problems in a record but none of these problems related to an outbound referral, then there would be no list for 'Outbound referrals related to problems' contained in the response.

 - Secondary lists will only be present where problems or consultations clinical areas have been queried directly
 - Secondary lists will only be present where data is available
 - Secondary lists will contain the appropriate warning code(s) where information has been excluded
 - 

## Warning codes

Warning codes are used to manage negation where resources are present in a system to be returned by a query but are not included in the returned data for a specific reason.

Warning codes will be returned in the list when any item that would have been included in that list as a response to the query is not present due to one of the defined reasons. In the case where an item may have been present in more than one list, e.g. medications and medications related to problems, the warning code will be present in both lists. Any warning codes returned will be contained in the extension List.extension[warningCode].

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
