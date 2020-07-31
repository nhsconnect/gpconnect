---
title: Documents guidance
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_documents_guidance.html
summary: "Guidance on the representation of documents in GP Connect"
---

{% include note.html content="Documents are defined in a separate [Access Document](access_documents.html) capability, which complements Access Record Structured by allowing the querying and retrieval of documents for a patient." %}



## Introduction
A clinical document (CD) is a written, printed or electronic record that provides evidence of medical care. Clinical documents must be accurate, timely and reflect specific services provided to a patient. A clinical document could be any document that the GP practice adds to a clinical record of the patient.

## Returning document metadata in Access Record Structured
When querying for consultations and problems, [DocumentReference](access_documents_development_documentreference.html) resources containing document metadata will be returned for any linked documents. The document location will be returned alongside the metadata so that consumers can retrieve the [Binary](access_documents_development_binary.html) resource for the document. In order to do this, consumers will need to have been assured against the [Access Document](access_documents.html) capability.
