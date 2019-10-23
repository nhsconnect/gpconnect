---
title: Access Record Structured
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured.html
summary: "Introduction to the Access Record Structured capability"
---

## Purpose ##

The Access Record Structured capability enables an NHS system to request and consume a patient’s GP record in a structured and coded format that is machine readable. The data will be made available via a standard API. Structured data allows the consuming system to import and process the patient data in whatever way it requires to best support patients and the healthcare professionals treating them. GP Connect does not place any specific restrictions on how the data is processed so long as the data is only used for the direct care of the patient and the system meets the specified GP Connect consumer requirements (including information governance and clinical safety standards).

## Scope ##

The Access Record Structured capability will expose data for a number of clinical areas. This release supports:

1. Medications
2. Allergies
3. Immunizations
4. Uncategorised items
5. Consultations
6. Problems
7. Investigations
8. Referrals (Outbound)

{% include note.html content="The Access Document capability is available in its own GP Connect specification version. 
Access Document compliments Access Record Structure by retrieval of a documents list or individual documents.
Please consult the [specification versions page](https://developer.nhs.uk/gp-connect-specification-versions/) for more details." %}

{% include roadmap.html content="Subsequent releases are to be scoped" %}

## FHIR version ##
Standard for Trial Use 3 (STU3) is the version of FHIR which will be adopted for the Access Record Structured capability. A decision was taken to uplift the profiles from the previous DSTU2 version for the following reasons:

 - STU3 is widely being adopted in the UK interoperability community
 - there are many breaking changes between DSTU2 and STU3
 - no supplier development had started on the previous DSTU2 versions
 - the STU3 profiles offer additional clinical value
