---
title: Clinical terminologies
keywords: development
tags: [design,development]
sidebar: overview_sidebar
permalink: design_clinical_terminologies.html
summary: "Brief guidance on how clinical terminologies are expected to be used within GP Connect"
---

## Terminology and classifications ## 

NHS Digital Information Standards(https://digital.nhs.uk/services/terminology-and-classifications){:target="_blank"} are responsible for the UK management of [SNOMED CT](https://digital.nhs.uk/services/terminology-and-classifications/snomed-ct){:target="_blank"}, [Read Codes](https://digital.nhs.uk/services/terminology-and-classifications/read-codes){:target="_blank"} and other healthcare terminology products.

They also maintain the [NHS Dictionary of Medicines and Devices (dm+d)](http://www.nhsbsa.nhs.uk/1121.aspx){:target="_blank"} in partnership with the NHS Business Service Authority.

### SNOMED CT, READ2 & CTV3 code usage ###

GP Connect systems are expected to handle coded data as follows:

- data originally entered into a system using the preferred system (that is, SNOMED CT)
  - SHALL be returned as SNOMED CT. The SNOMED CT DescriptionID should be included in addition to the ConceptID where available. The DescriptionID can convey a different meaning to the ConceptID due to the difference in the specific wording used for the two codes.
  - if no suitable code exists in the value set (that is, if only text is available, then just text MAY be used)
- data originally entered into a system using an alternate coding system (for example, READ2 or CTV3)
  - SHALL be returned in the code system it was originally entered in (for example, READ2 or CTV3) AND
  - SHALL also be returned as a preferred code (that is, SNOMED CT) if a valid mapping/alternate code exists (for example, there is an NHS Digital assured READ2 or CTV3 to SNOMED CT mapping in place)

#### Assured mappings ####

[Assured mappings](https://isd.hscic.gov.uk/trud3/user/guest/group/2/pack/8){:target="_blank"} can be found in the **NHS Data Migration** download.

{% include important.html content="Updated assured mappings are released every 6 months; suppliers are expected to update their systems in line with the timescales currently required under the GPSoC framework." %}


### Case sensitivity of terminologies ###
[FHIR terminologies](https://www.hl7.org/fhir/STU3/terminologies.html#required){:target="_blank"}

Throughout this specification, coded values are always treated as a pair composed of 'system' and 'code', where the system is a URL that identifies the code system that defines the codes. 

**Notes:**
 - system values are always case sensitive
 - different code systems make their own rules as to whether the codes they define are case sensitive or not 
 - all the codes defined by FHIR itself are case sensitive and SHALL be used in the provided case (usually, but not always, lowercase)
