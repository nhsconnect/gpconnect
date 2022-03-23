---
title: Immunisation guidance
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_immunization_guidance.html
summary: "Guidance for populating and consuming the Immunization FHIR&reg; resource"
---

## What is immunisation?

Immunisation is the process by which an individual's immune system becomes fortified against an agent (known as the immunogen).

When this system is exposed to molecules that are foreign to the body, called non-self, it will orchestrate an immune response, and it will also develop the ability to quickly respond to a subsequent encounter because of immunological memory.
This is a function of the adaptive immune system.
Therefore, by exposing a person to an immunogen in a controlled way, the person's body can learn to protect itself: this is called active immunisation.

## What is a vaccination?

Vaccination is the administration of a vaccine to help the immune system develop protection from a disease.
Vaccines contain a microorganism or virus in a weakened or killed state, or proteins or toxins from the organism.
In stimulating the body's adaptive immunity, they help prevent sickness from an infectious disease.
When a sufficiently large percentage of a population has been vaccinated, herd immunity results.
The effectiveness of vaccination has been widely studied and verified.
Vaccination is the most effective method of preventing infectious diseases; widespread immunity due to vaccination is largely responsible for the worldwide eradication of smallpox and the elimination of diseases such as polio and tetanus from much of the world.

## What immunisation data is GP Connect sending?

In GP Connect, what is sent in the `Immunization` resource is the event of a patient being administered a vaccination or where there is an intention to administer a vaccine which does not occur.
This may be a contemporaneous record by the clinician administering the vaccination (or by another member of the practice staff recording the event directly on behalf of the clinician) or it may be a record of an immunisation administered elsewhere as reported to the registered GP practice by the patient, a carer, guardian or other representative of the patient or another healthcare provider.

A record of an immunisation may be created as part of a scheduled programme of immunisations such as childhood immunisations, seasonal influenza vaccination or in response to specific circumstances (for example, prior to travel, disease outbreak or occupational risk).

If a vaccination is recorded as an issued medication, the details of the issued medication are not included in the immunisations response.
The medication details **MUST** be sent as medication resources (if the consumer requests medications). 
This may be in addition to an immunisation resource for the event of the vaccination administration, depending on how the immunisation event was recorded. 

## Using the procedure code

GP clinical systems do not all record the full vaccine product (dm+d code) for an immunisation.
GP clinical systems often record the type of vaccine administered as opposed to the vaccine product.
This may be as a procedure code or a local code which can be mapped to a procedure code.
GP Connect, therefore, uses the vaccination procedure code to denote the vaccine being administered.
The vaccination procedure code is a mandatory element.
The vaccine product code will often be a `nullFlavor` code, but the actual vaccine product **MUST** be included if it is available.

## Vaccinations that were not given

