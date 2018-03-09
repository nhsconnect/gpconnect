---
title: MedicationRequest
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medicationrequest.html
summary: "Guidance for populating and consuming the MedicationRequest resource"
div: resource-page
---

## Introduction ##

The headings below list the elements of the MedicationRequest resource and describe how to populate and consume them.

{% include important.html content="Any element not specifically listed below **SHOULD NOT** be populated or consumed." %}

{% include tip.html content="You'll find it helpful to read it in conjunction with the underlying [MedicationRequest profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1)" %} 

## Overarching principles ##

When populating the MedicationRequest profile it may appear that fields are duplicated in other associated resources. In the interests of minimising redundancy, the 2 following principles **SHOULD** be applied when populating the MedicationRequest profiles:

1. All mandatory fields MUST be populated.

2. Required fields **SHOULD** always be populated where the data exists in the system apart from where a lexically identical value exists for an equivalent data item in one of the parent profiles. For a MedicationRequest with `intent` of `plan` the associated MedicationStatement would be the parent profile. For a MedicationRequest with `intent` of `order`, the associated MedicationStatement and MedicationRequest with `intent` of `plan` are both considered parent profiles.

## MedicationRequest elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The logical identifier of the MedicationRequest resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

The MedicationRequest profile URL.

Fixed value [https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1)





## MedicationRequest element usage ##

