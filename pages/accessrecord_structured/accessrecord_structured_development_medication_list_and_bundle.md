---
title: List and bundle
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication_list_and_bundle.html
summary: "Details of the lists and bundles used in Access Record Structured"
---
## Using the bundle resource

GP Connect has not created a separate bundle profile and will use the standard FHIR&reg; bundle to contain the resources returned for a query. The bundle **SHOULD** have the type set to ‘collection’ and contain all the relevant resources as per the standard FHIR guidance, which can be accessed on the [HL7 website.](http://hl7.org/fhir/bundle.html).

## Using the list resource

The list resource in FHIR is used to help manage a collection of resources. In GP Connect it is used to identify the data returns for each query. For each clinical area query, GP Connect will return one or more predefined list that identifies the data returned for that query.

- When multiple queries in the same API call return data in the same profile, the list will identify which data in the profile has been returned for which query.
- Where there are no items returned, the list will be empty.
- Where the return includes warning messages (for example, when clinical data is excluded), those messages will be in the list profile.manage negation where no resources are present in a system to be returned by a query. An attribution that is common to the resources it references will be returned, differentiating between items at different stages of a workflow, providing a mechanism to deal with warnings that can be applied to the group of resources.

{% include note.html content=" The List resource is still in the process of being curated and may be subject to change depending on the outcome of the curation process. Codes to populate the code and warningCode fields are yet to be confirmed but will be added to the guidance shortly." %}

### Confidential items

Where items have been excluded from the returned resources due to patient consent preferences or as they are part of the exclusion dataset this **SHOULD** be indicated at the list level. If an item that would have been an entry in a list is excluded the warningCode field **SHOULD** be populated using the confidential items warning code.

### Data in transit

This only refers to data transmitted from GP to GP when a patient moves GP practice. This is where a patient is registered at their new GP practice but their medical records from their previous GP practice has not yet been received and/or incorporated into their new GP practice system. When this takes place all the lists returned will have the data in transit warning code in the warningcode field.

### Data awaiting filing

Where data exists in a provider system workflow that would have been included as part of the bundle returned had it been integrated in the system, then this **SHOULD** be sent in a separate list to the rest of the entries. The list **SHOULD** be sent using the appropriate list.code relevant to the type of resource that it contains as defined in the guidance for that resource group and contain the warningCode for data awaiting filing.
This will allow consuming systems to be able to display the data and indicate that it has not been reviewed by an appropriate person at the providing practice.

### List profile population

| Element  | Usage | Datatype | Optionality | Guidance 
|----------|-------|----------|:-----------:|---------------------------------
|`identifier`|Unique identifier for the list|`identifier`|O||
|`Status`|Whether the list is current/retired/entered-in-error|`Code`|M|'current' for all lists to be used in GP Connect.|
|`mode`|Whether the list is working/snapshot/changes|`Code`|M|Fixed value of 'snapshot' for GP Connect.|
|`title`|Descriptive name for the list|`Code`|O|To use PRSB SNOMED CT ref set of codes and corresponding human readable description in string.
|`code`|The purpose of the list|`Code`|M|The relevant code is specified in the guidance for each of the profiles. (list of codes to be confirmed) 
|`subject`|Reference to the patient|`Reference`|M|
|`encounter`|Reference to a relevant encounter|`Reference`|O|DO NOT USE - items in lists in GP Connect may be relevant to multiple encounters.
|`date`|When the list was created|`dateTime`|O|
|`source`|Who and/or what defined the list contents (aka Author) |`Reference (Practitioner, Patient, Device)`|O|
|`orderedBy`|What order the list has|`CodeableConcept`|O|As the data where lists are being used in GP Connect is structured it is simple for the consumer to put it in an order.
|`note`|Comments about this list|`Annotation`|R|
|`warningCode`|A code warning of an issue related to this list|`CodeableConcept`|R|This extension is used to capture warnings that the list may be incomplete as data has been excluded due to confidentiality or may be missing due to data being in transit.
|`entry`|Entries in the list|`BackBoneElement`|R|
|`entry.flag`||`CodeableConcept`|O|DO NOT USE - no use defined in the current version of GP Connect.
|`entry.deleted`|If this item is actually marked as deleted|`Boolean`|O|DO NOT USE - deleted items **SHOULD NOT** be returned by providers as part of GP Connect.
|`entry.date`|When the item was added to the list|`dateTime`|O|As GP Connect represents a snapshot at the time the request was made by the consuming system this is not required to be populated.
|`entry.item`|Actual entry|`Reference`|R|Reference to the item that is part of the list.
|`emptyReason`|Why the list is empty|`CodeableConcept`|R|A null flavour of noContent **SHOULD** be used if a query returns no results to enter into a list.
