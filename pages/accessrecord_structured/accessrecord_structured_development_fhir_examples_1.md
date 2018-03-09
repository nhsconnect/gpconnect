---
title: FHIR&reg; example 1
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_1.html
summary: "Acess Record Structured FHIR examples"
---

## Note ##

- The GP Connect API is not a full FHIR RESTful interface - therefore not all resources returned are directly accessible
- The message conventions reflect this e.g. fullURLs for individual resources are not provided

## Example request ##

{% include todo.html content="TODO" %}

## Example response ##

Example of response to `/Patient/$getstructuredrecord` operation with `includeAllergies` and `includeEndedAllergies` set to true.

For the purposes of the example it is assumed that there is a single resolved allergy present.

{% include todo.html content="Add Patient and registered GP Organization resources" %}

```json
{
  "resourceType": "Bundle",
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
            "id": "res-1",
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
              "identifier": {
                "system": "https://fhir.nhs.uk/Id/nhs-number",
                "value": "1234567890"
              }
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
          "identifier": {
            "system": "https://fhir.nhs.uk/Id/nhs-number",
            "value": "1234567890"
          }
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
          "identifier": {
            "system": "https://fhir.nhs.uk/Id/nhs-number",
            "value": "1234567890"
          }
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
          "identifier": {
            "system": "https://fhir.nhs.uk/Id/nhs-number",
            "value": "1234567890"
          }
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
      "resource": {
        "resourceType": "Practitioner",
        "meta": {
          "profile": [
            "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Practitioner-1"
          ]
        },
        "name": [
          {
            "family": "Clarkson",
            "prefix": [
              "Dr"
            ],
            "given": [
              "John"
            ]
          }
        ],
        "active": true,
        "identifier": [
          {
            "system": "https://fhir.nhs.uk/Id/sds-user-id",
            "value": "G8122438"
          }
        ],
        "id": "e0244de8-07ef-4274-9f7a-d7067bcc8d21"
      }
    }
  ],
  "meta": {
    "lastUpdated": "2018-03-01T10:57:34+00:00"
  },
  "type": "searchset"
}
```
