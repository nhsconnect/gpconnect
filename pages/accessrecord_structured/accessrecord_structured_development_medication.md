---
title: Medication
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication.html
summary: "Guidance for populating and consuming the Medication resource"
---

## Medication resource usage ##

The subheadings below show you how to populate and consume elements of the Medication resource.

You'll find it helpful to read it in conjunction with the underlying [Medication profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1).

Any element not specifically listed **SHOULD NOT** be populated.

### Medication.id ###

<table class='resource-attributes'>
  <tr>
    <td class='ra-datatype'>Data type</td>
    <td class='ra-datatype-value'>Id</td>
    <td class='ra-optionality'>Optionality</td>
    <td class='ra-optionality-value'>Mandatory</td>
  </tr>
</table>

The logical identifier of the Medication resource.

### Medication.meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td>Data type</td>
    <td>uri</td>
    <td>Optionality</td>
    <td>Mandatory</td>
  </tr>
</table>

The Medication profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1)

### Medication.code ###

<table class='resource-attributes'>
  <tr>
    <td>Data type</td>
    <td>CodeableConcept</td>
    <td>Optionality</td>
    <td>Mandatory</td>
  </tr>
</table>

The code that identifies the medication.

A SNOMED dm+d code **MUST** be supplied, if available.

#### Degraded medications ####

Where degraded medication records arising from GP2GP record transfer are present in the patient record then these **MUST** be coded using the SNOMED degrade code (`196421000000109`, Transfer-degraded medication entry) with the original medication name conveyed by `CodeableConcept.text`.

#### Mixtures ####

In some systems it is possible to prescribe custom formulations compounded from other medications (extemporaneous preparations).

Mixtures **MUST** be expressed using the degrade code (`196421000000109`, Transfer-degraded medication entry) with the constituents of the mixture expressed via `CodeableConcept.text`.

#### Non dm+d medications ####

In some cases, drugs may be recorded as free text or may be present in the original system’s drug dictionary, but not in dm+d.

Where no dm+d code is available to describe the medication then the medication code **MUST** be expressed using the degrade (`196421000000109`, Transfer-degraded medication entry) with the original drug name present in `CodeableConcept.text`.

#### dm+d name versus displayed name ####

It is possible for historic/legacy medications to be displayed with a name corresponding to the name in the original system’s drug dictionary rather than the dm+d name.

This name **MUST** be preserved via `CodeableConcept.text` when representing the medication via resources. `CodeableConcept.text` is redundant when the displayed medication name on the original system and the dm+d name is identical, and, in these cases, `CodeableConcept.text` **MUST** be omitted.

### Medication.package ###

<table class='resource-attributes'>
  <tr>
    <td>Data type</td>
    <td>BackboneElement</td>
    <td>Optionality</td>
    <td>Optional</td>
  </tr>
</table>

If the GP providing system has data relating to the batch number or expiry date they **MAY** be populated within this element.
