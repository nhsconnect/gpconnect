---
title: Immunisation guidance
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_immunization_guidance.html
summary: "FHIR&reg; resource Immunization"
---

## What is immunisation?

Immunisation, is the process by which an individual's immune system becomes fortified against an agent (known as the immunogen).

When this system is exposed to molecules that are foreign to the body, called non-self, it will orchestrate an immune response, and it will also develop the ability to quickly respond to a subsequent encounter because of immunological memory. This is a function of the adaptive immune system. Therefore, by exposing an animal to an immunogen in a controlled way, its body can learn to protect itself: this is called active immunisation.

## What is a vaccination?

Vaccination is the administration of a vaccine to help the immune system develop protection from a disease. Vaccines contain a microorganism or virus in a weakened or killed state, or proteins or toxins from the organism. In stimulating the body's adaptive immunity, they help prevent sickness from an infectious disease. When a sufficiently large percentage of a population has been vaccinated, herd immunity results. The effectiveness of vaccination has been widely studied and verified.[1][2][3] Vaccination is the most effective method of preventing infectious diseases;[4] widespread immunity due to vaccination is largely responsible for the worldwide eradication of smallpox and the elimination of diseases such as polio and tetanus from much of the world.

## What immunisation data is GP Connect sending

In GP Connect what is sent in the <code>immunization</code> resource is the event of a patient being administered a vaccination. 
This may be a contemporaneous record by the clinician administering the vaccination (or by another member of the practice staff recording the event directly on behalf of the clinician) or it may be a record of an immunisation administered elsewhere as reported to the registered GP practice by the patient, a carer, guardian or other representative of the patient or another healthcare provider.

A record of an immunisation may be created as part of a scheduled programme of immunisations such as childhood immunisations, seasonal influenza vaccination or in response to specific circumstances (for example, prior to travel, disease outbreak or occupational risk).

## Using the procedure code

GP Clinical Systems do not all record the full vaccine product (dm+d code) for an immunisation.
GP Clinical Systems often record the type of vaccine administered as opposed to the vaccine product.
This may be as a procedure code or a local code which can be mapped to a procedure code. 
GP Connect therefore uses the vaccination procedure code to denote the vaccine being administered.
The vaccination procedure code is a mandatory element.
The vaccine product code will often be a null flavor code, but the actual vaccine product **MUST** be included if it is available.

## Vaccinations that were not given

This version of the specification only supports immunisations which have been given to the patient.
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

The Immunization FHIR profile contains elements to denote that a vaccination does not count towards immunity.
This could be applied where a vaccination is suspected or found to be ineffective, for example as a result of a product recall or cold chain break. 
GP clinical systems do not have a standard means to identify an ineffective vaccination, hence immunisaton records will always be returned as counting towards immunity.

## Reactions to a vaccine

Allergic or adverse reactions to an immunisation may be captured in the GP Clinical System but these are not generally directly associated to the immunisation event.
It has not been considered reliable to link any allergic or adverse reaction to the immunisation record therefore information about reactions will not be included.
For details of allergies or adverse reaction, the <code>AllergyIntolerance</code> resource **MUST** be requested.

## Immunisation schedules and recalls

The resources required to describe planned immunisation schedules or diarised recalls to complete an immunisation series are out of scope for this guidance.

## Immunisation notes

GP Systems that support a note entry against the immunisation **MUST** populate the text to the <code>note</code> element.
Additionally, any other information relevant to the immunisation which does not have a suitable, supported element within the <code>immunization</code> resource **MUST** be populated to the <code>note</code> as a key value pair.
This includes where there is an element in the profile for the type of information, but the data type is not compatible with the way the data is recorded in the GP System.
For example, the vaccine manufacturer is recorded in a free text field so it is not suited as a reference to an <code>organization</code> resource for the <code>manufacturer</code> element and is therefore populated to the <code>note</code> element as 'Manufacturer: Acme Pharmaceuticals'.
This might also apply to the <code>doseQuantity</code> element if the GP System holds the dosage information in a format which does not comply with the <code>Quantity</code> datatype structure.

## Using the `List` resource for immunisation queries

The results of a query for immunisation details **MUST** return a `List` containing references to all `Immunization` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason` with the value `noContent`.
