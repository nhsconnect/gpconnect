---
title: Medication
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_medication.html
summary: "Guidance for populating and consuming the Medication resource"
---

## Introduction ##

The table below shows you how to use each element of the Medication resource. You'll find it helpful to read it in conjunction with the underlying [Medication profile definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1).

## Medication element usage ##

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
       <td style="font-size: 13px"><code class="highlighter-rouge">code</code></td>
      <td style="font-size: 13px">Medication code</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
      <td style="font-size: 13px">The code that identifies the medication. A dm+d code **SHOULD** always be supplied if possible. If not, then a code from another codesystem or the SNOMED degrade code (196421000000109, Transfer-degraded medication entry) MUST be supplied.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">status</code></td>
       <td style="font-size: 13px">If a medication is active or inactive</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">code</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Not necessary for this version of GP Connect.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">isBrand</code></td>
       <td style="font-size: 13px">True if a brand</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">boolean</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Not necessary for this version of GP Connect</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">isOverTheCounter</code></td>
       <td style="font-size: 13px">True if medication does not require a prescription</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">boolean</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Not necessary for this version of GP Connect.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">manufacturer</code></td>
       <td style="font-size: 13px">Manufacturer of the item</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Reference (Organization)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Not necessary for this version of GP Connect.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">form</code></td>
       <td style="font-size: 13px">The form of the medication, e.g. powder, tablets, capsule, etc.</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Not necessary for this version of GP Connect.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">ingredient</code></td>
       <td style="font-size: 13px">Active or inactive ingredient</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">BackboneElement</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Not necessary for this version of GP Connect.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">package</code></td>
       <td style="font-size: 13px">Details about packaged medications</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">BackboneElement</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">If the supplier has data relating to the batch number or expiry date they may be populated here.</td>
    </tr>
    <tr>
       <td style="font-size: 13px"><code class="highlighter-rouge">image</code></td>
       <td style="font-size: 13px">Picture of the medication</td>
       <td style="font-size: 13px"><code class="highlighter-rouge">Attachment</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
       <td style="font-size: 13px">Not necessary for this version of GP Connect.</td>
    </tr>
  </tbody>
</table>

