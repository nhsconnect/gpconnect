---
title: MedicationRequest
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medicationrequest.html
summary: "Guidance for populating and consuming the MedicationRequest profile"
div: resource-page
---

## Introduction ##

The headings below list the elements of the `MedicationRequest` profile and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [MedicationRequest profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1/_history/1.6)" %}

## Overarching principles ##

When populating the MedicationRequest profile it may appear that fields are duplicated in other associated resources. In the interests of minimising redundancy, the 2 following principles **MUST** be applied when populating the MedicationRequest profiles:

1. All mandatory fields **MUST** be populated.

2. Required fields **MUST** always be populated where the data exists in the system apart from where a lexically identical value exists for an equivalent data item in one of the parent profiles. For a MedicationRequest with `intent` of `plan` the associated MedicationStatement would be the parent profile. For a MedicationRequest with `intent` of `order`, the associated MedicationStatement and MedicationRequest with `intent` of `plan` are both considered parent profiles.

## MedicationRequest elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the `MedicationRequest` profile.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The `MedicationRequest` profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1)

### extension[repeatInformation] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Extension</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Extension elements to hold details of repeat authorisation.

Only populate for a `MedicationRequest` with an `intent` = `plan`.
For a `MedicationRequest` with an `intent` = `order` none of the `repeatInformation` fields are populated.

### extension[repeatInformation].numberOfRepeatPrescriptionsAllowed ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>UnsignedInt</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The number of repeat issues authorised if specified.

**MUST** be present where a repeat is authorised for a defined number of issues.

**MUST NOT** be specified for acute prescriptions or where the number of repeat issues has not been defined. There is no concept of an initial dispense in GP Connect usage. Therefore, the `numberOfRepeats` allowed is the total number of allowed issues.

### extension[repeatInformation].numberOfRepeatPrescriptionsIssued ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>UnsignedInt</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Running total of number of issues made against a repeat authorisation.

**MUST** be zero, if not yet issued.

### extension[repeatInformation].authorisationExpiryDate ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The date a repeat prescription authorisation will expire.

Only populate for a `MedicationRequest` with an `intent` = `plan`.
For a `MedicationRequest` with an `intent` = `order` this is not populated.

### extension[statusReason] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension (statusReason)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Where a medication/medical device has been stopped (status == ‘stopped’), the reason is provided in the statusReason extension.

Mandatory for authorisations with stopped status.

Only populate for a `MedicationRequest` with an `intent` = `plan`. Do not populate for a `MedicationRequest` with an `intent` = `order`.

### extension[statusReason].date ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension (valueDateTime)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The dateTime the medication/medical device was stopped/discontinued.

Mandatory for stopped/discontinued medications/medical devices as the date will always be known. In exceptional cases where for legacy data there is no statusReason recorder in the system then this **MUST** be populated with the text 'No information available'.

### extension[statusReason].reason ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension (CodeableConcept)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The textual reason either free text or the term of a code for stopping/discontinuing the medication/medical device.

**MUST** be populated when `StatusReason.date` is populated.

{% include tip.html content="Please see [CodeableConcept and common code systems](accessrecord_structured_development_resources_overview.html#codeableconcept-and-common-code-and-identifier-systems) when populating this element." %}

### extension[prescriptionType] ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension (CodeableConcept)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

If a medication/medical device is an acute (code : `acute`), delayed acute (`delayed-prescribing`), repeat (`repeat`) or repeat dispense (`repeat-dispensing`).

This field provides an explicit repeat/acute flag rather than deriving it from presence of extension elements or repeatNumber.

