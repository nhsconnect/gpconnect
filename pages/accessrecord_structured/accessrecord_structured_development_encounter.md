---
title: Consultation
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_guidance_consultation.html
summary: "Guidance for the representation and consumption of Consultations"
---
## Encounter elements ##

### id ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Id</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The logical identifier of the Encounter resource.

### meta.profile ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>uri</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

The Encounter profile URL.

### identifier ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Identifier</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..*</td>
  </tr>
</table>

This is for business identifiers.

This is sliced to include a cross care setting identifier which MUST be populated. The codeSystem for this identifier is `https://fhir.nhs.uk/Id/cross-care-setting-identifier`.

### status ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>status</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Fixed value of **finished**. 

Existing vocabulary is driven by use of Encounter for appointment style encounters rather than provision of consultation context. Hence use most appropriate value from limited set available.

### statusHistory ###

Not used.

### class ###

Not used.

###  classHistory ###

Not used.

### type ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>CodeableConcept</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Carries the consultation type as displayed by system via #.text#

TO DO - resolve potential for coding allowing for likely vaguess lack of exact mapping in available codes. Would need definition of appropriate vocabulary. Question value of coding but certainly something that may be of interest.

### priority ###

Not used.

### subject ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Patient)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to Patient resource representing the Patient against whom the source consultation/encounter was recorded.

### episodeOfCare ###

Not used

### incomingReferral ###

TO DO: interesting because SystemOne supports this linkage for inbound referrals

### participant ###

Yes - need to look at whether there are appropriate codes vocabularies to define author, primary performer erc ....

### appointment ###

Do we want it ????? Would seem a shame not to hasve it?


### period ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Period</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> </td>
  </tr>
</table>

**.start** is mandatory and should be populated with the displayed consultation date and time 

**.end** should be populated where the encounter end date and time is known or calculated and populated where the duration is known.

The audit trail date time of the consultation is carried by **Composition.date**

### length ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Duration</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> </td>
  </tr>
</table>

Specifies the length of the consultation. Should be calculated and populated where an end time for the consultation is known.

### reason ###

Not used

### diagnosis ###

Not used

### account ###

Not used

### hospitalization ###

Not used

### location ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Location)</code></td>
    <td><b>Optionality:</b> Optional</td>
    <td><b>Cardinality:</b> 0..1</td>
  </tr>
</table>

References an instances of the Location resource that provides more detail on where the Consultation/encounter took place e.g. Branch surgery.

**.status** and **.period** are not used

### serviceProvider ###

<table class='resource-attributes'>
  <tr>
    <td><b>Data type:</b> <code>Reference(Organization)</code></td>
    <td><b>Optionality:</b> Mandatory</td>
    <td><b>Cardinality:</b> 1..1</td>
  </tr>
</table>

Reference to the responsible organisation for the encounter.

### partOf ###

Not used.
