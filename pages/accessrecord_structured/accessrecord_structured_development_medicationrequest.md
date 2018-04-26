---
title: MedicationRequest resource
keywords: getcarerecord
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medicationrequest.html
summary: "Guidance for populating and consuming the MedicationRequest resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the MedicationRequest resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **MUST NOT** be populated or consumed. A full list of elements not used is available [here](accessrecord_structured_development_medicationrequest.html#elements-not-in-use)." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [MedicationRequest profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1)" %} 

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

The logical identifier of the MedicationRequest resource. This **MUST** be a unique and persisted identifier. 

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The MedicationRequest profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1)

### basedOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(CarePlan, MedicationRequest, ProcedureRequest, ReferralRequest)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

This field is used to create the links between `MedicationRequest` resources to represent the medication ordering process as described [here] (add link to representing the ordering process in FHIR) This **MUST** be used when a resource has an `intent` element that is set to `order` and is `basedOn` a `MedicationRequest` resource that has an `intent` set to `plan`.

**DO NOT USE** for authorisations ie. for a MedicationRequest with `intent` of `plan`.

### groupIdentifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Composite request this is part of.

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

- `active` represents an active authorisation - used for active repeat medications.
- `stopped` represents a repeat authorisation which has been discontinued/stopped.
- `complete` **MUST** be used for all acute authorisations.


### intent ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Code</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Used to distinguish between authorisations and medication issues.

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

The medication the authorisation is for.

The Medication resource provides the coded representation of the medication.


### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Who the medication is for, i.e. who it will be administered to.

Reference to patient.


### context ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Encounter)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The `Encounter` within which the medication was authorised.

As per base profile guidance.


### authoredOn ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Authorisation date, when the medication was authorised.

Unless there is a distinct user modifiable availabilityTime for the authorisation, this is the audit trail dateTime for when the authorisation was entered.


### requester ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Person and their organization requesting authorisation for prescription.

To be used if the medication was prescribed at another practice and has been imported via GP2GP. In that case, the `onBehalfOf` **MUST** be completed with a reference to the other organisation. 

If the medication has been prescribed elsewhere and, for example, is detailed in the sending system as a hospital medication, this **MUST** be detailed using an `organisation.type` code in the agent reference in the requester element.


### recorder ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Practitioner)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The responsible `Practitioner` who authorised the medication.

May not always be the user who entered the record on the system but, where a system supports attribution to a responsible clinician, the attributed clinician **MUST** be referenced here.


### reasonCode ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

The coded reason for authorising the medication.


### reasonReference ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Condition), Reference(Observation)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

References the condition or observation that was the reason for this authorisation.

Unless there is a specific linkage in the context of medication, indirect linkages to be handled via Problem list.


### note ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Annotation</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..*</td>
  </tr>
</table>

All notes that are associated with this medication record.

Sometimes labelled Pharmacy text or instructions for pharmacy.


### dosageInstruction.text ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Complete dosage instructions as text.


### dosageInstruction.patientInstruction ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>String</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Additional instructions for patient, i.e. RHS of prescription label.


### dispenseRequest.validityPeriod ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Period</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Prescription start and end dates.

Start date is mandatory. Where there is a defined expiry or end date the end date **MUST** be supplied. For acute prescriptions no specific end date **SHALL** be supplied.


### dispenseRequest.quantity ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>SimpleQuantity</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The quantity to dispense.

If the units are text then the extension dispenseRequest.quantityText **MUST** be used.


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

Number of days supply per dispense.


### dispenseRequest.performer ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organization)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Nominated pharmacy for dispense.


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


### repeatInformation ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Extension</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Extension elements to hold details of repeat authorisation.


### repeatInformation.numberOfRepeatPrescriptionsAllowed ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>PositiveInt</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The number of repeat issues authorised if specified.

**MUST** be present where a repeat is authorised for a defined number of issues. 

**MUST NOT** be specified for acute medications or where the number of repeat issues has not been defined. There is no concept of an initial dispense in GP Connect usage. Therefore, the `numberOfRepeats` allowed is the total number of allowed issues.


### repeatInformation.numberOfRepeatPrescriptionsIssued ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>PositiveInt</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Running total of number of issues made against a repeat authorisation.

Must be zero, if not yet issued.


### repeatInformation.authorisationExpiryDate ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>dateTime</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The date a repeat prescription authorisation will expire.


### prescriptionType ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension (prescriptionType)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

If a medication is an acute, delayed acute, repeat, repeat dispense or prescribed elsewhere.	

Explicit repeat or acute flag rather than deriving it from presence of extension elements or repeatNumber.


### statusReason ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension (statusReason)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

Where a medication has been stopped (status == ‘stopped’), the reason is provided in the statusReason extension.

Mandatory for authorisations with stopped status.


### statusReason.date ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension (valueDateTime)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The dateTime the medication was stopped/discontinued.

Mandatory for stopped/discontinued medications as the date will always be known.

### statusReason.reason ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>extension (CodeableConcept)</code></td>
    <td><b>Optionality:</b> Required</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The textual reason either free text or the term of a code for stopping/discontinuing the medication.

Must be populated when StatusReason.date is populated.


<br>
## Elements **not in use** ##

The following elements **MUST NOT** be populated:

<h3 style="color:#ED1951;"><b>definition</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(ActivityDefinition, PlanDefinition)</code></td>
  </tr>
</table>

Not in scope for this release of Care Connect.


<h3 style="color:#ED1951;"><b>category</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
  </tr>
</table>

Not in scope for this release of Care Connect. 


<h3 style="color:#ED1951;"><b>priority</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>code</code></td>
  </tr>
</table>

Not in scope for this release of Care Connect. 


<h3 style="color:#ED1951;"><b>supportingInformation</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Any)</code></td>
  </tr>
</table>

Not in scope for this release of Care Connect. 



<h3 style="color:#ED1951;"><b>substitution</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>BackboneElement</code></td>
  </tr>
</table>

Not in scope for this release of Care Connect. 


<h3 style="color:#ED1951;"><b>eventHistory</b></h3>

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Provenance)</code></td>
  </tr>
</table>

Not in scope for this release of Care Connect.  


