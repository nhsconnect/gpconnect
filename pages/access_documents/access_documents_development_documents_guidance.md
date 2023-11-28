---
title: Documents guidance
keywords: getcarerecord
tags: [getcarerecord]
sidebar: access_documents_sidebar
permalink: access_documents_development_documents_guidance.html
summary: "Guidance for the representation and consumption of documents"
---

## What is a document? ##

A clinical document (CD) is a written, printed or electronic record that provides evidence of medical care. Clinical documents must be accurate, timely and reflect specific services provided to a patient. A clinical document could be any document that the GP practice adds to a clinical record of the patient.

## Problem statement ##

A patient's registered GP practice is considered to be a custodian of its clinical documents received from various health and care settings.
Other practices and healthcare settings are not able to electronically search for a patient's document in the patient's registered GP practice and retrieve those documents.
This is usually a manual process whereby other GP practices and healthcare settings ask a patient's GP practice for documents of the patient. The patient's GP practice then emails or faxes a patient's documents. This can lead to loss of valuable time and effort of GP practice's staff.
GP practices have poor metadata of clinical documents and it makes it difficult for the clinicians to search the documents in the GP Practice.

## Objective ##

Enable health and care organisations to electronically search for and retrieve patient's clinical documents from their GP practice.
Standardise the search and retrieval of clinical documents from the GP practices using GP Connect API standards.

## As is ##

<IMG src="images/access_documents/As-Is.jpg" alt="As is process for search and retrieval of documents from a GP practice"  style="max-width:80%;max-height:80%;">

### Process steps

| Id | Title                              | Description                                                                                   |
| -- | -----                              | -----------                                                                                   |
| 1  | Send document                      | Hospital sends document to the GP practice.                                                   |
| 2  | Document upload to clinical system | The document is manually or automatically uploaded to the clinical system of the GP practice. |
| 3  | Document matched to patient record | The clinical system matches the document to the patient record.                               |
| 4  | File document                      | Clinician views the document in their clinical system.                                        |
| 5  | File document                      | Clinician reads or adds meta data information to the document.                                |
| 6  | File document                      | Clinician extracts read codes, adds read code or annotates the document.                      |
| 7  | File document                      | Clinician adds the document to a workflow.                                                    |
| 8  | Request document                   | Hospital request for a document of a patient from its registered GP practice.                 |
| 9  | Search document                    | Clinician in a GP practice searches for the document.                                         |
| 10 | Send document                      | Clinician emails/faxes the document to the hospital.                                          |
| 11 | View document                      | Hospital receives and views the requested document.                                           |

### Known issues ###

* Lack of versioning of documents in the GP practices. DateTime stamp is used to identify the latest version of the document.
* No nationally agreed list of document types - GP practices have their own list of document types, which may also include free text.
* Poor metadata of documents - GP systems have poor metadata information about documents.
* Documents in disparate systems in a GP practice - Documents metadata information and its versions may exist in disparate systems in a GP practice. However, documents and its basic information does sync back from document management systems to the clinical system.

## Value proposition ##

 <IMG src="images/access_documents/ValueProp.png" alt="Value Proposition"  style="max-width:100%;max-height:80%;">

## Scope ##

  <IMG src="images/access_documents/ARDocsScope.JPG" alt="Scope of documents"  style="max-width:60%;max-height:60%;">

## Use case ##

<IMG src="images/access_documents/DistrictNursePatient.png" alt="District nurse attends a patient at home and views their discharge summary"  style="max-width:73%;max-height:60%;">

## Document Type ##

Document types vary across GP practices and may contain free text.
Requirements analysis and Professional Record Standards Body (PRSB) documentation identifies a demand for a clear classification of documents.
To address this issue, GP Connect recommends the use of the 'Record composition type simple reference set (foundation metadata concept)' with Refset Id 1127551000000109.
A text value can be provided for values that do not exist in the valueset.

## Patient records where documents are not available ##

GP clinical systems may have some patient records that have information about the document but the document may not be available to the clinical system. To resolve this, GP Connect APIs should return a placeholder for the document specifying that there is a document but it is not available. The metadata information about the document should provide information about the authoring organisation of the document. More information about how this should be populated is available on the [DocumentReference page](access_documents_development_documentreference.html#contentattachmenttitle).

## Document format ##

Documents of industry standard format are allowed. Any local document formats are not allowed.

## Multiple versions of the document ##

A GP practice may have multiple versions of the same document of the patient in their clinical system. Providers shall only return latest version of the document via the GP Connect APIs.

## Internal or external documents ##

The GP practice from which the document is being requested is the custodian of the document. Requirements analysis suggests that end-users would like to understand if the patient document that they are retrieving from the GP practice is an internally generated document in the GP practice or an external organisation has sent that document to the GP practice.
If the 'Authoring Organisation' of the document is the same as the custodian of the document then it's an internally generated document.
If the 'Authoring Organisation' of the document is NOT the same as the custodian of the document then it's an externally generated document.

## File size of the document ##

End-users would like to know the size of the document before retrieving the document. Providers return the size of the document in the response payload to the API requests that are made prior to retrieving a document. The information is contained in `content.attachment.size` on the [DocumentReference](access_documents_development_documentreference.html) resource. The API calls made prior to retrieving a document are:

* [Search for a patient's documents](access_documents_development_search_patient_documents.html) for standard document retrieval
* [Migrate a patient's structured record](accessrecord_structured_development_migrate_patient_record.html) for patient migration document retrieval

When retrieving documents through the [Retrieve a document](access_documents_development_retrieve_patient_documents.html) API the document **MUST NOT** be larger than 5MB.
If a document exceeds 5MB a placeholder should be returned specifying that the document hasn't been returned due to its file size. This is achieved by populating the `content.attachment.title` property of the [DocumentReference](access_documents_development_documentreference.html).

There is no such limitation on the size of documents able to be retrieved through the [Migrate a document](access_documents_development_migrate_patient_documents.html) API.

## Multiple systems/providers being used in a GP practice to manage documents ##

A GP practice may use document management systems for managing documents besides the clinical systems. The documents held in document management system sync to the clinical system along with its basic information such as document type, clinical setting, organisation, description and date. Any read codes extracted in the document management system is also synced to the clinical system. This is done so that, in the case when the document management system is unavailable, the document is still available in the principal clinical system and vice versa.
GP Connect APIs would search for documents and retrieve documents only from the clinical system.

## Document Status ##

Document Status would always have default value of 'current' as only the latest version of the document is retrievable from a GP practice.

## Confidential Documents ##

GP Connect APIs are currently restricted to search and retrieval of documents that have NO internal confidentiality policy applied, but may in future expand to include all documents subject to data controller determination of who can access documents from the clinical record that has confidentiality/protection policy applied.

## Unreviewed Documents ##

GP Connect APIs allow search and retrieval of documents that have not been reviewed and filed. It would enable the health and care workers to have access to the required documents at the right time and take informed decisions with the patient for their health and  care.
It has been considered that there is the possibility that some of the unreviewed documents might be deemed and subsequently marked confidential at clinical review, but at this stage the clinical safety and continuity concerns outweigh the small risk of disclosure of data that may merit consideration of confidentiality policy application.

## Documents for deceased patients ##

GP Connect APIs **MAY** allow for search and retrieval of documents for deceased patients for a period of 28 days after the patient’s death.
The providers **MUST** allow for the period to be configurable. If a request is received after this period, the providers **MUST** return an error as per [error handling](access_documents_use_case_find_a_patient#error-handling). The providers **MUST** return a deceased patient’s record only if the patient was a main GMS registered patient prior to being de-registered due to death.
