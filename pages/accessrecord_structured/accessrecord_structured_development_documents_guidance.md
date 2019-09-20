---
title: Documents
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_structured_development_documents_guidance.html
summary: "Guidance for the representation and consumption of documents"
---

## What is a document? ##

A clinical document (CD) is a written, printed or electronic record that provides evidence of medical care. Clinical documents must be accurate, timely and reflect specific services provided to a patient.
Clinical documentation is used to facilitate inter-provider communication, allow evidence-based healthcare systems to automate decisions, provide evidence for legal records and create patient registry functions so public health agencies can manage and research large patient populations more efficiently.

## Problem statement ##

A patient's GP practice is custodian of patient's clinical documents received from various health and care settings.
Other practices and healthcare settings are not able to electronically search for a patient's document in the patient's GP practice and retrieve those documents.
This is usually a manual process whereby other GP practices and healthcare settings ask a patient's GP practice for documents of the patient. The patient's GP practice then emails or faxes a patient's documents. This can lead to loss of valuable time and effort of GP practice's staff.

## Objective ##

Enable health and care organisations to electronically search for and retrieve patient's clinical documents from their GP practice.
Standardise the search and retrieval of clinical documents from the GP practices using GP Connect API Standards.

## As is ##

<IMG src="images/access_structured/As-Is.jpg" alt="As is process for search and retrieval of documents from a GP practice"  style="max-width:80%;max-height:80%;">

### Process steps

 <table width="80%" height="60%">
    <thead>
        <tr>
            <th>Id</th>
            <th>Title</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>1</td>
            <td>Send document</td>
            <td>Hospital sends document to the GP practice</td>
        </tr>
      <tr>
            <td>2</td>
            <td>Document upload to clinical system</td>
            <td>The document is manually or automatically uploaded to the clinical system of the GP practice.</td>
        </tr>
      <tr>
            <td>3</td>
            <td>Document matched to patient record</td>
            <td>The clinical system matches the document to the patient record.</td>
        </tr>
      <tr>
            <td>4</td>
            <td>File document</td>
            <td>Clinician views the document in their clinical system.</td>
        </tr>
      <tr>
            <td>5</td>
            <td>File document</td>
            <td>Clinician reads or meta data information to the document.</td>
        </tr>
      <tr>
            <td>6</td>
            <td>File document</td>
            <td>Clinician extracts read codes, add read code or annotates the document.</td>
        </tr>
      <tr>
            <td>7</td>
            <td>File document</td>
            <td>Clinician add the document to a workflow.</td>
        </tr>
      <tr>
            <td>8</td>
            <td>Request document</td>
            <td>Hospital request for a document of a patient from its registered GP practice.</td>
        </tr>
      <tr>
            <td>9</td>
            <td>Search document</td>
            <td>Clinician in a GP practice searches for the document.</td>
        </tr>
     <tr>
            <td>10</td>
            <td>Send document</td>
            <td>Clinician emails/faxes the document to the hospital. </td>
        </tr>
     <tr>
            <td>11</td>
            <td>View document</td>
            <td>Hospital receives and views the requested document.</td>
        </tr>
    </tbody>
</table>


### Known issues ###

   * Lack of versioning of documents in the GP practices. DateTime stamp is used to identify the latest version of the document.
   * No nationally agreed list of document types - GP practices have their own list of document types, which may also include free text.
   * Poor metadata of documents - GP systems have poor metadata information about documents.
   * Documents in disparate systems in a GP practice - documents metadata information and its versions may exist in disparate systems in a GP practice. However, documents and its basic information does sync back from document management systems to the clinical system.

## Scope ##

  <IMG src="images/access_structured/ARDocsScope.jpg" alt="Scope of documents"  style="max-width:60%;max-height:60%;">


## Use case ##

### a. Community pharmacist provides diabetes services ###

 **Scenario**

The community pharmacist provides a diabetes service. Providing this service to patients can reduce the workload on the local GP practice(s), so the practice(s) can focus on higher priority or more critical services or provide greater convenience to the patient and, thus, the local GP practice(s) refer patients to the community pharmacist.

**Actors**

Patient, community pharmacist, GP Connect APIs, community pharmacy IT system, GP practice IT system

**Main flow**