<table>
  <thead>
    <tr>
      <th>Element</th>
      <th>Usage</th>
      <th>Datatype</th>
      <th style="text-align: center">Optionality</th>
      <th>Guidance</th>
    </tr>
  </thead>
  <tbody>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">identifier</code></td>
       <td style="font-size: 13px">Logical identifier for resource</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Identifier</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Refer to generic guidance</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">definition</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (ActivityDefinition, PlanDefinition)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">basedOn</code></td>
       <td style="font-size: 13px">To use for intent=’order’ resources that are based on an intent=’plan’ resource</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (CarePlan, MedicationRequest, ProcedureRequest, ReferralRequest)</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">Do not use for authorisations (intent of ‘plan’) - it is valid for issue which would always be basedOn the MedicationRequest authorisation resource.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">groupIdentifier</code></td>
       <td style="font-size: 13px">Composite request this is part of</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Identifier</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">All repeat prescribed and repeat dispensed medications **SHOULD** have a group identifier that is populated for the ‘plan’ and all ‘orders’ relating to them.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">status</code></td>
       <td style="font-size: 13px">The status of the authorisation</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">code</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Use one of active, completed or stopped: ‘active’ represents an active authorisation - used for active repeat medications, ‘stopped’ a repeat authorisation which has been discontinued/stopped, ‘complete’ **SHOULD** be used for all acute authorisations. ** Justification - if we were to use active for acute authorisations when would it transition to complete without introducing complicated date-based statuses (perhaps OK for a ‘current’ medication list but not necessarily OK here).</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">intent</code></td>
       <td style="font-size: 13px">Distinguished between authorisations and medication issues</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">code</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">‘plan’ represents an authorisation, ‘order’ represents a prescription issue</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">category</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">priority</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">code</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">medication</code></td>
       <td style="font-size: 13px">The medication the authorisation is for.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Medication)</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">The Medication resource provides the coded representation of the medication.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">subject</code></td>
       <td style="font-size: 13px">Who the medication is for, i.e. who it will be administered to.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Patient)</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Reference to patient</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">context</code></td>
       <td style="font-size: 13px">The encounter within which the medication was authorised.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Encounter)</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">As per base profile guidance.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">supportingInformation</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Any)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">D</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">authoredOn</code></td>
       <td style="font-size: 13px">Authorisation date, when the medication was authorised.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">dateTime</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Unless there is a distinct user modifiable availabilityTime for the authorisation, this is the audit trail dateTime for when the authorisation was entered.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">requester</code></td>
       <td style="font-size: 13px">Person and their organization requesting authorisation for prescription</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">BackboneElement</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">To be used if the medication was prescribed at another practice and has been imported via GP2GP. In that case, the onBehalfOf **SHOULD** be completed with a reference to the other organisation. If the medication has been prescribed elsewhere and, for example, is detailed in the sending system as a hospital medication, this MUST be detailed using an organisation.type code in the agent reference in the requester element.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">recorder</code></td>
       <td style="font-size: 13px">The responsible practitioner who authorised the medication</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Practitioner)</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">May not always be the user who entered the record on the system but, where a system supports attribution to a responsible clinician, the attributed clinician **SHOULD** be referenced here.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">reasonCode</code></td>
       <td style="font-size: 13px">The coded reason for authorising the medication</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">reasonReference</code></td>
       <td style="font-size: 13px">References the condition or observation that was the reason for this authorisation.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Condition, Observation)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Unless there is a specific linkage in the context of medication, indirect linkages to be handled via Problem list.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">note</code></td>
       <td style="font-size: 13px">Notes for dispenser</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Annotation</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">Sometimes labelled Pharmacy text or instructions for pharmacy.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dosageInstruction.text</code></td>
       <td style="font-size: 13px">Complete dosage instructions as text</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">String</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dosageInstruction.patientInstruction</code></td>
       <td style="font-size: 13px">Additional instructions for patient, i.e. RHS of prescription label.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">String</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dispenseRequest.validityPeriod</code></td>
       <td style="font-size: 13px">Prescription start and end dates.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Period</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Start date is mandatory. Where there is a defined expiry or end date the end date **SHOULD** be supplied. For acute prescriptions no specific end date **SHOULD** be supplied.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dispenseRequest.numberOfRepeatsAllowed</code></td>
       <td style="font-size: 13px">The number of repeat issues allowed for repeat and repeat dispensed medications where specified</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">positiveInt</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">DO NOT USE - use the extension repeatInformation.numberOfRepeatPrescriptionsAllowed.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dispenseRequest.quantity</code></td>
       <td style="font-size: 13px">The quantity to dispense.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">SimpleQuantity</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">If the units are text then the extension dispenseRequest.quantityText **SHOULD** be used.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dispenseRequest.quantityText</code></td>
       <td style="font-size: 13px">Textual representation of quantity.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">String</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">Only to be used if there is no numerical value.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dispenseRequest.expectedSupplyDuration</code></td>
       <td style="font-size: 13px">Number of days’ supply per dispense.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Duration</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dispenseRequest.performer</code></td>
       <td style="font-size: 13px">Nominated pharmacy for dispense.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Organization)</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">substitution</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">BackboneElement</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">priorPrescription</code></td>
       <td style="font-size: 13px">References prior prescription authorisation.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (MedicationRequest)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">May be used, for example, to reference prior authorisation where prescription is re-authorised or where amendments have been made. May reference the previous authorisation before the amendment.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">eventHistory</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Provenance)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">repeatInformation</code></td>
       <td style="font-size: 13px">Extension elements to hold details of repeat authorisation.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Extension</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">repeatInformation. numberOfRepeat PrescriptionsAllowed</code></td>
       <td style="font-size: 13px">The number of repeat issues authorised if specified.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">PositiveInt</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">Must be present where a repeat is authorised for a defined number of issues. Must not be specified for acute medications or where the number of repeat issues has not been defined. There is no concept of an initial dispense in GP Connect usage. Therefore, the numberOfRepeats allowed is the total number of allowed issues.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">repeatInformation.numberOfRepeat PrescriptionsIssued</code></td>
       <td style="font-size: 13px">Running total of number of issues made against a repeat authorisation.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">PositiveInt</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Must be Zero, if not yet issued.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">repeatInformation.authorisationExpiryDate</code></td>
       <td style="font-size: 13px">The date a repeat prescription authorisation will expire.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">dateTime</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">PrescriptionType</code></td>
       <td style="font-size: 13px">If a medication is an acute, delayed acute, repeat, repeat dispense or prescribed elsewhere.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Code</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Explicit repeat or acute flag rather than deriving it from presence of extension elements or repeatNumber.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">StatusReason</code></td>
       <td style="font-size: 13px">Where a medication has been stopped (status == ‘stopped’), the reason is provided in the statusReason extension.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">extension (StatusReason)</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">Mandatory for authorisations with stopped status.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">StatusReason.date</code></td>
       <td style="font-size: 13px">The dateTime the medication was stopped/discontinued.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">extension (valueDateTime)</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Mandatory for stopped/discontinued medications as the date will always be known.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">StatusReason.Reason</code></td>
       <td style="font-size: 13px">The textual reason either free text or the term of a code for stopping/discontinuing the medication.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Extension (valueString)</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">Must be populated when StatusReason.date is populated.</td>
    </tr>
  </tbody>
</table>
