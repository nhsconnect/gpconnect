---
title: Returning data in lists
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_lists_for_message_structure.html
summary: "Guidance for using lists to construcat a query response"
div: resource-page
---
## Using lists to return data in GP Connect

The bundle returned in response to a query for data in GP Connect structured uses lists to provide a structure that is easy for consumers to process. 

This page details how lists are used to create that structure. In this version of the GP Connect specifiaction there are 17 types of lists that can be returned and that are listed in the table below..

| Purpose | SNOMED Code |SNOMED Preferred Term / List.title|
| ------ | ------ |
|Medications and medical devices | 933361000000108| Medications and medical devices |
|Allergies and adverse reactions | 886921000000105| Allergies and adverse reaction  |
|Ended allergies | 1103671000000101| Ended allergies |
|Immunisations | 1102181000000102| Immunisations |
|List of consultations | 1149501000000101 | List of consultations |
|Consultations - medications related to Consultations |0000000|Meds related to Consultations|
|Consultations - allergies related to Consultations |0000000|Allergies related to Consultations|
|Consultations - ended allergies related to Consultations |0000000|Ended allergies related to Consultations|
|Consultations - immunisations related to Consultations |0000000|Immunisations to Consultations|
|Consultations - uncategorised data related to Consultations |0000000|Miscalaneous data related to Consultations|
|Problems | 717711000000103| Problems |
|Problems - medications related to problems |0000000|Meds related to problems|
|Problems - allergies related to problems |0000000|Allergies related to problems|
|Problems - ended allergies related to problems |0000000|Ended allergies related to problems|
|Problems - immunisations related to problems |0000000|Immunisations to problems|
|Problems - uncategorised data related to problems |0000000|Miscalaneous data related to problems|
|Uncategorised data | 826501000000100| Miscellaneous record |


