---
title: Business requirements
keywords: requirements
tags: [requirements]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_requirements.html
summary: "Summary of organisational requirements that have informed development work"
---

## User stories and logical data model ##

The [GP Connect Requirements Catalogue for Access Record Structured Data](pages/accessrecord_structured/GP%20Connect%20Req%20Cat%20-%20Access%20Record%20Structured%20Data%20v0.5.xlsx){:target="_blank"} contains the full set of business requirements that need to be met to support the retrieval of medications and allergy data in a structured format.

The requirements are described as a set of user stories with separate acceptance criteria for the provider and consumer systems.

The logical data model identifies and defines the data items that are required by the business. Each logical data item is mapped to the FHIR&reg; profile that will be used to transmit the data.

The Excel spreadsheet is split into 6 tabs:

1.	Document Management: Revision history
2.	NHS England Scenarios:	A set of scenarios defined by NHS England that identify the scope of the work.
3.	Processes – Use Cases:	An index of the use cases used to develop the user stories and logical model. Links to the individual use cases are given below.
4.	User Stories:	The user stories that describe the business requirements for the provider and consumer products.
5. User Stories - IG: The user stories that describe the standards and information governance requirements for the provider and consumer products.
6.	Logical Data Model:	The logical model that identifies and defines that data items that will be supplied.

## Use cases and business processes ##

The use cases define how and where there is a business need that can be supported by GP Connect structured data. They contain the following key components:

 - Description
 - Justification
 - Process Flow (including data requirements)

The level of detail varies from use case to use case.

 - [3.1	Active Checking of a prescription in Unscheduled Care](pages/accessrecord_structured/use_cases/3.1 Use_case_Allergies_Servelec_v1_1.docx)

- [3.2	View GP Current Medication in Coordinate my Care](pages/accessrecord_structured/use_cases/3.2 Use_case_care_plan_CMC_v1_1.docx)

- [3.3	View Patient centric summary in Leeds Care Record](pages/accessrecord_structured/use_cases/3.3 Use_Case_Care_Rec_Leeds_v1_1.docx)

- [3.4	A care professional user of the Local Care Record reviews a patient’s GP Practice medication information](pages/accessrecord_structured/use_cases/3.4 Use_case_LCR_Meds_Guys_v1_1.docx)

- [3.5	Medicines Reconciliation for Acute Care Admissions](pages/accessrecord_structured/use_cases/3.5 Use_case_Meds_Reconciliation_Warr_ v1_2.docx)

- [3.6	Out of Hours GP accesses medications, allergies and problems](pages/accessrecord_structured/use_cases/3.6 Use_case_OoH_Oxford_v1_1.docx)

- [3.7	Admission of patient to the Yorkshire Eating Disorders Clinic](pages/accessrecord_structured/use_cases/3.7 Use_case_New_Patient_Eating_Disorders.docx)

- [3.8	Community Nurse reviews the GP record when they visit a patient](pages/accessrecord_structured/use_cases/3.8 Use_case_community_nursing_visit.docx)

- [3.9	Dentist reviews the GP record when they treat a patient](pages/accessrecord_structured/use_cases/3.9 Use_case_dentist.docx)

- [3.10	Import Patient Record for Acute Care Admissions (including medication reconciliation)](pages/accessrecord_structured/use_cases/3.10 Use_case_Import_record_for_acute_admission.docx)

- [3.11	Import Patient Record for a private hospital](pages/accessrecord_structured/use_cases/3.11 Use_case_Import_record_for_private_hospital.docx)

- [3.12	Referral to Single point of access for Mental Health](pages/accessrecord_structured/use_cases/3.12 Use_case_Single_point_of_access.docx)

- [3.13	Triaged by Clinical Assessment Service clinician after referral to Single Point of Access for Mental Health](pages/accessrecord_structured/use_cases/3.13 Use_case_CAS.docx)

- [3.14	Health Visitor appointments during a child’s early years](pages/accessrecord_structured/use_cases/3.14 Use_case_Health_Visitor_After_Birth.docx)

- [3.15	School nurse appointments](pages/accessrecord_structured/use_cases/3.15 Use_case_School_Nurse.docx)

- [3.16	Medications reconciliation following admission of patient to Leeds Teaching Hospital](pages/accessrecord_structured/use_cases/3.16 Use_case_eMedicines.docx)

- [3.17	Out of Hours and Extended hours GP appointments in a federated GP environment](pages/accessrecord_structured/use_cases/3.17 Use_case_GP_Practice_Federation.docx)

- [3.18	Medications reconciliations prior to admission of patient to Becklin Centre](pages/accessrecord_structured/use_cases/3.18 Use_case_Pharmacy_Becklin_Centre v0.2.docx)

- [3.19	Community Pharmacy managing patients](pages/accessrecord_structured/use_cases/3.19 Use_case_CP_managed_patients.docx)

- [3.20	Community Pharmacy giving vaccinations](pages/accessrecord_structured/use_cases/3.20 Use_case_CP_giving_vaccinations.docx)

- [3.21	A care professional user of the Local Care Record reviews a patient’s GP Practice risks and warnings](pages/accessrecord_structured/use_cases/3.21 Use_case_LCR_Risks_Guys_v1_0.docx)

- [3.22	Clinical Triage Platform Consume GP held Patient Data](pages/accessrecord_structured/use_cases/3.22 Use_case_CTP_Input_Data_Consume_GP_Held_Record v0.1.docx)

- [3.23 Midwife views patient record before visiting patient](pages/accessrecord_structured/use_cases/3.23 Use_case_Maternity.docx)

## Clinical engagement ##

To help ensure that the functionality being developed will be able to support a wide range of clinical uses, GP Connect has engaged with a range of clinicians and other stakeholders to get an understanding of how that data may be used and what is required to support its use.

This engagement has included:

 - Hospital Consultants and Doctors
 - Hospital Pharmacists and Technicians
 - Mental Health Nurses
 - Mental Health Pharmacists and Technicians
 - Mental Health Point of Access Centre
 - General Practitioners
 - Community Pharmacists
 - Midwives
 - Health Visitors
 - Health System Suppliers
 - Commissioning Support Units
 - Hospital Trusts

The feedback from these stakeholders has been used to develop the business use cases, user stories and a logical data model available above. These will form the basis of the technical specification and will be used to assure that the GP Connect API meets the needs of the business.

