---
title: MedicationStatement
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medicationstatement.html
summary: "Guidance for populating and consuming the MedicationStatement resource"
---

## Introduction ##

The table below shows you how to use each element of the MedicationStatement resource. You'll find it helpful to read it in conjunction with the underlying [MedicationStatement profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1).

## MedicationStatement element usage ##

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
       <td style="font-size: 13px"><code class="highlighter-rouge">basedOn</code></td>
       <td style="font-size: 13px">Link to the MedicationRequest that this MedicationStatement is ‘basedOn’</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (MedicationRequest)</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Every MedicationStatement MUST be baseOn a MedicationRequest with intent set to ‘plan’</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">partOf</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (MedicationAdministration, MedicationDispense, MedicationStatement, Procedure, Observation)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">context</code></td>
       <td style="font-size: 13px">The encounter within which the medication was authorised</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Encounter)</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">As per base profile guidance.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">status</code></td>
       <td style="font-size: 13px">The status of the authorisation.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">code</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Use one of active, completed or stopped: ‘active’ represents an active authorisation - used for active repeat medications, ‘stopped’ a repeat authorisation which has been discontinued/stopped, ‘complete’ **SHOULD** be used for all acute authorisations.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">category</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">medication</code></td>
       <td style="font-size: 13px">The medication the authorisation is for</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Medication)</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">The Medication resource provides the coded representation of the medication.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">effective</code></td>
       <td style="font-size: 13px">Start and end dates of this medication record.</td>
       <td style="font-size: 13px">
<code class="highlighter-rouge">dateTime</code> or <code class="highlighter-rouge">Period</code>
</td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">Start date is mandatory. Where there is a defined expiry or end date the end date **SHOULD** be supplied. For acute prescriptions no specific end date **SHOULD** be supplied.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dateAsserted</code></td>
       <td style="font-size: 13px">When this medication Statement was believed true</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">dateTime</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Unless there is a distinct user modifiable availabilityTime for the authorisation, this is the audit trail dateTime for when the authorisation was entered.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">informationSource</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Patient, Practitioner, RelatedPerson, Organization)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">subject</code></td>
       <td style="font-size: 13px">Who the medication is for, i.e. who it will be administered to.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Patient)</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Reference to patient</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">derivedFrom</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Any)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">taken</code></td>
       <td style="font-size: 13px">Whether a medication was taken.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">code</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px">Providers MUST use a default value of unk – unknown.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">reasonNotTaken</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">reasonCode</code></td>
       <td style="font-size: 13px">The coded reason for authorising the medication.</td>
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
       <td style="font-size: 13px">All notes that are associated with this medication record.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Annotation</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">All patient notes and prescriber notes at authorisation(plan) and issue(order) level **SHOULD** be included in this field. They **SHOULD** be concatenated and indicate the level the notes come from, e.g. 1st Issue and also be prefixed with either ‘Patient Notes:’ or ‘Prescriber Notes:’ as appropriate.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dosage/text</code></td>
       <td style="font-size: 13px">Complete dosage instructions as text</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">String</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">dosage/patient Instruction</code></td>
       <td style="font-size: 13px">Additional instructions for patient, i.e. RHS of prescription label.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">String</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px"> </td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">lastIssueDate</code></td>
       <td style="font-size: 13px">When the medication was last issued.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">dateTime</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
       <td style="font-size: 13px">This will be the authored on field for the most recent MedicationRequest with an intent of ‘order’. For repeat dispense this will be the latest ValidityPeriod/start date that is not in the future.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">medicationEpisode ChangeSummary</code></td>
       <td style="font-size: 13px">DO NOT USE</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Complex Extension</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Guidance</td>
    </tr>
  </tbody>
</table>
