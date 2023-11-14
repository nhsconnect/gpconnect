---
title: Business requirements
keywords: requirements
tags:
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_requirements.html
summary: "Clinical, user and governance requirements that must be supported by the solution"
---

## User stories and logical data model ##

The GP Connect Requirements Catalogue for Access Record Structured Data contains the full set of business requirements that need to be met to support the retrieval of data in a structured format for the supported clinical areas of the GP record:

>###   [GP Connect Requirements Catalogue for Access Record Structured Data](pages/accessrecord_structured/GP%20Connect%20Req%20Cat%20-%20Access%20Record%20Structured%20Data%20v2.4.xlsx){:target="_blank"}

The requirements are described as a set of user stories with separate acceptance criteria for the provider and consumer systems.

The logical data model identifies and defines the data items that are required by the business. Each logical data item is mapped to the FHIR&reg; profile that will be used to transmit the data.

## Use cases and business processes ##

The use cases define how and where there is a business need that can be supported by GP Connect structured data. They contain the following key components:

- Description
- Justification
- Process flow (including data requirements)

The level of detail varies from use case to use case.

- [3.1 Active checking of a prescription in unscheduled care](accessrecord_usecase_3.1.html)

- [3.2 View GP current medication in Coordinate My Care](accessrecord_usecase_3.2.html)

- [3.3 View patient-centric summary in Leeds Care Record](accessrecord_usecase_3.3.html)

- [3.4 A care professional user of the Local Care Record reviews a patient’s GP practice medication information](accessrecord_usecase_3.4.html)

- [3.5 Medicines reconciliation for acute care admissions](accessrecord_usecase_3.5.html)

- [3.6 Out of hours GP accesses medications, allergies and problems](accessrecord_usecase_3.6.html)

- [3.7 Admission of patient to the Yorkshire Centre for Eating Disorders](accessrecord_usecase_3.7.html)

- [3.8 Community nurse reviews the GP record when they visit a patient](accessrecord_usecase_3.8.html)

- [3.9 Dentist reviews the GP record when they treat a patient](accessrecord_usecase_3.9.html)

- [3.10 Import patient record for acute care admissions (including medication reconciliation)](accessrecord_usecase_3.10.html)

- [3.11 Import patient record for a private hospital](accessrecord_usecase_3.11.html)

- [3.12 Referral to single point of access for mental health](accessrecord_usecase_3.12.html)

- [3.13 Triaged by Clinical Assessment Service clinician after referral to Single Point of Access for mental health](accessrecord_usecase_3.13.html)

- [3.14 Health visitor appointments during a child’s early years](accessrecord_usecase_3.14.html)

- [3.15 School nurse appointments](accessrecord_usecase_3.15.html)

- [3.16 Medications reconciliation following admission of patient to Leeds Teaching Hospital](accessrecord_usecase_3.16.html)

- [3.17 Out of hours and extended hours GP appointments in a federated GP environment](accessrecord_usecase_3.17.html)

- [3.18 Medications reconciliations prior to admission of patient to Becklin Centre](accessrecord_usecase_3.18.html)

- [3.19 Community pharmacy managing patients](accessrecord_usecase_3.19.html)

- [3.20 Community pharmacy giving vaccinations](accessrecord_usecase_3.20.html)

- [3.21 A care professional user of the Local Care Record reviews a patient’s GP practice risks and warnings](accessrecord_usecase_3.21.html)

- [3.22 Clinical Triage Platform consumes GP-held patient data](accessrecord_usecase_3.22.html)

- [3.23 Midwife views patient record before visiting patient](accessrecord_usecase_3.23.html)

- [3.24 Practice nurse administering a vaccination](accessrecord_usecase_3.24.html)
- [3.25 Parental consent differs for immunisation](accessrecord_usecase_3.25.html)
- [3.26 Mental health new referral daily triage](accessrecord_usecase_3.26.html)
- [3.27 Review a patient's GP practice information - list of diagnoses](accessrecord_usecase_3.27.html)
- [3.28 Review a patient's GP practice information - relating to events](accessrecord_usecase_3.28.html)
- [3.29 Review a patient's GP practice information - current and past examination and investigation results](accessrecord_usecase_3.29.html)
- [3.30 Palliative care](accessrecord_usecase_3.30.html)
- [3.31 Community cardiac nurse](accessrecord_usecase_3.31.html)
- [3.32 OOH assessment of potential measles case](accessrecord_usecase_3.32.html)
- [3.33 A professional user of the Local Care Record needs to review a patient's GP practice information - current and past problems](accessrecord_usecase_3.33.html)
- [3.34 Review a patient's GP practice information - clinical summary of the patient](accessrecord_usecase_3.34.html)
- [3.35 Review a patient's GP practice information - current and past procedures](accessrecord_usecase_3.35.html)
- [3.36 Referral to social prescribing](accessrecord_usecase_3.36.html)
- [3.37 Community pharmacist providing diabetes services](accessrecord_usecase_3.37.html)
- [3.38 Community pharmacist providing spirometry services](accessrecord_usecase_3.38.html)
- [3.39 111/999 call handler](accessrecord_usecase_3.39.html)
- [3.40 Paramedic](accessrecord_usecase_3.40.html)
- [3.41 Health Visitors appointment during pregnancy - antenatal](accessrecord_usecase_3.41.html)

## Clinical engagement ##

To help ensure that the functionality being developed will be able to support a wide range of clinical uses, GP Connect has engaged with a range of clinicians and other stakeholders to get an understanding of how that data may be used and what is required to support its use.

This engagement has included:

- Hospital consultants and doctors
- Hospital pharmacists and technicians
- Mental health nurses
- Mental health pharmacists and technicians
- Mental health point of access centre
- General practitioners
- Community pharmacists
- Midwives
- Health visitors
- Health system suppliers
- Commissioning support units
- Hospital trusts

The feedback from these stakeholders has been used to develop the business use cases, user stories and the logical data model. These will form the basis of the technical specification and will be used to assure that the GP Connect API meets the needs of the business.
