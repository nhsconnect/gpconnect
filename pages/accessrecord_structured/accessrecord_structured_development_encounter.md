---
title: Encounter
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_encounter.html
summary: "Guidance for populating the Encounter resource for consultations"
---

## Encounter elements

### id

Data type: Id	Optionality: Mandatory	Cardinality: 1..1


The logical identifier of the Encounter resource.

### meta.profile

Data type: uri	Optionality: Mandatory	Cardinality: 1..1


The Encounter profile URL.

### identifier

Data type: Identifier	Optionality: Mandatory	Cardinality: 1..*


This is for business identifiers.

This is sliced to include a cross care setting identifier which MUST be populated. The codeSystem for this identifier is `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

### status

Data type: status	Optionality: Mandatory	Cardinality: 1..1


Fixed value of **finished**. 

Existing vocabulary is driven by use of Encounter for appointment style encounters rather than provision of Consultation context. Hence use most appropriate value from limited set available. 

Some systems allow Consultations to be assigned a draft or incomplete status but this status is not conveyed in GP Connect as the information recorded in such Consultation is still treated as authoratative by the source systems.

### statusHistory

Not used.

### class

Not used.

### classHistory

Not used.

### type

Data type: CodeableConcept	Optionality: Mandatory	Cardinality: 1..1


Carries the Consultation type as displayed by system via the CodeableConcept **.text** attribute.

TO DO - rule a mapping to a Snomed CT vocabulary in or out

### priority

Not used.

### subject

Data type: Reference(Patient)	Optionality: Mandatory	Cardinality: 1..1


Reference to Patient resource representing the Patient against whom the source Consultation/encounter was recorded.

### episodeOfCare

Not used

### incomingReferral

Not used.

The current scope of GP Connect excludes inbound referrals.

### participant

Data type: BackboneElement	Optionality: Required	Cardinality: 0..*


Where available will always be populated with at least one **.individual** Reference(Practitioner) with **.type** value of **'PPRF'**  from the  vocabulary. This should reference a Practitioner resource representing the individual with primary attribution for the Consultation/Encounter (usually the single primary attributed user shown in system journals or other views).

Other participants e.g. Registrars, trainees or other parties present may be referenced but with a participation type of **'PART'**.

No other values of participation type should be used.

The authorship of the Consultation/Encounter i.e. the actual user who entered the information on the system should be expressed via **List.source**.

### appointment

Data type: Reference(Appointment)	Optionality: Required	Cardinality: 0..*


### period

Data type: Period	Optionality: Required	Cardinality: 0..1


If recorded, **.start** is mandatory and should be populated with the displayed Consultation date and time 

**.end** should be populated where the encounter end date and time is known or calculated and populated where the duration is known.

The audit trail date time of the Consultation is carried by the associated Consultation List via **List.date**

The **period** attribute may be omitted where the effective/clinical date for the Consultation on the source system is not recorded e.g. an unknown date and time.

### length

Data type: Duration	Optionality: Required	Cardinality: 0..1


Specifies the length of the Consultation. Should be calculated and populated where an end time for the Consultation is known.

### reason

Not used

### diagnosis

Not used

### account

Not used

### hospitalization

Not used

### location

Data type: Reference(Location)	Optionality: Required	Cardinality: 0..*


References an instance of the Location resource that provides more detail on where the Consultation/encounter took place e.g. Branch surgery.

**location.status** and **location.period** are not used

### serviceProvider

Data type: Reference(Organization)	Optionality: Required	Cardinality: 0..1


Reference to the responsible organisation for the Consultatiion/Encounter.

### partOf

Not used.