1.	The patient is referred to the pommunity pharmacist for diabetes service by the GP.
2.	The community pharmacist wants to view certain clinical documents of the patient.
3.	The community pharmacist accesses GP Connect to search for information about matching clinical documents from the patient’s registered GP practice system.
4.	GP Connect requests metadata information about clinical documents from the GP clinical system and presents it to the community pharmacy system.
5.	The community pharmacists view this information and request to view a clinical document from the GP practice system via GP Connect.
6.	Community pharmacy system receives binary of the requested document and presents it in a readable format
7.	The community pharmacist views the clinical document and uses this information to assist their treatment of the patient.


### b. Paramedic accesses Do Not Attempt Resuscitation (DNAR) document ###

**Scenario**

A paramedic is visiting a patient who has collapsed at home and needs to ascertain whether the patient has a Do Not Attempt Resuscitation order recorded on the GP system, and the date it was recorded.  Ideally, the paramedic would be able to see DNR history and associated information such as whether the patient and family are aware of the decision.  
They should also be able to access an uploaded DNAR document, if it exists.

**Actors**

Paramedic, paramedic's IT system, patient, GP Connect APIs, GP practice IT system

**Main flow**

1.	Paramedic accesses patient information on their mobile EPR.
2.	The paramedic wants to view DNAR document of the patient to understand patient’s consent to resuscitate or not.
3.	Paramedic's system accesses GP Connect to search for information about any DNAR document of the patient from their registered GP practice’s clinical system.
4.	GP Connect requests metadata information about matching documents of the patient from the GP practice system and presents it to the paramedic’s system.
5.	The paramedic views the metadata information of matching documents on their system and requests to view the DNAR document from the GP practice system via GP Connect.
6.	The paramedic's system receives the binary of the document and presents it in a readable format.
7.	The paramedic views the DNAR document and uses this information to assist their treatment of the patient.

## Documents classification ##
Document types vary across GP practices and may contain free text. Requirements analysis and Professional Record Standards Body (PRSB) documentation identifies a demand for a clear classification of documents.
To address this issue, GP Connect has created a valueset of document types. It is based on the clinical document indexing standards created by NHS Scotland. Providers would map their document types to the GP Connect document types valueset. Where the providers have a code that does not exist in the value set, they can provide their code and its value in the text field. This would improve the standardisation of document types across the GP practices.

## Patient records where documents are not available ##
GP clinical systems may have some migrated patient records that have information about the document but the document is not available to the clinical system. To resolve this, GP Connect APIs would return a placeholder for the document specifying that there is a document but it is not available. The metadata information about the document would provide information about the authoring organisation of the document from where the document can be requested.

## Document format ##
Providers to provide documents in the following industry acceptable format:
* Plain Text (text/plain) - .txt
* HTML Text (text/html) - .html, .htm
* PDF (application/pdf) - .pdf
* XML Text (text/xml) - .xml
* RTF Text (text/rtf) - .rtf, .rtx
* Basic Audio (audio/basic) - .au
* PNG Image (image/png) - .png
* GIF Image (image/gif) - .gif
* JPEG Image (image/jpeg) - .jpg, .jpe, .jpeg
* TIFF Image (image/tiff) - .tif, .tiff
* MSWORD (application/msword) - .doc
* MSWORD (application/vnd.openxmlformats-officedocument.wordprocessingml.document) - .docx
* DICOM

## Multiple versions of the document ##
A GP practice may have multiple versions of the same document of the patient in their clinical system. Providers would only return latest version of the document via the GP Connect APIs.

## Internal or external documents ##
The GP practice from which the document is being requested is the custodian of the document. Requirements analysis suggest that end-users would like to understand if the patient document that they are retrieving from the GP practice is an internally generated document in the GP practice or an external organisation has sent that document to the GP practice.
If the 'Authoring Organisation' of the document is same as custodian of the document then it's an internally generated document.
If the 'Authoring Organisation' of the document is NOT the same as custodian of the document then it's an externally generated document.

## File size of the document ##
End-users would like to know the size of the document before retrieving the document. Providers would return the file size of the document in the response payload for Search Document GP Connect API request.

## Multiple systems/providers being used in a GP practice to manage documents ##
A GP practice may use document management systems for managing documents besides the clinical systems. The documents held in document management system sync to the clinical system along with its basic information such as document type, clinical setting, organisation, description and date. Any read codes extracted in the document management system is also synced to the clinical system. This is done so that, in case when the document management system is unavailable, the document is still available in the principal clinical system and vice versa.
GP Connect APIs would search for documents and retrieve documents only from the clinical system.



