---
title: FHIR&reg; Medication example 4
keywords: structured design
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_fhir_examples_4.html
summary: "Access Record Structured FHIR examples"
---

## Overview ##

Example of a call to return the following items from a patient's structured record:

- Medication
- Prescription Issues

## Request payload ##

Note: The `includePrescriptionIssues` parameter has explicitly been set to `true`.

```json
{
  "resourceType": "Parameters",
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
      "name": "includeMedication",
      "part": [
        {
          "name": "includePrescriptionIssues",
          "valueBoolean": true
        }
      ]
    }
  ]
}
```

## Response payload ##



```json
{
   "resourceType": "Bundle",
   "id": "79183513-1382-4cdd-9470-7dbad15ea7b0",
   "type": "collection",
   "meta": {
      "profile": [
         "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1"
      ],
      "lastUpdated": "2018-03-01T10:57:34+00:00"
   },
   "entry": [
      {
         "resource": {
            "resourceType": "List",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-Medication-List-1"
               ]
            },
            "status": "current",
            "mode": "snapshot",
            "title": "Medication List",
            "code": {
               "coding": [
                  {
                     "code": "TBD",
                     "display": "Medication List",
                     "system": "http://snomed.info/sct"
                  }
               ]
            },
            "subject": {
               "identifier": {
                  "value": "1234567890",
                  "system": "https://fhir.nhs.uk/Id/nhs-number"
               }
            },
            "date": "2018-03-01T10:57:34+00:00",
            "orderedBy": {
               "coding": [
                  {
                     "code": "event-date",
                     "system": "http://hl7.org/fhir/list-order"
                  }
               ]
            },
            "entry": [
               {
                  "item": {
                     "reference": "MedicationStatement/6bff710a-0bdc-4c9b-b98b-40db0a107edc"
                  }
               },
               {
                  "item": {
                     "reference": "MedicationStatement/791ceb40-db0a-491d-ab0f-22f5a08509fd"
                  }
               }
            ]
         }
      },
		{
         "resource": {
            "resourceType": "MedicationStatement",
            "id": "6bff710a-0bdc-4c9b-b98b-40db0a107edc",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1"
               ]
            },
            "extension": [
               {
                  "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationStatementLastIssueDate-1",
                  "valueDateTime": "2016-05-10"
               }
            ],
            "basedOn": {
               "reference": "MedicationRequest/7e68abae-a50a-4dd2-8445-7a2aa9936bee"
            },
            "status": "completed",
            "medicationReference": {
               "reference": "Medication/c260b451-9821-42de-81f9-ba86dcea2c32"
            },
            "effectiveDateTime": "2016-05-10",
            "dateAsserted": "2016-05-10",
            "subject": {
               "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
            },
            "taken": "unk",
            "note": [
               {
                  "text": "TO DO NOTES"
               }
            ],
            "dosage": [
               {
                  "patientInstruction": "INSTRUCTIONS FOR PATIENT",
                  "text": "TAKE ONE DAILY"
               }
            ]
         }
      },
      {         
         "resource": {
		 "resourceType": "Medication",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1"
               ]
            },
            "id": "c260b451-9821-42de-81f9-ba86dcea2c32",
            "code": {
               "coding": [
                  {
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
                     ],
                     "display": "Product containing amoxicillin 250 mg/1 each oral capsule (clinical drug)",
                     "code": "323509004",
                     "system": "http://snomed.info/sct"
                  }
               ]
            }
         }
      },
      {
         "resource": {
            "resourceType": "MedicationRequest",
            "id": "7e68abae-a50a-4dd2-8445-7a2aa9936bee",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"
               ]
            },
            "status": "completed",
            "intent": "plan",
            "medicationReference": {
               "reference": "Medication/c260b451-9821-42de-81f9-ba86dcea2c32"
            },
            "subject": {
               "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
            },
            "authoredOn": "2016-05-10",
            "recorder": {
               "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
            },
            "note": [
               {
                  "text": "NOTES FOR PHARMACY"
               }
            ],
            "dosageInstruction": [
               {
                  "patientInstruction": "INSTRUCTIONS FOR PATIENT",
                  "text": "TAKE ONE DAILY"
               }
            ],
            "dispenseRequest": {
               "expectedSupplyDuration": {
                  "code": [
                     "d"
                  ],
                  "value": "28",
                  "unit": "day",
                  "system": "http://unitsofmeasure.org"
               },
               "quantity": {
                  "extension": [
                     {
                        "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1",
                        "valueString": "capsule(s)"
                     }
                  ],
                  "value": 28
               },
               "validityPeriod": {
                  "start": "2016-05-10"
               }
            },
            "extension": [
               {
                  "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1",
                  "valueCodeableConcept": {
                     "coding": [
                        {
                           "code": "acute",
                           "display": "Acute",
                           "system": "https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"
                        }
                     ]
                  }
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "MedicationRequest",
            "id": "ca89c863-1569-4e0f-ae8c-31bf98367555",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"
               ]
            },
            "basedOn": {
               "reference": "MedicationRequest/7e68abae-a50a-4dd2-8445-7a2aa9936bee"
            },
            "status": "completed",
            "intent": "order",
            "medicationReference": {
               "reference": "Medication/c260b451-9821-42de-81f9-ba86dcea2c32"
            },
            "subject": {
               "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
            },
            "authoredOn": "2016-05-10",
            "recorder": {
               "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
            },
            "note": [
               {
                  "text": "NOTES FOR PHARMACY"
               }
            ],
            "dosageInstruction": [
               {
                  "patientInstruction": "INSTRUCTIONS FOR PATIENT",
                  "text": "TAKE ONE DAILY"
               }
            ],
            "dispenseRequest": {
               "expectedSupplyDuration": {
                  "code": [
                     "d"
                  ],
                  "value": "28",
                  "unit": "day",
                  "system": "http://unitsofmeasure.org"
               },
               "quantity": {
                  "extension": [
                     {
                        "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1",
                        "valueString": "capsule(s)"
                     }
                  ],
                  "value": 28
               },
               "validityPeriod": {
                  "start": "2016-05-10"
               }
            },
            "extension": [
               {
                  "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1",
                  "valueCodeableConcept": {
                     "coding": [
                        {
                           "code": "acute",
                           "display": "Acute",
                           "system": "https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"
                        }
                     ]
                  }
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "MedicationStatement",
            "id": "791ceb40-db0a-491d-ab0f-22f5a08509fd",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationStatement-1"
               ]
            },
            "extension": [
               {
                  "url": "https://fhir.hl7.org.uk/STU3/StructureDefinition/Extension-CareConnect-MedicationStatementLastIssueDate-1",
                  "valueDateTime": "2016-09-11"
               }
            ],
            "basedOn": {
               "reference": "MedicationRequest/8e078d04-8312-433a-b6b4-46bf52542b0c"
            },
            "status": "active",
            "medicationReference": {
               "reference": "Medication/8b339981-e9be-4e37-bf03-799295a6aec8"
            },
            "effectivePeriod": {
               "start": "2016-08-11"
            },
            "dateAsserted": "2016-08-11",
            "subject": {
               "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
            },
            "taken": "unk",
            "note": [
               {
                  "text": "SOME NOTES"
               }
            ],
            "dosage": [
               {
                  "patientInstruction": "INSTRUCTIONS FOR PATIENT",
                  "text": "TAKE ONE DAILY"
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "Medication",
            "id": "8b339981-e9be-4e37-bf03-799295a6aec8",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Medication-1"
               ]
            },
            "code": {
               "coding": [
                  {
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
                     ],
                     "display": "Aspirin 75mg dispersible tablet (product)",
                     "code": "319773006",
                     "system": "http://snomed.info/sct"
                  }
               ]
            }
         }
      },
      {
         "resource": {
            "resourceType": "MedicationRequest",
            "id": "8e078d04-8312-433a-b6b4-46bf52542b0c",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"
               ]
            },
            "groupIdentifier": {
               "value": "urn:uuid:eba24af1-5b74-4790-aa5a-2134fd27ad75"
            },
            "status": "active",
            "intent": "plan",
            "medicationReference": {
               "reference": "Medication/8b339981-e9be-4e37-bf03-799295a6aec8"
            },
            "subject": {
               "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
            },
            "authoredOn": "2016-08-11",
            "recorder": {
               "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
            },
            "note": [
               {
                  "text": "NOTES FOR PHARMACY"
               }
            ],
            "dosageInstruction": [
               {
                  "patientInstruction": "INSTRUCTIONS FOR PATIENT",
                  "text": "TAKE ONE 3 TIMES/DAY"
               }
            ],
            "dispenseRequest": {
               "expectedSupplyDuration": {
                  "code": [
                     "d"
                  ],
                  "value": "28",
                  "unit": "day",
                  "system": "http://unitsofmeasure.org"
               },
               "quantity": {
                  "extension": [
                     {
                        "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1",
                        "valueString": "tablets(s)"
                     }
                  ],
                  "value": 84
               },
               "validityPeriod": {
                  "start": "2016-08-11"
               }
            },
            "extension": [
               {
                  "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationRepeatInformation-1",
                  "extension": [
                     {
                        "url": "numberOfRepeatPrescriptionsAllowed",
                        "valuePositiveInt": 5
                     },
                     {
                        "url": "numberOfRepeatPrescriptionsIssued",
                        "valuePositiveInt": 2
                     }
                  ]
               },
               {
                  "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1",
                  "valueCodeableConcept": {
                     "coding": [
                        {
                           "code": "repeat",
                           "display": "Repeat",
                           "system": "https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"
                        }
                     ]
                  }
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "MedicationRequest",
            "id": "8afe3af9-995d-4ccc-9211-f8c2620be670",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"
               ]
            },
            "basedOn": {
               "reference": "MedicationRequest/8e078d04-8312-433a-b6b4-46bf52542b0c"
            },
            "groupIdentifier": {
               "value": "urn:uuid:eba24af1-5b74-4790-aa5a-2134fd27ad75"
            },
            "status": "completed",
            "intent": "order",
            "medicationReference": {
               "reference": "Medication/8b339981-e9be-4e37-bf03-799295a6aec8"
            },
            "subject": {
               "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
            },
            "authoredOn": "2016-08-11",
            "recorder": {
               "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
            },
            "note": [
               {
                  "text": "NOTES FOR PHARMACY"
               }
            ],
            "dosageInstruction": [
               {
                  "patientInstruction": "INSTRUCTIONS FOR PATIENT",
                  "text": "TAKE ONE 3 TIMES/DAY"
               }
            ],
            "dispenseRequest": {
               "expectedSupplyDuration": {
                  "code": [
                     "d"
                  ],
                  "value": "28",
                  "unit": "day",
                  "system": "http://unitsofmeasure.org"
               },
               "quantity": {
                  "extension": [
                     {
                        "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1",
                        "valueString": "tablet(s)"
                     }
                  ],
                  "value": 84
               },
               "validityPeriod": {
                  "start": "2016-08-11"
               }
            },
            "extension": [
               {
                  "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1",
                  "valueCodeableConcept": {
                     "coding": [
                        {
                           "code": "repeat",
                           "display": "Repeat",
                           "system": "https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"
                        }
                     ]
                  }
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "MedicationRequest",
            "id": "a946012a-283b-46c4-8312-e1312a54ab9c",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-MedicationRequest-1"
               ]
            },
            "basedOn": {
               "reference": "MedicationRequest/8e078d04-8312-433a-b6b4-46bf52542b0c"
            },
            "groupIdentifier": {
               "value": "urn:uuid:eba24af1-5b74-4790-aa5a-2134fd27ad75"
            },
            "status": "completed",
            "intent": "order",
			"medicationReference": {
               "reference": "Medication/8b339981-e9be-4e37-bf03-799295a6aec8"
            },
            "subject": {
               "reference": "Patient/04603d77-1a4e-4d63-b246-d7504f8bd833"
            },
            "authoredOn": "2016-09-11",
            "recorder": {
               "reference": "Practitioner/e0244de8-07ef-4274-9f7a-d7067bcc8d21"
            },
            "note": [
               {
                  "text": "NOTES FOR PHARMACY"
               }
            ],
            "dosageInstruction": [
               {
                  "patientInstruction": "INSTRUCTIONS FOR PATIENT",
                  "text": "TAKE ONE 3 TIMES/DAY"
               }
            ],
            "dispenseRequest": {
               "expectedSupplyDuration": {
                  "code": [
                     "d"
                  ],
                  "value": "28",
                  "unit": "day",
                  "system": "http://unitsofmeasure.org"
               },
               "quantity": {
                  "extension": [
                     {
                        "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-MedicationQuantityText-1",
                        "valueString": "tablet(s)"
                     }
                  ],
                  "value": 84
               },
               "validityPeriod": {
                  "start": "2016-09-11"
               }
            },
            "extension": [
               {
                  "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-PrescriptionType-1",
                  "valueCodeableConcept": {
                     "coding": [
                        {
                           "code": "repeat",
                           "display": "Repeat",
                           "system": "https://fhir.nhs.uk/STU3/CodeSystem/CareConnect-PrescriptionType-1"
                        }
                     ]
                  }
               }
            ]
         }
      },
      {
         "resource": {
            "resourceType": "Patient",
            "id": "04603d77-1a4e-4d63-b246-d7504f8bd833",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Patient-1"
               ],
               "lastUpdated": "2018-03-09T07:52:45.466+00:00"
            },
            "gender": "female",
            "generalPractitioner": [
               {
                  "reference": "Practitioner/G8133438",
                  "display": "Dr J Bhatia"
               }
            ],
            "name": [
               {
                  "use": "official",
                  "prefix": [
                     "Mrs"
                  ],
                  "family": "Munoz",
                  "given": [
                     "Vicky"
                  ]
               }
            ],
            "active": true,
            "birthDate": "1935-09-20",
            "identifier": [
               {
                  "system": "https://fhir.nhs.uk/Id/nhs-number",
                  "extension": [
                     {
                        "url": "https://fhir.nhs.uk/STU3/StructureDefinition/Extension-CareConnect-GPC-NHSNumberVerificationStatus-1",
                        "valueCodeableConcept": {
                           "coding": [
                              {
                                 "code": "K3XZhBz91kCLWKuTUnEArg=='"
                              }
                           ]
                        }
                     }
                  ],
                  "value": "99999999"
               }
            ]
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
         "resource": {
            "resourceType": "Organization",
            "id": "1",
            "meta": {
               "profile": [
                  "https://fhir.nhs.uk/STU3/StructureDefinition/CareConnect-GPC-Organization-1"
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
            ]
         }
      }
   ]
}
```
