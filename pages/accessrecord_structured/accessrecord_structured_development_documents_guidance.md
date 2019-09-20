---
title: Documents
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_documents_sidebar
permalink: accessrecord_structured_development_documents_guidance.html
summary: "Guidance for the representation and consumption of documents"
---

## What is a Document ##

A clinical document (CD) is a written, printed or electronic record that provides evidence of medical care. Clinical documents must be accurate, timely and reflect specific services provided to a patient.
Clinical documentation is used to facilitate inter-provider communication, allow evidence-based healthcare systems to automate decisions, provide evidence for legal records and create patient registry functions so public health agencies can manage and research large patient populations more efficiently.

## Problem Statement ##

A Patient's GP Practice is custodian of Patient's clinical documents received from various health and care settings.
Other Practices and health care settings are not able to electronically search for a Patient's document in the Patient's GP practice and retrieve those documents.
This is usually a manual process whereby other GP Practices and Health care settings ask a Patient's GP Practice for documents of the Patient. The Patient's GP Practice then emails or faxes a Patient's documents. This can lead to loss of valuable time and effort of GP Practice's staff.

## Objective ##

Enable health and care organisations to electronically search for and retrieve Patient's clinical documents from their GP Practice.
Standardise the search and retrieval of clinical documents from the GP Practices using GPConnect API Standards.

## As Is ##

<IMG src="images/access_structured/As-Is.jpg" alt="As-Is process for search and retrieval of documents from a GP Practice"  style="max-width:80%;max-height:80%;">

### Process Steps

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
            <td>Hospital sends document to the GP Practice</td>
        </tr>
      <tr>
            <td>2</td>
            <td>Document upload to clinical system</td>
            <td>The document is manually or automatically uploaded to the Clinical System of the GP Practice.</td>
        </tr>
      <tr>
            <td>3</td>
            <td>Document matched to patient record</td>
            <td>The clinical System matches the document to the patient record.</td>
        </tr>
      <tr>
            <td>4</td>
            <td>File document</td>
            <td>Clinician views the document in their clinical system</td>
        </tr>
      <tr>
            <td>5</td>
            <td>File document</td>
            <td>Clinician reads or meta data information to the document</td>
        </tr>
      <tr>
            <td>6</td>
            <td>File document</td>
            <td>Clinician extracts read codes, add read code or annotates the document.</td>
        </tr>
      <tr>
            <td>7</td>
            <td>File document</td>
            <td>Clinician add the document to a workflow</td>
        </tr>
      <tr>
            <td>8</td>
            <td>Request document</td>
            <td>Hospital request for a document of a Patient from it’s registered GP Practice</td>
        </tr>
      <tr>
            <td>9</td>
            <td>Search document</td>
            <td>Clinician in a GP Practice searches for the document</td>
        </tr>
     <tr>
            <td>10</td>
            <td>Send document</td>
            <td>Clinician emails/faxes the document to the Hospital </td>
        </tr>
     <tr>
            <td>11</td>
            <td>View document</td>
            <td>Hospital receives and views the requested document</td>
        </tr>
    </tbody>
</table>

### Multiple versions of the document Scenarios

 1.	A GP Practice receives multiple versions of the same document

<table width="60%" height="30%">
    <thead>
        <tr>
            <th>Doc Id</th>
            <th>System </th>
            <th>Version</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>D1</td>
            <td>Clinical System</td>
            <td>v1</td>
        </tr>
      <tr>
            <td>D1</td>
            <td>Clinical System</td>
            <td>v2</td>
        </tr>
    </tbody>
    </table>

 2. A document is received in a Clinical System, it is then annotated and saved in the Document Management System.

<table width="60%" height="30%">
    <thead>
        <tr>
            <th>Doc Id</th>
            <th>System </th>
            <th>Version</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>D1</td>
            <td>Clinical System</td>
            <td>v1</td>
        </tr>
      <tr>
            <td>D1</td>
            <td>Doc Management System</td>
            <td>v2</td>
        </tr>
    </tbody>
    </table>

  3. A document is received in a Clinical System, it is then annotated and saved in the Document Management System. When the workflow is complete, it is then sent to the clinical system.

 <table width="60%" height="30%">
    <thead>
        <tr>
            <th>Doc Id</th>
            <th>System </th>
            <th>Version</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>D1</td>
            <td>Clinical System</td>
            <td>v1</td>
        </tr>
      <tr>
            <td>D1</td>
            <td>Doc Management System</td>
            <td>v2</td>
        </tr>
      <tr>
            <td>D1</td>
            <td>Clinical System</td>
            <td>v2</td>
        </tr>
    </tbody>
    </table>


### Known Issues ###

   * Lack of versioning of documents in the GP Practices. DateTime stamp is used to identify the latest version of the document.
   * No nationally agreed list of Document Types - GP Practices have their own list of document types which may also include free text.
   * Poor metadata of documents - GP systems have poor metadata information about documents.
   * Documents in disparate systems in a GP Practice - Documents metadata information and it’s versions may exist in disparate systems in a GP Practice. However, documents and it's basic information does sync back from Document Management Systems to the Clinical system.

