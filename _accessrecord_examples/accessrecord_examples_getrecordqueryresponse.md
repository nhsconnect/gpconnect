---
title: GetRecordQueryResponse
sidebar: accessrecord_sidebar
permalink: accessrecord_examples_getrecordqueryresponse.html
summary: "Profile data examples for the Access Record HTML response."
profiles:
  - name: GPConnect-Searchset-Bundle-1
    examples:
      - name: Bundle-CareRecord-Medications
        description: 	GPConnect-Searchset-Bundle-1 containing the GP Connect Query Response bundled resources (Patient Care Record) Medications Section Example
      - name: Bundle-CareRecord-Summary
        description: GPConnect-Searchset-Bundle-1 containing the GP Connect Query Response bundled resources (Patient Care Record) Summary Section Example
      - name: Bundle-OperationOutcome
        description: 	GPConnect-Searchset-Bundle-1 containing the the GP Connect Query Response bundled resources (Operation Outcome - NHS Number Invalid) Example
  - name: GPConnect-OperationOutcome-1
    examples:
      - name: OperationOutcome-1a
        description: GPConnect-OperationOutcome-1 (NHS Number Invalid) Example
      - name: OperationOutcome-1b
        description: GPConnect-OperationOutcome-1 (No Record Found) Example
  - name: GPConnect-Patient-1
    examples:
      - name: Patient
        description: NHS Patient example
  - name: GPConnect-CareRecord-Composition-1
    examples:
      - name: Composition-CareRecord-AdministrativeItems
        description: NHS Patient Care Record - Administrative Items Section
      - name: Composition-CareRecord-AllergiesandSensitivities
        description: NHS Patient Care Record - Allergies and Sensitivities Section
      - name: Composition-CareRecord-ClinicalItems
        description: NHS Patient Care Record - Clinical Items Section
      - name: Composition-CareRecord-Encounters
        description: NHS Patient Care Record - Encounters Section
      - name: Composition-CareRecord-Immunisations
        description: NHS Patient Care Record - Immunisations Section
      - name: Composition-CareRecord-Investigations
        description: NHS Patient Care Record - Investigations Section
      - name: Composition-CareRecord-Medications	
        description: NHS Patient Care Record - Medications Section
      - name: Composition-CareRecord-Observations
        description: NHS Patient Care Record - Observations Section
      - name: Composition-CareRecord-PatientDetails
        description: NHS Patient Care Record - Patient Details Section
      - name: Composition-CareRecord-Problems
        description: NHS Patient Care Record - Problems Section
      - name: Composition-CareRecord-Referrals
        description: NHS Patient Care Record - Referrals Section
      - name: Composition-CareRecord-Summary
        description: NHS Patient Care Record - Summary Section
  - name: GPConnect-Practitioner-1
    examples:
      - name: GP-Practitioner
        description: GP
      - name: Practitioner
        description: Consultant
      - name: Practitioner-1a
        description: Nurse
  - name: GPConnect-Location-1
    examples:
      - name: Location-1a
        description: Hematology clinic
      - name: Location-1b
        description: Hospital
  - name: GPConnect-Organization-1
    examples:
      - name: GP-Organization
        description: GP Organization
      - name: Organization-1a
        description: Organization Example
      - name: Organization-1b
        description: Organization Example
  - name: GPConnect-Device-1
    examples:
    - name: Device
      description: Device
---
{% include profiles.html profiles=page.profiles %}