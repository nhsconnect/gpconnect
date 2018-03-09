---
title: FHIR&reg; example 1
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_1.html
summary: "Acess Record Structured FHIR examples"
---

## Example request ##

Example of request to `$getstructuredrecord` operation with `includeAllergies` set, and `includeEndedAllergies` set to `true`.

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
          "valueBoolean": true
        }
      ]
    }
  ]
}
```

## Example response ##

Example of response to `$getstructuredrecord` operation with `includeAllergies` set, and `includeEndedAllergies` set to true.

For the purposes of the example it is assumed that there is a single resolved allergy present.

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
        "meta": {
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Allergy-List-1"
          ]
        },
        "status": "current",
        "title": "Active Allergies",
        "code": {
          "coding": [
            {
              "display": "Active Allergies",
              "system": "http://snomed.info/sct",
              "code": "TBD"
            }
          ]
        },
        "resourceType": "List",
        "entry": [
          {
            "item": "AllergyIntolerance/561850bd-360c-4d17-b3c8-a837ef0cbfba"
          },
          {
            "item": "AllergyIntolerance/6bff710a-0bdc-4c9b-b98b-40db0a107edc"
          },
          {
            "item": "AllergyIntolerance/5eb0f76a-cecb-4b83-999d-ddb76e551a9b"
          },
          {
            "item": "AllergyIntolerance/d92b7d42-554d-4c92-b829-e76508185702"
          }
        ],
        "date": "2018-03-01T10:57:34+00:00",
        "mode": "snapshot",
        "orderedBy": {
          "coding": [
            {
              "system": "http://hl7.org/fhir/list-order",
              "code": "event-date"
            }
          ]
        },
        "subject": {
          "identifier": {
            "system": "https://fhir.nhs.uk/Id/nhs-number",
            "value": "1234567890"
          }
        }
      }
    },
    {
      "resource": {
        "contained": [
          {
            "id": "561850bd-360c-4d17-b3c8-a837ef0cbfba",
            "reaction": [
              {
                "manifestation": [
                  {
                    "coding": [
                      {
                        "display": "Vomiting (disorder)",
                        "code": "422400008",
                        "system": "http://snomed.info/sct",
                        "extension": [
                          {
                            "url": "https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid",
                            "extension": [
                              {
                                "url": "DescriptionID",
                                "valueId": "2647992016"
                              },
                              {
                                "url": "DescriptionDisplay",
                                "valueString": "Emesis"
                              }
                            ]
                          }
                        ]
                      }
                    ]
                  }
                ],
                "severity": "severe"
              }
            ],
            "verificationStatus": "unconfirmed",
            "assertedDate": "2011-05-07",
            "type": "intolerance",
            "code": {
              "coding": [
                {
                  "display": "Aspirin 75mg dispersible tablet (product)",
                  "code": "319773006",
                  "system": "http://snomed.info/sct",
                  "extension": [
                    {
                      "url": "https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid",
                      "extension": [
                        {
                          "url": "DescriptionID",
                          "valueId": "56962301000001119"
                        },
                        {
                          "url": "DescriptionDisplay",
                          "valueString": "Aspirin 75mg dispersible tablets"
                        }
                      ]
                    }
                  ]
                }
              ]
            },
            "resourceType": "AllergyIntolerance",
            "clinicalStatus": "resolved",
            "patient": {
              "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
            },
            "note": [
              {
                "text": "Allergy Type: Adverse Reaction, Certainty: Absolute, Severity: Very Severe, NOTES: Some freetext notes"
              }
            ],
            "recorder": {
              "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
            },
            "category": [
              "medication"
            ],
            "meta": {
              "profile": [
                "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"
              ]
            },
            "criticality": "low"
          }
        ],
        "meta": {
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Allergy-List-1"
          ]
        },
        "status": "current",
        "title": "Resolved Allergies",
        "code": {
          "coding": [
            {
              "display": "Resolved Allergies",
              "system": "http://snomed.info/sct",
              "code": "TBD"
            }
          ]
        },
        "resourceType": "List",
        "entry": [
          {}
        ],
        "date": "2018-03-01T10:57:34+00:00",
        "mode": "snapshot",
        "orderedBy": {
          "coding": [
            {
              "system": "http://hl7.org/fhir/list-order",
              "code": "event-date"
            }
          ]
        },
        "subject": {
          "identifier": {
            "system": "https://fhir.nhs.uk/Id/nhs-number",
            "value": "1234567890"
          }
        }
      }
    },
    {
      "resource": {
        "id": "6bff710a-0bdc-4c9b-b98b-40db0a107edc",
        "reaction": [
          {
            "manifestation": [
              {
                "coding": [
                  {
                    "display": "On examination - itchy rash (disorder)",
                    "code": "304386008",
                    "system": "http://snomed.info/sct",
                    "extension": [
                      {
                        "url": "https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid",
                        "extension": [
                          {
                            "url": "DescriptionID",
                            "valueId": "446685017"
                          },
                          {
                            "url": "DescriptionDisplay",
                            "valueString": "O/E - itchy rash"
                          }
                        ]
                      }
                    ]
                  }
                ]
              }
            ],
            "severity": "mild"
          }
        ],
        "verificationStatus": "unconfirmed",
        "assertedDate": "2012-05-07T00:00+00:00",
        "type": "allergy",
        "code": {
          "coding": [
            {
              "display": "Product containing amoxicillin 250 mg/1 each oral capsule (clinical drug)",
              "code": "323509004",
              "system": "http://snomed.info/sct",
              "extension": [
                {
                  "url": "https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid",
                  "extension": [
                    {
                      "url": "DescriptionID",
                      "valueId": "56966201000001112"
                    },
                    {
                      "url": "DescriptionDisplay",
                      "valueString": "Amoxicillin 250mg capsules"
                    }
                  ]
                }
              ]
            }
          ]
        },
        "resourceType": "AllergyIntolerance",
        "clinicalStatus": "active",
        "patient": {
          "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
        },
        "note": [
          {
            "text": "Certainty: Likely, Severity: Minimal, NOTES: Some freetext notes"
          }
        ],
        "recorder": {
          "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
        },
        "category": [
          "medication"
        ],
        "meta": {
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"
          ]
        },
        "criticality": "low"
      }
    },
    {
      "resource": {
        "id": "5eb0f76a-cecb-4b83-999d-ddb76e551a9b",
        "reaction": [
          {
            "manifestation": [
              {
                "coding": [
                  {
                    "display": "Peanut-induced anaphylaxis (disorder)",
                    "code": "241933001",
                    "system": "http://snomed.info/sct",
                    "extension": [
                      {
                        "url": "https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid",
                        "extension": [
                          {
                            "url": "DescriptionID",
                            "valueId": "362151013"
                          },
                          {
                            "url": "DescriptionDisplay",
                            "valueString": "Peanut-induced anaphylaxis"
                          }
                        ]
                      }
                    ]
                  }
                ]
              }
            ],
            "severity": "severe"
          }
        ],
        "verificationStatus": "unconfirmed",
        "assertedDate": "2016-02-08T10:57:34+00:00",
        "type": "allergy",
        "code": {
          "coding": [
            {
              "display": "Peanut - dietary (substance)",
              "code": "256349002",
              "system": "http://snomed.info/sct",
              "extension": [
                {
                  "url": "https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid",
                  "extension": [
                    {
                      "url": "DescriptionID",
                      "valueId": "381850016"
                    },
                    {
                      "url": "DescriptionDisplay",
                      "valueString": "Peanut - dietary"
                    }
                  ]
                }
              ]
            }
          ]
        },
        "resourceType": "AllergyIntolerance",
        "clinicalStatus": "active",
        "patient": {
          "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
        },
        "note": [
          {
            "text": "Certainty: Certain, Severity: Life Threatening, NOTES: notes on the peanut allergy"
          }
        ],
        "recorder": {
          "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
        },
        "category": [
          "environental"
        ],
        "meta": {
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"
          ]
        },
        "criticality": "high"
      }
    },
    {
      "resource": {
        "id": "d92b7d42-554d-4c92-b829-e76508185702",
        "verificationStatus": "unconfirmed",
        "type": "allergy",
        "code": {
          "coding": [
            {
              "display": "Transfer-degraded drug allergy (record artifact)",
              "code": "196461000000101",
              "system": "http://snomed.info/sct",
              "extension": [
                {
                  "url": "https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-coding-sctdescid",
                  "extension": [
                    {
                      "url": "DescriptionID",
                      "valueId": "294801000000114"
                    },
                    {
                      "url": "DescriptionDisplay",
                      "valueString": "Transfer-degraded drug allergy"
                    }
                  ]
                }
              ]
            }
          ]
        },
        "resourceType": "AllergyIntolerance",
        "clinicalStatus": "active",
        "patient": {
          "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
        },
        "note": [
          {
            "text": "NOTES: This was entered incorrectly on the source system as a history/journal entry and not as a drug allergy"
          }
        ],
        "assertedDate": "2016-01-08T11:57:34+00:00",
        "category": [
          "medication"
        ],
        "recorder": {
          "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
        },
        "meta": {
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-AllergyIntolerance-1"
          ]
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