In exceptional cases where for legacy data there is no prescriptionType recorded in the system then this **MUST** be populated with the text ‘No information available’.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This **MUST** be populated with a globally unique and persistent identifier (that is, it doesn't change between requests and therefore stored with the source data). This **MUST** be scoped by a provider specific namespace for the identifier.

Where *consuming* systems are integrating data from this resource to their local system, they **MUST** also persist this identifier at the same time.

If the EPS identifier is present then the identifier.value is where the EPS Id SHOULD also be added. The codeSystem for this identifier is `https://fhir.nhs.uk/Id/prescription-order-item-number`

### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(CarePlan, MedicationRequest, ProcedureRequest, ReferralRequest)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

This field is used to create the links between `MedicationRequest` profiles to represent the medication ordering process as described [here](accessrecord_structured_development_medication_resource_relationships.html). This **MUST** be used when a profile has an `intent` element that is set to `order` and is `basedOn` a `MedicationRequest` profile that has an `intent` set to `plan`.

**DO NOT USE** for authorisations - that is, for a `MedicationRequest` with `intent` of `plan`.

### groupIdentifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>
The EPS prescriptionID if this medication or medical device has been prescribed via the Electronic Prescriptions Service. The element in the Identifier data type that **MUST** be populated when a groupIdentifier is populated is `identifier.value`.

All EPS prescribed drugs **MUST** have the prescriptionID present in this field and have `system` element set to `https://fhir.nhs.uk/Id/prescription-order-number`.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The status of the authorisation.

Use one of `active`, `completed` or `stopped`:

- `active` represents an active authorisation - used for active medications/medical devices.
- `stopped` represents an authorisation which has been discontinued, cancelled or stopped.
- `completed` represents an authorisation which has run its course.

For `MedicationRequest` instances where `intent` is set to `plan`:

- For repeats and repeat dispensed the status refers to the status of the plan (the entire cycle of prescriptions).
- For acutes the status refers to the status of the prescription issue.

For `MedicationRequest` instances where `intent` is set to `order`:

- The status refers to the status of the prescription issue.

### intent ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Used to distinguish between authorisations and issues.

Use one of `plan` or `order`:

- `plan` represents an authorisation of a medication or medical device.
- `order` represents a prescription or issue of a medication or medical device.

### medication ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Medication)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The medication/medical device the authorisation is for.

The `Medication` profile provides the coded representation of the medication/medical device.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Who the medication/medical device is for - that is, to whom it will be administered.

Reference to patient.

### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The consultation when the medication/medical device was authorised.

For a `MedicationRequest` with an `intent` = `plan` this is the consultation where the plan was authorised.
For a `MedicationRequest` with an `intent` = `order` this is the consultation where the specific issue was authorised.

### authoredOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Authorisation date, when the medication/medical device was authorised.

Unless there is a distinct user-modifiable date and time for the authorisation, this is the audit trail dateTime for when the authorisation was entered.

### requester ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Person and their organization requesting authorisation for prescription.

May not always be the user who entered the record on the system but, where a system supports attribution to a responsible clinician, the attributed clinician **MUST** be referenced here.

If it was prescribed at another practice and has been imported via GP2GP. In that case, the `onBehalfOf` **MUST** be completed with a reference to the other organisation.

### recorder ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The person who entered the record on the system.

### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

All notes that are associated with this medication/medical device record.

Sometimes labelled Pharmacy text or instructions for pharmacy.

### dosageInstruction ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Dosage</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

For provider systems that support fully structured dosage instructions a complete `Dosage` structure should be populated as per [implementation guidance](accessrecord_structured_development_medication_guidance.html#medication-and-medical-device-interoperability).

Where fully structured dosage instructions are not supported by provider systems `Dosage.text` and `Dosage.patientInstruction` should be populated as described below. All other elements that are part of the dosage datatype are optional, and may be populated in line with [ISN DAPB4013](https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections/dapb4013-medicine-and-allergy-intolerance-data-transfer).

### dosageInstruction.text ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Complete dosage instructions as text.

These instructions should be formatted as specified by [ISN DAPB4013](https://digital.nhs.uk/data-and-information/information-standards/information-standards-and-data-collections-including-extractions/publications-and-notifications/standards-and-collections/dapb4013-medicine-and-allergy-intolerance-data-transfer) and laid out in the [UK Core implementation guide](https://simplifier.net/guide/ukcoreimplementationguideformedicines/ElementDosage?version=current#text).

In exceptional cases where for legacy data, over-the-counter treatments or hospital treatments there is no dosage recorded in the system then this **MUST** be populated with the text 'No information available' or 'Not recorded' as most appropriate to the circumstance.

### dosageInstruction.patientInstruction ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Additional instructions for patient - that is, RHS of prescription label.

### dispenseRequest.validityPeriod ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Period</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Prescription start and end dates.

Start date is mandatory. Where there is a defined expiry or end date the end date **MUST** be supplied.

For `MedicationRequest` instances where `intent` is set to `plan`:

- This refers to the period that the medication/medical device plan is active.
- This **MUST** mirror `MedicationStatement.effective`

For `MedicationRequest` instances where `intent` is set to `order`:

- This refers to the period that the issued prescription is active

`Period.start` is **MANDATORY**.

Use one of the following dates in order of descending preference:

- The prescription issue date recorded in the patient record
- The date the prescription was recorded.

`Period.end` is **MANDATORY**.

Use one of the following dates in order of descending preference:

- The prescription end date recorded in the patient record
- The prescription end date derived from period.start and the duration
- The Period.start date
  - This option should only occur where data has been lost (for example, during the record transfer between two systems) and is used to ensure that an ended prescription will always have an end date.

### dispenseRequest.quantity ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>SimpleQuantity</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The quantity to dispense.

If the value is text, then the extension dispenseRequest.quantityText **MUST** be used.

### dispenseRequest.quantityText ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

This field is used to contain the units relating to the quantity. For example, 'tablet(s)', 'capsule(s)' or 'dose(s)'.

It may also be a textual representation of quantity. Only to be used in this way if there is no numerical value.

### dispenseRequest.expectedSupplyDuration ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Duration</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Number of days' supply per dispense.

### dispenseRequest.performer ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organization)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The organisation that dispensed the issue. Can only be completed where the provider organisation knows explicitly which organisation dispensed the issue. It cannot be assumed to be the nominated pharmacy or appliance supplier.

Only populate for a `medicationRequest` with an `intent` = `order`. For a `medicationRequest` with an `intent` = `plan` this field is not populated.

### priorPrescription ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(MedicationRequest)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

References prior prescription authorisation.

May be used, for example, to reference prior authorisation where prescription is re-authorised or where amendments have been made. May reference the previous authorisation before the amendment.

<h2 style="color:#ED1951;"> MedicationRequest elements <b>not in use</b> </h2>

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"> meta.versionId </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> meta.lastUpdated </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Instant</code></td>
  </tr>
</table>

<h3 style="color:#ED1951;"> definition </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(ActivityDefinition, PlanDefinition)</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> category </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> priority </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> supportingInformation </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Any)</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> reasonCode </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

This information is available via linking to a Problem record.

<h3 style="color:#ED1951;"> reasonReference </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Condition), Reference(Observation)</code></td>
  </tr>
</table>

This information is available via linking to a Problem record.

<h3 style="color:#ED1951;"> substitution </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> detectedIssue </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(DetectedIssue)</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.

<h3 style="color:#ED1951;"> eventHistory </h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Provenance)</code></td>
  </tr>
</table>

This is not in scope for this version of Care Connect and therefore not available for use in GP Connect.
