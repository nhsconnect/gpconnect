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

In GP Connect, what is sent in the `Immunization` resource is the event of a patient being administered a vaccination.
This may be a contemporaneous record by the clinician administering the vaccination (or by another member of the practice staff recording the event directly on behalf of the clinician) or it may be a record of an immunisation administered elsewhere as reported to the registered GP practice by the patient, a carer, guardian or other representative of the patient or another healthcare provider.

A record of an immunisation may be created as part of a scheduled programme of immunisations such as childhood immunisations, seasonal influenza vaccination or in response to specific circumstances (for example, prior to travel, disease outbreak or occupational risk).

## Using the procedure code

GP clinical systems do not all record the full vaccine product (dm+d code) for an immunisation.
GP clinical systems often record the type of vaccine administered as opposed to the vaccine product.
This may be as a procedure code or a local code which can be mapped to a procedure code.
GP Connect, therefore, uses the vaccination procedure code to denote the vaccine being administered.
The vaccination procedure code is a mandatory element.
The vaccine product code will often be a `nullFlavor` code, but the actual vaccine product **MUST** be included if it is available.

## Vaccinations that were not given

GP clinical systems may capture details of circumstances where an immunisation has not been given but there was an intention to.
Planned immunisations may not be given for a variety of reasons, such as:

* an explicit refusal for a specific vaccine or for any form of immunisation
* lack of consent for a vaccine to be administered
* the vaccine is temporarily declined
* a contraindication with another medication
* the patient does not attend an appointment or does not attend an open clinic (for example, seasonal flu vaccination clinic)
* the patient is unwell or does not meet criteria for the vaccination

This version of the specification supports inclusion of intended vaccinations which were not given for the reasons of: declined; contra-indicated; unfit or did not attend.
Consumers should be aware that the presence of a vaccination not given record is only in relation to an intended vaccination event on a given day, that is it is not stating the vaccination has definitely not been given (especially in the case of 'did not attend').

### Populating elements for an immunisation not given

Specific rules are applied to the population of some of the elements where the record is for an intended immunisation which was not given.
A few of these are highlighted here.

The provider **MUST** populate elements as described below when sending details of immunisations not given within the immunisation resource.

* <code>extension[vaccinationProcedure]</code> **MUST** be the vaccination procedure which was intended but did not happen
* <code>notGiven</code> **MUST** be <code>true</code>
* <code>explanation.reasonNotGiven</code> **SHOULD** be included with the appropriate code for the reason the vaccination did not happen

See [immunization](accessrecord_structured_development_immunization.html) for full details of the elements.

### Consumer handling of notGiven modifier

Consumer systems are to determine whether to present the details of immunisations not given as received or to transform the information in some manner.
Consumer systems not wishing to or not able to support the context modifier <code>notGiven</code> is <code>true</code> against the "given" procedure code **MAY** make use of the following codes.

* 61541000000104 | First diphtheria, tetanus and acellular pertussis, inactivated polio, Haemophilus influenzae type b and hepatitis B vaccination not done
* 61551000000101 | Second diphtheria, tetanus and acellular pertussis, inactivated polio, Haemophilus influenzae type b and hepatitis B vaccination not done
* 61561000000103 | Third diphtheria, tetanus and acellular pertussis, inactivated polio, Haemophilus influenzae type b and hepatitis B vaccination not done
* 61591000000109 | Booster diphtheria, tetanus, acellular pertussis and inactivated polio vaccination not done
* 61611000000101 | Low dose diphtheria, tetanus and inactivated polio vaccination not done
* 61621000000107 | First rotavirus vaccination not done
* 61631000000109 | Second rotavirus vaccination not done
* 61641000000100 | First meningitis B vaccination not done
* 61651000000102 | Second meningitis B vaccination not done
* 61671000000106 | Booster meningitis B vaccination not done
* 61721000000101 | First pneumococcal conjugated vaccination not done
* 61731000000104 | Second pneumococcal conjugated vaccination not done
* 61741000000108 | Third pneumococcal conjugated vaccination not done
* 61751000000106 | First measles, mumps and rubella vaccination not done
* 61761000000109 | Second measles, mumps and rubella vaccination not done
* 61811000000102 | Haemophilus influenzae type B and meningitis C vaccination not done
* 62141000000103 | Meningitis ACW and Y vaccination not done
* 62181000000106 | First human papillomavirus vaccination not done
* 62191000000108 | Second human papillomavirus vaccination not done
* 62201000000105 | First varicella vaccination not done
* 62211000000107 | Second varicella vaccination not done
* 62221000000101 | BCG (Bacillus Calmette-Guerin) vaccination not done
* 63281000000106 | First intranasal seasonal influenza vaccination not done
* 82671000000102 | First hepatitis B junior vaccination not done
* 82681000000100 | Second hepatitis B junior vaccination not done
* 82701000000103 | Third hepatitis B junior vaccination not done

These codes are part of the refset <code>63041000000107 | Routine childhood immunisation schedule procedure not done simple reference set (foundation metadata concept)</code> which may be expanded to include codes for other vaccinations as required.

The consumer **MAY** additionally need to handle <code>explanation.reasonNotGiven</code> alongside the "not done" code to provide the classified reason the vaccination was not given.

### Categorised and uncategorised records

GP provider systems have different means to record immunisations not given.
Depending on the reason the immunisation was not given, it may be recorded in way a which categorises the coded entry with immunisations or it may be recorded [uncategorised](accessrecord_structured_development_uncategorisedData_guidance.html).
GP provider systems **MUST** populate the appropriate resource according to whether the record is categorised as an immunisation or not.
GP systems may not record all instances of not giving intended vaccinations in a structured or coded format due to unavailability of suitable codes or local practice.

Consumer systems may need to request multiple resources if full details of immunisations not given are required.

### Consent for vaccination

The immunisation resource includes refusal of vaccination but does not include the consent for immunisation.
If a consumer system needs to find records of consent, perhaps to check whether a refusal has been reversed, then additional profiles will need to be requested.

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
For example, the vaccine manufacturer is recorded in a free text field so it is not suited as a reference to an `Organization` resource for the <code>manufacturer</code> element and is therefore populated to the <code>note</code> element as 'Manufacturer: Acme Pharmaceuticals'.
This might also apply to the <code>doseQuantity</code> element if the GP system holds the dosage information in a format which does not comply with the <code>Quantity</code> datatype structure.

## Using the `List` resource for immunisation queries

The results of a query for immunisation details **MUST** return a `List` containing references to all `Immunization` resources that are returned.

The `List` **MUST** be populated in line with the guidance on `List` resources.

If the `List` is empty, then an empty `List` **MUST** be returned with an `emptyReason.code` with the value `no-content-recorded`. In this case, `List.note` **MUST** be populated with the text 'Information not available'.
