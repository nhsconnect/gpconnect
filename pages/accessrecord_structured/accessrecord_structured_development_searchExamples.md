---
title: Search examples
keywords: getcarerecord, structured
tags: [getcarerecord, structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_searchExamples.html
summary: "Introduction to search criteria in GP Connect"
---

## Search examples ##

We have developed a number of example searches that demonstrate the different ways a consumer may request data in GP Connect. These have been created in conjunction with our clinical team to demonstrate the possible ways of requesting similar data that we anticipate consumers are likely to require.

The different approaches to requests that will return similar information have been chosen here to demonstrate the filter constraints that we have imposed to mitigate the risk described here in the [Search criteria](accessrecord_structured_development_search.html#clinicalrisk) page.

### 1. Request allergies and medications from the last year

```json
{
  "resourceType": "Parameters",
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeMedication",
      "part": [
        {
          "name": "medicationSearchFromDate",
          "valueDate": "2019-02-21"
        }
      ]
    }
  ]
}
```

### 2. Request medications for the last year, allergies and problems
**a) If done in one query then all medications would be returned, no date filter could be applied:**
```json
{
  "resourceType": "Parameters",
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeMedication"
    }
  ]
},
{
  "name": "includeProblems"
}
```

**b) If done in two separate queries, the first would return allergies and problems and the second would return medications for the last year:**

```json
{
  "resourceType": "Parameters",
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeProblems"
    }
  ]
}
```
**AND**

```json
{
  "resourceType": "Parameters",
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
          "name": "medicationSearchFromDate",
          "valueDate": "2019-02-21"
        }
      ]
    }
  ]
}
```

### 3. Request a patient's last three consultations

```json
{
  "resourceType": "Parameters",
  "parameter": [
    {
      "name": "patientNHSNumber",
      "valueIdentifier": {
        "system": "https://fhir.nhs.uk/Id/nhs-number",
        "value": "9999999999"
      }
    },
    {
      "name": "includeConsultations",
      "part": [
        {
          "name": "includeNumberOfMostRecent",
          "valueInteger": 3
        }
      ]
    }
  ]
}
```

### 4. Request a patient's last three consultations with problems, medications and allergies
**a) If done in one query then all medications would be returned, no date filter could be applied:**

```json
{
"resourceType": "Parameters",
"parameter": [
	{
		"name": "patientNHSNumber",
		"valueIdentifier": {
			"system": "https://fhir.nhs.uk/Id/nhs-number",
			"value": "9999999999"
		}
	},
	{
		"name": "includeConsultations",
		"part": [
			{
				"name": "includeNumberOfMostRecent",
				"valueInteger": 3
			}
		]
	},
	{
		"name": "includeProblems"
	},
	{
		"name": "includeAllergies",
		"part": [
			{
				"name": "includeResolvedAllergies",
				"valueBoolean": true
			}
		]
	},
	{
		"name": "includeMedication"
	}
]
}
```

**b) If done in two separate queries, the first would retrieve the last three consultations and problems and the second would retrieve allergies and medications for the last year:**

```json
{
  "resourceType": "Parameters",
  "parameter": [
    {
      "name": "patientNHSNumber",
      "valueIdentifier": {
        "system": "https://fhir.nhs.uk/Id/nhs-number",
        "value": "9999999999"
      }
    },
    {
      "name": "includeConsultations",
      "part": [
        {
          "name": "includeNumberOfMostRecent",
          "valueInteger": 3
        }
      ]
    },
    {
      "name": "includeProblems"
    }
  ]
}
```
**AND**

```json
{
  "resourceType": "Parameters",
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeMedication",
      "part": [
        {
          "name": "medicationSearchFromDate",
          "valueDate": "2019-12-21"
        }
      ]
    }
  ]
}
```

### 5. Request child health information, medication, allergies, immunisations, problems and observations
**a) If done in one query this would retrieve all medications and observations, no date filter could be applied:**

```json
{
  "resourceType": "Parameters",
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeMedication"
    },
    {
      "name": "includeProblems"
    },
    {
      "name": "includeImmunisations"
    },
    {
      "name": "includeUncategorisedData"
    }
  ]
}
```

**b) If done in two queries this would get last year of medications, all allergies, problems, immunisations and observations:**

```json
{
  "resourceType": "Parameters",
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
          "name": "medicationSearchFromDate",
          "valueDate": "2019-12-21"
        }
      ]
    }
  ]
}
```
**AND**

```json
{
  "resourceType": "Parameters",
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeProblems"
    },
    {
      "name": "includeImmunisations"
    },
    {
      "name": "includeUncategorisedData"
    }
  ]
}
```

**c) Another option would be two queries where the first retrieves the last year of medications and observations and the second retrieves all allergies, problems and immunisations:**

```json

{
  "resourceType": "Parameters",
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
          "name": "medicationSearchFromDate",
          "valueDate": "2019-12-21"
        }
      ]
    },
		{
      "name": "includeUncategorisedData",
      "part": [
        {
          "name": "uncategorisedDataSearchPeriod",
          "valuePeriod": {
            "start": "2019-12-21",
            "end": "2020-02-21"
          }
        }
      ]
    }
  ]
}
```
**AND**

```json
{
  "resourceType": "Parameters",
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeProblems"
    },
    {
      "name": "includeImmunisations"
    }
  ]
}
```

### 6. Request all information that has been recorded for the patient in the last three months
**a) If done in one query this would return everything, no date filter could be applied on medications or observations:**
```json
{
  "resourceType": "Parameters",
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
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeMedication"
    },
    {
      "name": "includeConsultations",
      "part": [
        {
          "name": "consultationSearchPeriod",
          "valuePeriod": {
            "start": "2019-12-21",
            "end": "2020-02-21"
          }
        }
      ]
    },
    {
      "name": "includeProblems"
    },
    {
      "name": "includeImmunisations"
    },
    {
      "name": "includeUncategorisedData"
    }
  ]
}
```

**b) If done in two queries this would be a query for the last three months for observations and medications and a second query for the last three months' consultations and all allergies, problems and immunisations:**
```json
{
  "resourceType": "Parameters",
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
          "name": "medicationSearchFromDate",
          "valueDate": "2019-12-21"
        }
      ]
    },
    {
      "name": "includeUncategorisedData",
      "part": [
        {
          "name": "uncategorisedDataSearchPeriod",
          "valuePeriod": {
            "start": "2019-12-21",
            "end": "2020-02-21"
          }
        }
      ]
    }
  ]
}
```

**AND**
```json
{
  "resourceType": "Parameters",
  "parameter": [
    {
      "name": "patientNHSNumber",
      "valueIdentifier": {
        "system": "https://fhir.nhs.uk/Id/nhs-number",
        "value": "9999999999"
      }
    },
		{
      "name": "includeConsultations",
      "part": [
        {
          "name": "consultationSearchPeriod",
          "valuePeriod": {
            "start": "2019-12-21",
            "end": "2020-02-21"
          }
        }
      ]
    },
    {
      "name": "includeAllergies",
      "part": [
        {
          "name": "includeResolvedAllergies",
          "valueBoolean": true
        }
      ]
    },
    {
      "name": "includeProblems"
    },
    {
      "name": "includeImmunisations"
    }
  ]
}
```
