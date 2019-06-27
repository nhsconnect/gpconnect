---
title: Immunization guidance
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_immunization_guidance.html
summary: "FHIR&reg; resource Immunization"
---

## What is an immunisation?

An immunisation is the event of a patient being administered a vaccination. This may be a contemporaneous record by the clinician administering the vaccination (or by another member of the practice staff recording the event directly on behalf of the clinician) or it may be a record of an immunisation administered elsewhere as reported to the registered GP practice by the patient, a carer, guardian or other representative of the patient or another healthcare provider.

Immunisation may be given as part of a scheduled programme of immunisations such as childhood immunisations, seasonal influenza vaccination or in response to specific circumstances (for example, prior to travel, disease outbreak or occupational risk).

## Using the procedure code

GP Clinical Systems have not recorded the full vaccine product (dm+d code) as their main identifier for immunisation.
GP Clinical Systems often record the type of vaccine administered as opposed to the vaccine product.
This may be as a procedure code or a local code which maps to a procedure code. 
The immunisation procedure code will be used as the main vaccine identifier. 
The vaccine product can be included if it is available.

## Vaccinations that were not given

This version of the specification only supports immunisation which have been given to the patient.
GP Clinical Systems may capture details of circumstances where an immunisation has not been given but there was an intention to.
Planned immunisations may not be given for a variety of reasons, such as:

* an explicit refusal for a specific vaccine or for any form of immunisation
* lack of consent for a vaccine to be administered
* the vaccine is temporarily declined
* a contraindication with another medication
* the patient does not attend an appointment or does not attend an open clinic (for example, seasonal flu vaccination clinic)
* the patient is unwell or does not meet criteria for the vaccination

All circumstances of an immunisation not given are out of scope of this version.
Options are to be evaluated for each not given use case and whether to include details in another resource or a future version of this profile.

## Ineffective vaccination

In the event a vaccination is suspected or found to be ineffective, for example as a result of a product recall or cold chain break, a record may be included without an identifier indicating it does not count towards immunity.
GP clinical systems do not have a standard means to identify an ineffective vaccination, hence records can only indicate that a vaccine was administered.

## Reactions to a vaccine

Allergic or adverse reactions to an immunisation may be captured in the GP Clinical System but these are not generally directly associated to the immunisation event.
It has not been considered reliable to link any allergic or adverse reaction to the immunisation record therefore information and reactions will not be included.
For details of allergies or adverse reaction, the Allergies resource **MUST** be requested.

## Immunisation schedules and recalls

The resources required to describe planned immunisation schedules or diarised recalls to complete an immunisation series are out of scope for this guidance.

## Data type incompatibility

It is possible that some participating systems will support recording of elements of the immunisation but in a way which is incompatible with the data type of the FHIR element.
An example might be the vaccine manufacturer recorded as a text qualifier to the immunisation procedure where the FHIR profile requires an organisation reference.
Where the data recorded is incompatible with the data type of the related FHIR profile element, the detail in the source system **MUST** be rendered as text (suitably formatted name/value pair) and placed in the <code>immunisation.note</code> element.