## Scope ##

  <IMG src="images/access_structured/ARDocsScope.jpg" alt="Scope of documents"  style="max-width:60%;max-height:60%;">


## Use Case ##

### a. Community Pharmacist provides Diabetes Services ###

 **Scenario**

The Community Pharmacist provides a diabetes service. Providing this service to Patients can reduce the workload on the local GP Practice(s) so the Practice(s) can focus on higher priority or more critical services or provide greater convenience to the Patient and thus the local GP Practice(s) refer Patients to the Community Pharmacist.

**Actors**

Patient, Community Pharmacist, GP Connect APIs, Community Pharmacy IT System, GP Practice IT system.

**Main Flow**

1.	The Patient is referred to the Community Pharmacist for diabetes service by the GP
2.	The Community Pharmacist wants to view certain clinical documents of the Patient
3.	The Community Pharmacist accesses GP Connect to search for information about matching clinical documents from the Patient’s registered GP practice system
4.	GP Connect requests metadata information about clinical documents from the GP clinical system and presents it to the community pharmacy system.
5.	The Community Pharmacist s view this information and requests to view a clinical document from the GP practice system via GPConnect.
6.	Community pharmacy system receives binary of the requested document and presents it in a readable format
7.	The Community Pharmacist views the clinical document and uses this information to assist their treatment of the Patient.


### b. Paramedic accesses Do Not Attempt Resuscitation document ###

**Scenario**

A Paramedic is visiting a Patient who has collapsed at home and needs to ascertain whether the Patient has a Do Not Resuscitation order recorded on the GP system, and the date it was recorded.  Ideally, the Paramedic would be able to see DNR history and associated information such as whether the Patient and family are aware of the decision.  
They should also be able to access an uploaded DNR document, if it exists.

**Actors**

Paramedic, Paramedic s IT system, Patient, GPConnect APIs, GP Practice ITsystem

**Main Flow**

1.	Paramedic accesses Patient information on their mobile EPR
2.	The Paramedic wants to view DNR document of the Patient to understand Patient’s consent to resuscitate or not.
3.	Paramedic s system accesses GP Connect to search for information about any DNR document of the Patient from their registered GP Practice’s clinical system
4.	GP Connect requests metadata information about matching documents of the Patient from the GP Practice system and presents it to the Paramedic ’s system.
5.	The Paramedic views the metadata information of matching documents on their system and requests to view the DNR document from the GP Practice system via GPConnect.
6.	The Paramedics system receives the binary of the document and presents it in a readable format.
7.	The Paramedic views the DNR document and use this information to assist their treatment of the Patient

## Documents Classification ##
Document types vary across GP Practices and may contain free text. Requirements analysis and Professional Record Standards Body (PRSB) documentation identifies a demand for a clear classification of documents.
To address this issue, GPConnect has created a valueset of document types. It is based on the Clinical document indexing standards created by NHS Scotland. Providers would map their document types to the GPConnect document types valueset. Where the Providers have a code that does not exist in the value set, they can provide their code and its value in the text field. This would improve the standardisation of document types across the GP Practices.

## Patient records where documents are not available ##
GP clinical systems may have some migrated patient records that have information about the document but the document is not available to the clinical system. To resolve this, GPConnect APIs would return a placeholder for the document specifying that there is a document but it is not available. The metadata information about the document would provide information about the Authoring Organisation of the document from where the document can be requested.

## Document Format ##
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

## Multiple Versions of the Document ##
A GP Practice may have multiple versions of the same document of the Patient in their clinical system. Providers would only return latest version of the document via the GPConnect APIs.

## Internal or External Documents ##
The GP Practice from which the document is being requested is the custodian of the document. Requirements analysis suggest that end-users would like to understand if the patient document that they are retrieving from the GP Practice is an internally generated document in the GP Practice or an external Organisation has sent that document to the GP Practice.
If the 'Authoring Organisation' of the document is same as Custodian of the document then it's an internally generated document.
If the 'Authoring Organisation' of the document is NOT the same as Custodian of the document then it's an externally generated document.

## File Size of the document ##
End-users would like to know the size of the document before retrieving the document. Providers would return the file size of the document in the response payload for Search Document GPConnect API request.

## Multiple systems/providers being used in a GP Practice to manage documents ##
A GP Practice may use Document Management systems for managing documents besides the clinical systems. The documents held in Document Management system sync to the clinical system along with it's basic information such as document type, clinical setting, organisation, description and date. Any read codes extracted in the document management system is also synced to the clinical system. This is done so that in case when the document management system is unavailable, the document is still available in the prinicple clinical system and vice versa.
GPConnect APIs would search for documents and retrieve documents only from the clinical system.




