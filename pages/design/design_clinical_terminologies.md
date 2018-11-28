---
title: Clinical terminologies
keywords: development
tags: [design,development]
sidebar: overview_sidebar
permalink: design_clinical_terminologies.html
summary: "Brief guidance on how clinical terminologies are expected to be used within GP Connect."
---

## UK Terminology Centre (UKTC) ## 

The [UKTC](http://systems.digital.nhs.uk/data/uktc){:target="_blank"} is responsible for the UK management of [SNOMED CT](http://systems.digital.nhs.uk/data/uktc/snomed){:target="_blank"}, [Read Codes](http://systems.digital.nhs.uk/data/uktc/readcodes){:target="_blank"} and other healthcare terminology products.

The [UKTC](http://systems.digital.nhs.uk/data/uktc){:target="_blank"} also maintains the [NHS Dictionary of Medicines and Devices (dm+d)](http://www.nhsbsa.nhs.uk/1121.aspx){:target="_blank"} in partnership with the NHS Business Service Authority.

### SNOMED CT, READ2 & CTV3 code usage ###

GP Connect systems are expected to handle coded data as follows:

- Data originally entered into a system using the preferred system (i.e. SNOMED CT)
	- SHALL be returned as SNOMED CT.
	- If no suitable code exists in the value set (i.e. if only text is available, then just text MAY be used).
- Data originally entered into a system using an alternate coding system (i.e. READ2 or CTV3)
	- SHALL be returned in the code system it was originally entered in (i.e. READ2 or CTV3) AND
	- SHALL also be returned as a preferred code (i.e. SNOMED CT) if a valid mapping/alternate code exists (i.e. there is a NHS Digital assured READ2 or CTV3 to SNOMED CT mapping in place).

#### Assured mappings ####

[Assured Mappings](https://isd.hscic.gov.uk/trud3/user/guest/group/2/pack/8){:target="_blank"} can be found in the **NHS Data Migration** download.

{% include important.html content="Updated assured mappings are released every 6 months; suppliers are expected to update their systems in-line with the timescales currently required under the GPSoC framework." %}


### Case Sensitivity of Terminologies ###
[FHIR Terminologies](https://www.hl7.org/fhir/terminologies.html#required){:target="_blank"}

Throughout this specification, coded values are always treated as a pair composed of "system" and "code", where the system is a URL that identifies the code system that defines the codes. Note, that system values are always case sensitive. Different code systems make their own rules as to whether the codes they define are case sensitive or not. Note that all the codes defined by FHIR itself are case sensitive and SHALL be used in the provided case (usually, but not always, lowercase).