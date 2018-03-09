---
title: FHIR&reg; example 3
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_3.html
summary: "Acess Record Structured FHIR examples"
---

## Example request ##

Example of request to `$getstructuredrecord` operation with `includeAllergies` set, and `includeEndedAllergies` set to false.

```json
{
  "meta": {
    "profile": {
      "value": "https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1"
    }
  },
  "parameter": [
    {
      "name": "patientNHSNumber",
      "valueIdentifier": {
        "system": "https://fhir.nhs.uk/Id/nhs-number",
        "value": "9999999999"
      }
    },
    {
      "name": "includeAllergies",
      "part": [
        {
          "name": "includeEndedAllergies",
          "valueBoolean": false
        }
      ]
    }
  ]
}
```


## Example response ##

Example of response to `$getstructuredrecord` operation with `includeAllergies` set, and `includeEndedAllergies` set to false.

Assumes - 'No Known Allergies' has been positively asserted on record and is not contradicted by presence of active allergies on record.

```json
{
  "resourceType": "Bundle",
  "id": "79183513-1382-4cdd-9470-7dbad15ea7b0",
  "meta": {
    "lastUpdated": "2018-03-01T10:57:34+00:00"
  },
  "type": "searchset",
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
        "emptyReason": {
          "coding": [
            {
              "system": "http://hl7.org/fhir/special-values",
              "code": "nil-known",
              "display": "Nil Known"
            }
          ],
          "text": "No Known Allergies"
        },
        "title": "Active Allergies",
        "patient": {
          "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
        }
      }
    },
    {
      "resourceType": "Patient",
      "id": "04603d77-1a4e-4d63-b246-d7504f8bd833",
      "meta": {
        "lastUpdated": "2018-03-09T07:52:45.466+00:00",
        "profile": [
          "https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"
        ]
      },
      "identifier": [
        {
          "system": "https://fhir.nhs.uk/Id/nhs-number",
          "value": "9999999999"
        },
        {
          "system": "https://fhir.nhs.uk/Id/PPMIdentifier",
          "value": "1234567890"
        }
      ],
      "active": true,
      "name": [
        {
          "use": "official",
          "family": "Munoz",
          "given": [
            "Vicky"
          ],
          "prefix": [
            "Mrs"
          ]
        }
      ],
      "gender": "female",
      "birthDate": "1935-09-20",
      "generalPractitioner": [
        {
          "reference": "Practitioner/G8133438",
          "display": "Dr J Bhatia"
        }
      ]
    },
    {
      "resource": {
        "resourceType": "Practitioner",
        "meta": {
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1"
          ]
        },
        "identifier": [
          {
            "system": "https://fhir.nhs.uk/Id/sds-user-id",
            "value": "G8133438"
          }
        ],
        "name": [
          {
            "family": "Bhatia",
            "prefix": [
              "Dr"
            ],
            "given": [
              "John"
            ]
          }
        ],
        "active": true,
        "id": "e0244de8-07ef-4274-9f7a-d7067bcc8d21"
      }
    },
    {
      "resourceType": "Organization",
      "id": "1",
      "meta": {
        "profile": [
          "https://fhir.hl7.org.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"
        ]
      },
      "identifier": [
        {
          "system": "https://fhir.nhs.uk/Id/ods-organization-code",
          "value": "C81010"
        }
      ],
      "active": true,
      "type": [
        {
          "coding": [
            {
              "system": "http://snomed.info/sct",
              "code": "394745000",
              "display": "General practice (organisation) (qualifier value)"
            }
          ]
        }
      ],
      "name": "The Moir Medical Centre",
      "telecom": [
        {
          "system": "phone",
          "value": "0115 9737320",
          "use": "work"
        }
      ],
      "address": [
        {
          "use": "work",
          "type": "both",
          "line": [
            "The Moir Medical Centre",
            "Regent Street, Long Eaton",
            "Nottingham"
          ],
          "city": "Nottingham",
          "district": "Derbyshire",
          "postalCode": "NG10 1QQ"
        }
      ],
      "partOf": {
        "reference": "Organization/3",
        "display": "Nhs Erewash Ccg"
      }
    }
  ]
}
```
