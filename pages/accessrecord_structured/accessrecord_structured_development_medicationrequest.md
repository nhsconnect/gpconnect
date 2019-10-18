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

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [MedicationRequest profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1/_history/1.2)." %}

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
    <td><b>Data type:</b> <code>PositiveInt</code></td>
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
    <td><b>Data type:</b> <code>PositiveInt</code></td>
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

If a medication/medical device is an acute, acute-handwritten, delayed acute, repeat or repeat dispense.

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

This is for business identifiers.

This is sliced to include a cross-care setting identifier which **MUST** be populated. The codeSystem for this identifier is `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

This **MUST** be a GUID.

*Providing* systems **MUST** ensure this GUID is globally unique and a persistent identifier (that is, it doesn't change between requests and therefore stored with the source data).

Where *consuming* systems are integrating data from this profile to their local system, they **MUST** also persist this GUID at the same time.

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

Composite request this is part of. The element in the Identifier data type that **MUST** be populated when a groupIdentifier is populated is `identifier.value`.

All repeat prescribed and repeat dispensed medications **MUST** have a group identifier that is populated for the ‘plan’ and all ‘orders’ relating to them.

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
- `complete` represents an authorisation which has run its course.

For `MedicationRequest` instances where `intent` is set to `plan`:

* For repeats and repeat dispensed the status refers to the status of the plan (the entire cycle of prescriptions).
* For acutes the status refers to the status of the prescription issue.

For `MedicationRequest` instances where `intent` is set to `order`:

* The status refers to the status of the prescription issue.

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

To be used if the medication/medical device was prescribed at another practice and has been imported via GP2GP. In that case, the `onBehalfOf` **MUST** be completed with a reference to the other organisation.

If the medication/medical device has been prescribed elsewhere and, for example, is detailed in the sending system as a hospital medication, this **MUST** be detailed using an `organisation.type` code in the agent reference in the requester element.

### recorder ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The responsible `Practitioner` who authorised the medication/medical device.

May not always be the user who entered the record on the system but, where a system supports attribution to a responsible clinician, the attributed clinician **MUST** be referenced here.

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

The elements of the dosage datatype detailed below should be populated as described. All other elements that are part of the dosage datatype are optional.

### dosageInstruction.text ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Complete dosage instructions as text.

In exceptional cases where for legacy data there is no dosage information recorded in the system then this **MUST** be populated with the text 'No information available'.

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

* This refers to the period that the medication/medical device plan is active.
* This **MUST** mirror `MedicationStatement.effective`

For `MedicationRequest` instances where `intent` is set to `order`:

*	This refers to the period that the issued prescription is active

`Period.start` is **MANDATORY**.

Use one of the following dates in order of descending preference:
*	The prescription issue date recorded in the patient record
*	The date the prescription was recorded.

`Period.end` is **MANDATORY**.

Use one of the following dates in order of descending preference:
*	The prescription end date recorded in the patient record
*	The prescription end date derived from period.start and the duration
*	The Period.start date
    * This option should only occur where data has been lost (for example, during the record transfer between two systems) and is used to ensure that an ended prescription will always have an end date.


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

Textual representation of quantity.

Only to be used if there is no numerical value.

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