GP clinical systems may capture details of circumstances where an immunisation has not been given but there was an intention to.
This version of the specification supports inclusion of intended vaccinations which were not given as defined by Digital Child Health.
For details of the requirements see [National Events Management Service - Vaccinations](https://developer.nhs.uk/apis/ems-beta/vaccinations_1.html) or versions as subsequently published.
If the GP clinical system holds a coded record of an intended, not given vaccination which is either outside of the scope of the 'not done' situation codes or the required code is not available, then the coded information should be included in an uncategorised data response.

Consumers should be aware that the presence of a vaccination not given record is only in relation to an intended vaccination event on a given day - that is, it is not stating the vaccination has definitely never been given.

### Populating elements for an immunisation not given

Specific rules are applied to the population of some of the elements where the record is for an intended immunisation which was not given.
A few of these are highlighted here.

The provider **MUST** populate elements as described below when sending details of immunisations not given within the immunisation resource.

* <code>extension[vaccinationProcedure]</code> **MUST** be the SNOMED CT 'not done' situation code for the vaccination which was intended but did not happen
* <code>notGiven</code> **MUST** be <code>true</code>
* <code>explanation.reasonNotGiven</code> **SHOULD** be included with the appropriate code for the reason the vaccination did not happen

See [immunization](accessrecord_structured_development_immunization.html) for full details of the elements.

### Consumer handling of immunisations not given

Consumer systems are to determine whether to request details of immunisations not given.
A consumer system which requires not given immunisations **MUST** request this by specifying the part parameter.
The default is to return given immunisations only.

Where a consumer system has requested immunisations not given, it **MUST** ensure that the not given data remains clearly distinct from given vaccinations. The consumer **MAY** need to handle <code>explanation.reasonNotGiven</code> alongside the "not done" code to provide the classified reason the vaccination was not given.

## Additional information about vaccinations 

The above section addresses circumstances where an immunisation is not given at the point of intending to give the vaccine.
GP Systems may capture other coded information relating to vaccinations other than the administration of the vaccine in an immunisations feature / module / categorisation.
This may be information regarding consent, dissent, invitations for vaccination, etc.
Where provider categorise such coded information as immunisation data, then it **MUST** only return it against an immunisation request.
GP Connect includes the parameter `includeStatus` to enable the consumer to specify the inclusion / exclusion of this information.
See [Retrieve a patient's structured record](accessrecord_structured_development_retrieve_patient_record.html) for full details of the parameter use.

Such coded records **MUST** be included with the immunisation bundle using an <code>observation</code> resource, as defined for [uncategorised data](accessrecord_structured_development_observation_uncategoriseddata.html).

Records returned against an immunisation request under the scope of this definition **MUST** be 
- excluded from the records returned for an uncategorised data request
- included in the immunisations `List`

Consumers shoud note than GP Systems differ with respect to additional information categorised as immunisations, therefore the same coded data may be returned against an immunisation or uncategorised data request by different provider systems.

### Ended records

Where a GP clinical system allows a consent or dissent to be ended, then the <code>observation.effective</code> element **MUST** be populated with a <code>Period</code> including the relevant start and end dates.

This does not apply if the consent or dissent has been ended as "entered in error", in which case the record **MUST NOT** be included.

### Multiple records

If a patient record has multiple records of consent for a single type of vaccination, for example a dissent and a consent, then all records **MUST** be included.

### Degraded records

Any records which the GP clinical systems classifies as an immunisation consent or dissent, but which do not appear in the hierarchies above **MUST** also be included.
Where there is an appropriate code which is outside of the stated hierarchy, then that **MAY** be used.
Where there is no identifiably appropriate SNOMED CT code for the consent or dissent, then the transfer degraded code **MUST** be used with a text element populated with the original text.

ConceptId - <code>196411000000103</code>
DescriptionId - <code>294691000000115</code>
Description - <code>Transfer-degraded record entry</code>

## Ineffective vaccination

The Immunization FHIR profile contains elements to denote that a vaccination does not count towards immunity.
This could be applied where a vaccination is suspected or found to be ineffective, for example as a result of a product recall or cold chain break.
GP clinical systems do not have a standard means to identify an ineffective vaccination.
Hence, immunisation records will always be returned as counting towards immunity.

## Reactions to a vaccine

Allergic or adverse reactions to an immunisation may be captured in the GP clinical system, but these are not generally directly associated to the immunisation event.
It has not been considered reliable to link any allergic or adverse reaction to the immunisation record.
Therefore, information about reactions will not be included.
For details of allergies or adverse reaction, the `AllergyIntolerance` resource **MUST** be requested.

## Immunisation schedules and recalls

The resources required to describe planned immunisation schedules are out of scope for this guidance.
According to local practice, immunisations due may be recorded as recalls and retrieved via [Diary entries](accessrecord_structured_development_diaryentry_guidance.html).

## Immunisation notes

GP systems that support a note entry against the immunisation **MUST** populate the text to the <code>note</code> element.
Additionally, any other information relevant to the immunisation which does not have a suitable, supported element within the `Immunization` resource **MUST** be populated to the <code>note</code> as a key value pair.
This includes where there is an element in the profile for the type of information, but the data type is not compatible with the way the data is recorded in the GP system.
For example, if the GP system holds the dosage information in a format which does not comply with the <code>doseQuantity</code> element's <code>Quantity</code> datatype, then it may be returned as a note key value pair.

## Using the `List` resource for immunisation queries

The results of a query for immunisation details **MUST** return a `List` containing references to all `Immunization` and `Observation` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason.code` with the value `no-content-recorded`. In this case, `List.note` **MUST** be populated with the text 'Information not available'.
