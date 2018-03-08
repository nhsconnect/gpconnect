---
title: FHIR Examples
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples.html
summary: "Acess Record Structured FHIR examples"
---

## Allergies ##

Example of response to getstructuredrecord request with includeAllergies and includeResolvedAllergies set to true

For the purposes of the example it is assumed that there is a single resolved allergy present.

- The GP Connect API is not a full FHIR RESTful interface - therefore not all resources returned are directly accessible
- The message conventions reflect this e.g. fullURLs for individual resources are not provided
- It is assumed that the querying system already has patient details so no patient resource is returned, instead the patient is referenced by identifier (NHS #)

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Bundle xmlns="http://hl7.org/fhir">
   <meta>
      <!-- Time response generated -->
      <lastUpdated value="2018-03-01T10:57:34+00:00" />
   </meta>
   <type value="searchset" />
   <entry>
      <resource>
         <List>
            <meta>
               <!-- TO DO: Confirm GP Connect list resource - not curated yet-->
               <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-List-1" />
            </meta>
            <status value="current" />
            <mode value="snapshot" />
            <title value="Active Allergies" />
            <code>
               <coding>
                  <system value="http://snomed.info/sct" />
                  <code value="TBD" />
                  <display value="Active Allergies" />
               </coding>
            </code>
            <date value="2018-03-01T10:57:34+00:00" />
            <subject>
               <identifier>
                  <system value="https://fhir.nhs.uk/Id/nhs-number" />
                  <value value="1234567890" />
               </identifier>
            </subject>
            <orderedBy>
               <coding>
                  <system value="http://hl7.org/fhir/list-order" />
                  <code value="event-date" />
               </coding>
            </orderedBy>
            <entry>
               <item reference="AllergyIntolerance/6bff710a-0bdc-4c9b-b98b-40db0a107edc" />
            </entry>
            <entry>
               <item reference="AllergyIntolerance/5eb0f76a-cecb-4b83-999d-ddb76e551a9b" />
            </entry>
            <entry>
               <item reference="AllergyIntolerance/d92b7d42-554d-4c92-b829-e76508185702" />
            </entry>
         </List>
      </resource>
   </entry>
   <entry>
      <resource>
         <List>
            <meta>
               <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Allergies-List-1" />
            </meta>
            <status value="current" />
            <mode value="snapshot" />
            <title value="Resolved Allergies" />
            <code>
               <coding>
                  <system value="http://snomed.info/sct" />
                  <code value="TBD" />
                  <display value="Resolved Allergies" />
               </coding>
            </code>
            <date value="2018-03-01T10:57:34+00:00" />
            <contained>
               <AllergyIntolerance>
                  <id value="res-1" />
                  <meta>
                     <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1" />
                  </meta>
                  <clinicalStatus value="resolved" />
                  <verificationStatus value="unconfirmed" />
                  <type value="intolerance" />
                  <category value="medication" />
                  <criticality value="low" />
                  <code>
                     <coding>
                        <extension url="https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid">
                           <extension url="DescriptionID">
                              <valueId value="56962301000001119" />
                           </extension>
                           <extension url="DescriptionDisplay">
                              <valueString value="Aspirin 75mg dispersible tablets" />
                           </extension>
                        </extension>
                        <system value="http://snomed.info/sct" />
                        <code value="319773006" />
                        <display value="Aspirin 75mg dispersible tablet (product)" />
                     </coding>
                  </code>
                  <!-- Logical reference to patient -->
                  <patient>
                     <identifier>
                        <system value="https://fhir.nhs.uk/Id/nhs-number" />
                        <value value="1234567890" />
                     </identifier>
                  </patient>
                  <recorder>
                     <reference value="Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21" />
                  </recorder>
                  <assertedDate value="2011-05-07" />
                  <note>
                     <text value="Allergy Type: Adverse Reaction, Certainty: Absolute, Severity: Very Severe, NOTES: Some freetext notes" />
                  </note>
                  <reaction>
                     <severity value="severe" />
                     <manifestation>
                        <coding>
                           <extension url="https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid">
                              <extension url="DescriptionID">
                                 <valueId value="2647992016" />
                              </extension>
                              <extension url="DescriptionDisplay">
                                 <valueString value="Emesis" />
                              </extension>
                           </extension>
                           <system value="http://snomed.info/sct" />
                           <code value="422400008" />
                           <display value="Vomiting (disorder)" />
                        </coding>
                     </manifestation>
                  </reaction>
               </AllergyIntolerance>
            </contained>
            <subject>
               <identifier>
                  <system value="https://fhir.nhs.uk/Id/nhs-number" />
                  <value value="1234567890" />
               </identifier>
            </subject>
            <orderedBy>
               <coding>
                  <system value="http://hl7.org/fhir/list-order" />
                  <code value="event-date" />
               </coding>
            </orderedBy>
            <entry>
               <item reference="#res-1" />
            </entry>
         </List>
      </resource>
   </entry>
   <entry>
      <resource>
         <AllergyIntolerance>
            <id value="6bff710a-0bdc-4c9b-b98b-40db0a107edc" />
            <meta>
               <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1" />
            </meta>
            <clinicalStatus value="active" />
            <verificationStatus value="unconfirmed" />
            <type value="allergy" />
            <category value="medication" />
            <criticality value="low" />
            <code>
               <coding>
                  <extension url="https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid">
                     <extension url="DescriptionID">
                        <valueId value="56966201000001112" />
                     </extension>
                     <extension url="DescriptionDisplay">
                        <valueString value="Amoxicillin 250mg capsules" />
                     </extension>
                  </extension>
                  <system value="http://snomed.info/sct" />
                  <code value="323509004" />
                  <display value="Product containing amoxicillin 250 mg/1 each oral capsule (clinical drug)" />
               </coding>
            </code>
            <!-- Logical reference to patient -->
            <patient>
               <identifier>
                  <system value="https://fhir.nhs.uk/Id/nhs-number" />
                  <value value="1234567890" />
               </identifier>
            </patient>
            <recorder>
               <reference value="Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21" />
            </recorder>
            <assertedDate value="2012-05-07T00:00+00:00" />
            <note>
               <text value="Certainty: Likely, Severity: Minimal, NOTES: Some freetext notes" />
            </note>
            <reaction>
               <severity value="mild" />
               <manifestation>
                  <coding>
                     <extension url="https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid">
                        <extension url="DescriptionID">
                           <valueId value="446685017" />
                        </extension>
                        <extension url="DescriptionDisplay">
                           <valueString value="O/E - itchy rash" />
                        </extension>
                     </extension>
                     <system value="http://snomed.info/sct" />
                     <code value="304386008" />
                     <display value="On examination - itchy rash (disorder)" />
                  </coding>
               </manifestation>
            </reaction>
         </AllergyIntolerance>
      </resource>
   </entry>
   <entry>
      <resource>
         <AllergyIntolerance>
            <id value="5eb0f76a-cecb-4b83-999d-ddb76e551a9b" />
            <meta>
               <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1" />
            </meta>
            <clinicalStatus value="active" />
            <verificationStatus value="unconfirmed" />
            <type value="allergy" />
            <category value="environental" />
            <criticality value="high" />
            <code>
               <coding>
                  <extension url="https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid">
                     <extension url="DescriptionID">
                        <valueId value="381850016" />
                     </extension>
                     <extension url="DescriptionDisplay">
                        <valueString value="Peanut - dietary" />
                     </extension>
                  </extension>
                  <system value="http://snomed.info/sct" />
                  <code value="256349002" />
                  <display value="Peanut - dietary (substance)" />
               </coding>
            </code>
            <patient>
               <identifier>
                  <system value="https://fhir.nhs.uk/Id/nhs-number" />
                  <value value="1234567890" />
               </identifier>
            </patient>
            <recorder>
               <reference value="Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21" />
            </recorder>
            <assertedDate value="2016-02-08T10:57:34+00:00" />
            <note>
               <text value="Certainty: Certain, Severity: Life Threatening, NOTES: notes on the peanut allergy" />
            </note>
            <reaction>
               <severity value="severe" />
               <manifestation>
                  <coding>
                     <extension url="https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid">
                        <extension url="DescriptionID">
                           <valueId value="362151013" />
                        </extension>
                        <extension url="DescriptionDisplay">
                           <valueString value="Peanut-induced anaphylaxis" />
                        </extension>
                     </extension>
                     <system value="http://snomed.info/sct" />
                     <code value="241933001" />
                     <display value="Peanut-induced anaphylaxis (disorder)" />
                  </coding>
               </manifestation>
            </reaction>
         </AllergyIntolerance>
      </resource>
   </entry>
   <entry>
      <resource>
         <AllergyIntolerance>
            <id value="d92b7d42-554d-4c92-b829-e76508185702" />
            <meta>
               <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1" />
            </meta>
            <clinicalStatus value="active" />
            <verificationStatus value="unconfirmed" />
            <type value="allergy" />
            <category value="medication" />
            <code>
               <coding>
                  <extension url="https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid">
                     <extension url="DescriptionID">
                        <valueId value="294801000000114" />
                     </extension>
                     <extension url="DescriptionDisplay">
                        <valueString value="Transfer-degraded drug allergy" />
                     </extension>
                  </extension>
                  <system value="http://snomed.info/sct" />
                  <code value="196461000000101" />
                  <display value="Transfer-degraded drug allergy (record artifact)" />
                  <text />
               </coding>
            </code>
            <patient>
               <identifier>
                  <system value="https://fhir.nhs.uk/Id/nhs-number" />
                  <value value="1234567890" />
               </identifier>
            </patient>
            <recorder>
               <reference value="Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21" />
            </recorder>
            <assertedDate value="2016-01-08T11:57:34+00:00" />
            <note>
               <text value="NOTES: This was entered incorrectly on the source system as a history/journal entry and not as a drug allergy" />
            </note>
         </AllergyIntolerance>
      </resource>
   </entry>
   <entry>
      <resource>
         <Practitioner>
            <id value="e0244de8-07ef-4274-9f7a-d7067bcc8d21" />
            <meta>
               <profile value="https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1" />
            </meta>
            <identifier>
               <system value="https://fhir.nhs.uk/Id/sds-user-id" />
               <value value="G8122438" />
            </identifier>
            <active value="true" />
            <name>
               <family value="Clarkson" />
               <given value="John" />
               <prefix value="Dr" />
            </name>
         </Practitioner>
      </resource>
   </entry>
</Bundle>
```
