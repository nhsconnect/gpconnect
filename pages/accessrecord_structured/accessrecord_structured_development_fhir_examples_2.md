---
title: FHIR&reg; example 2
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_2.html
summary: "Acess Record Structured FHIR examples"
---

## Note ##

- The GP Connect API is not a full FHIR RESTful interface - therefore not all resources returned are directly accessible
- The message conventions reflect this e.g. fullURLs for individual resources are not provided

## Example request ##

{% include todo.html content="TODO" %}

## Example response ##

Example of response to `/Patient/$getstructuredrecord` operation with `includeAllergies` and `includeEndedAllergies` set to false, or not provided.

Assumes - 'No Known Allergies' has not been positively asserted on record and but is not contradicted by presence of active allergies on record.

{% include todo.html content="Add Patient and registered GP Organization resources" %}

```json
{
  "resourceType": "Bundle",
  "entry": [
    {
      "resource": {
        "date": "2018-03-01T10:57:34+00:00",
        "resourceType": "List",
        "status": "current",
        "code": {
          "coding": [
            {
              "system": "http://snomed.info/sct",
              "code": "TBD",
              "display": "Active Allergies"
            }
          ]
        },
        "meta": {
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Allergy-List-1"
          ]
        },
        "mode": "snapshot",
        "note": [
          {
            "text": "There are no allergies in the patient record but it has not been confirmed with the patient that they have no allergies (i.e. 'no known allergies' code has not been recorded)."
          }
        ],
        "title": "Active Allergies",
        "subject": {
          "identifier": {
            "system": "https://fhir.nhs.uk/Id/nhs-number",
            "value": "1234567890"
          }
        }
      }
    }
  ],
  "type": "searchset",
  "meta": {
    "lastUpdated": "2018-03-01T10:57:34+00:00"
  }
}
```
