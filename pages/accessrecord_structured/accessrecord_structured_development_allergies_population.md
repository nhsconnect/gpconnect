---
title: Population
keywords: getcarerecord
tags: [getcarerecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_allergies_population.html
summary: "Guidance for populating and reading the AllergyIntolerance resource"
---

The table below shows you how to use each element of the AllergyIntolerance resource. You'll find it helpful to read it in conjunction with the underlying [AllergyIntolerance resource definition](https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1).

## AllergyIntolerance element usage ##

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
      <td style="font-size: 13px"><code class="highlighter-rouge">EndDate</code></td>
      <td style="font-size: 13px">The date the allergy or intolerance was recorded as resolved.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Extension (valueDateTime)</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
      <td style="font-size: 13px">Must be populated if the status is set to ‘resolved’.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">EndReason</code></td>
      <td style="font-size: 13px">The reason why the allergy or intolerance has been resolved.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Extension (valueString)</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
      <td style="font-size: 13px"> </td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">Evidence</code></td>
      <td style="font-size: 13px">Reference to confirmatory diagnostic report, e.g. pathology RAST test result.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Extension (valueReference)</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px"> </td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">clinicalStatus</code></td>
      <td style="font-size: 13px">‘active’ for all active allergies. ‘resolved’ for resolved allergies.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Code</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
      <td style="font-size: 13px">Producers which support the concept of resolved/ended allergies **SHOULD** set the clinicalStatus of resolved allergies to ‘resolved’.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">verificationStatus</code></td>
      <td style="font-size: 13px">Fixed value of ‘unconfirmed’</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Code</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
      <td style="font-size: 13px">DO NOT USE - this value is mandatory in base FHIR so cannot be removed. It is not a concept in GP systems and as such no meaning **SHOULD** be attributed to this field in consuming systems.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">type</code></td>
      <td style="font-size: 13px">Set to ‘allergy’ for reactions which are allergenic in nature (immunological), a value of ‘intolerance may be used to indicate Adverse Reactions (not immunologic in nature). Where the type is unknown the type element may be omitted.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Code</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px">Some systems allow explicit identification of Adverse Reactions and Intolerances and the type **SHOULD** be used to make this distinction where it exists.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">category</code></td>
      <td style="font-size: 13px">Use ‘medication’ for all drug allergy types, ‘environmental’ for all non-drug allergies. The other values in the ValueSet (food and biologic) **SHOULD NOT** be used by convention.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Code</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
      <td style="font-size: 13px">See note on ‘AllergyIntolerance Category’.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">criticality</code></td>
      <td style="font-size: 13px">Distinguishes between life-threatening (high) and non-life-threatening (low) potential as well as unable-to-assess. May be used in addition to severity within the reaction element to express severity, e.g. systems that support a severity of life-threatening may set criticality to high.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Code</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px">May be used in conjunction with reaction/severity by systems which support a severity of ‘Life Threatening’ or equivalent.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">code</code></td>
      <td style="font-size: 13px">The causative agent such as food, drug or substances that has caused or may cause an allergy, intolerance or adverse reaction in this patient.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
      <td style="font-size: 13px">Systems will evolve to use the specified vocabulary of SNOMED CT concepts from the specified subset. The subset includes products and concepts from the substance and product hierarchies and allows medication concepts from the dm+d SNOMED CT extension. In the interim this coded element will hold the primary code for the AllergyIntolerance which may in the case of drug allergies be a medication code or a pre-coordinated code which triggers decision support on the system. Where the AllergyIntolerance has no coded representation in the source system, but is identified as such in the source record then the appropriate degrade code may be used and the text of the AllergyIntolerance placed in the text of the code.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">onset[dateTime]</code></td>
      <td style="font-size: 13px">Date when allergy/intolerance first manifested. Currently restricted to values of dateTime for GP Connect provider systems.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">dateTime</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
      <td style="font-size: 13px">Present and populated when the provider system records an explicit onset date for an allergy.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">assertedDate</code></td>
      <td style="font-size: 13px">The datetime the record was recorded or believed to be true.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">dateTime</code></td>
      <td style="text-align: center; font-size: 13px">M</td>
      <td style="font-size: 13px">The asserted date is when the allergy related to the patient was asserted. In many cases, this will be when the allergy is entered onto the system, although some systems may allow this date to be modified.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">lastOccurrence</code></td>
      <td style="font-size: 13px">Represents the date and/or time of the last known occurrence of a reaction event.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">dateTime</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px">May not currently be available from participating systems and may be omitted. Ommission **SHOULD NOT** prejudice the ability of providers and consumers to process this element if and when it is available.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">note</code></td>
      <td style="font-size: 13px">All text associated with the AllergyIntolerance including user-entered notes and qualifiers is grouped together and expressed in this field. Ensures unmapped coded values or qualifiers are not lost.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Annotation</code></td>
      <td style="text-align: center; font-size: 13px">R</td>
      <td style="font-size: 13px">Must be used to contain any textual data relevant to the allergy.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">reaction.note</code></td>
      <td style="font-size: 13px">NOT TO BE USED</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Annotation</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px">AllergyIntolerance.note **SHOULD** contain all of the consolidated text from the allergy/intolerance.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">reaction.manifestation</code></td>
      <td style="font-size: 13px">Conveys the reaction resulting from the allergy/intolerance as a code. Where no code is available, but a textual description of the reaction is available then the nullFlavor UNC may be used and the textual description conveyed via reaction/description. If no reaction has explicitly been recorded, but the reaction element is present to convey severity, then reaction/manifestation **SHOULD** be coded as the nullFlavor NI. If the patient has been asked, but is unable to specify a reaction the nullFlavor, ‘ASKU’ **SHOULD** be used.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px"> </td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">reaction.description</code></td>
      <td style="font-size: 13px">Conveys the textual description of the manifestation where no code is available.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">String</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px">A consuming system may concatenate the contents (appropriately labelled) with text in AllergyIntolerance.note if a textual description of the manifestation is not supported in the receiving system record structure.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">reaction.severity</code></td>
      <td style="font-size: 13px">Severities of mild, moderate, severe are mapped directly to the FHIR ValueSet. Map life threatening to severe and populate criticality with high.</td>
      <td style="font-size: 13px">`Code’</td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px">Unmapped or converted severity codes in original system **SHOULD** be expressed in AllergyIntolerance.note.</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">reaction.exposureRoute</code></td>
      <td style="font-size: 13px">The route by which exposure to the substance causing the reaction occurred. Utilise the dm+d route codes.</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px"> </td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">reaction.onset[x]</code></td>
      <td style="font-size: 13px">NOT TO BE USED</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">Choice</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px">Onset explicitly supplied via AllergyIntolerance.onset[dateTime].</td>
    </tr>
    <tr>
      <td style="font-size: 13px"><code class="highlighter-rouge">reaction.substance</code></td>
      <td style="font-size: 13px">NOT TO BE USED</td>
      <td style="font-size: 13px"><code class="highlighter-rouge">CodeableConcept</code></td>
      <td style="text-align: center; font-size: 13px">O</td>
      <td style="font-size: 13px">The causative is explicitly and specifically coded via AllergyIntolerance.code.</td>
    </tr>
  </tbody>
</table>
