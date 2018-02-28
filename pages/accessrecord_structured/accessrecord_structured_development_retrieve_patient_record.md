---
title: Retrieve a patients structured record
keywords: getstructuredrecord, view
tags: [use_case,getstructuredrecord]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_retrieve_patient_record.html
summary: "Retrieve a patients structured record at a GP practice"
---

## Use case ##

Retrieve a patients record in FHIR structured format from a GP practice. Test

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization.
- GP Connect utilises a JSON Web Tokens (JWT) to transmit clinical audit & provenance details. 

## Prerequisites ##

### Consumer ###

The Consumer system:

- **SHALL** have previously resolved the organisation's FHIR endpoint base URL through the [Spine Directory Service](https://nhsconnect.github.io/gpconnect/integration_spine_directory_service.html)
- **SHALL** have previously traced the patient's NHS number using the [Personal Demographics Service](https://nhsconnect.github.io/gpconnect/integration_personal_demographic_service.html) or an equivalent service.

## API Usage ##

### Request operation ###

#### FHIR relative request ####

```http
POST /Patient/$gpc.getstructuredrecord-1
```

#### FHIR absolute request ####

```http
POST https://[proxy_server]/https://[provider_server]/[fhir_base]/Patient/$gpc.getstructuredrecord-1
```

#### Request headers ####

Consumers **SHALL** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's TraceID (i.e. GUID/UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.getstructuredrecord-1`|

Example HTTP request headers:

```http
POST http://gpconnect.fhir.nhs.net/fhir/Patient/$gpc.getstructuredrecord-1 HTTP/1.1
User-Agent: .NET FhirClient for FHIR 1.2.0
Accept: application/json+fhir;charset=utf-8
Prefer: return=representation
Host: michaelm-pc
Content-Type: application/json+fhir;charset=utf-8
Content-Length: 289
Expect: 100-continue
Connection: Keep-Alive
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:operation:gpc.getstructuredrecord-1
```

#### Payload request body ####

The following data-elements are mandatory (i.e. data **MUST** be present):

- the `patientNHSNumber` is the NHS number of the patient who's GP record you want to access.
- the `includeResourceGroup` are the resource groups you wish to return.

The following data-elements are optional:

- the `timePeriod` defines the period of data you wish to return.
	-  not providing `timePeriod` returns all data (including dates in future).
- the `start` and `end` values specify the exact period to be returned.
	- providing both `start` and `end` returns data within the values provided.
	- providing `start` only returns all data after that value (including dates in future).
	- providing `end` only returns all data before that value.
- the `includeIssues` value idenifies if all medication issues should be returned.

The request payload is a set of [Parameters](https://www.hl7.org/fhir/parameters.html) conforming to the `gpconnect-structuredrecord-operation-1` profiled `OperationDefinition`, see below:

{% include tip.html content="This is a type level operation (i.e. is not associated with a given resource instance)." %} 

```xml
<Parameters xmlns="http://hl7.org/fhir">
	<id value="b28bbed9-55b1-46ea-b019-b984a156decc"/>
	<meta>
		<profile value="https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-AccessStructuredRecord-1"/>
	</meta>	
	<parameter>
		<name value="patientNHSnumber"/>
		<valueIdentifier id="4569871235"/>
	</parameter>
	<parameter>
		<name value="includeResourceGroup:Medication"/>
			<part>
				<name value="timePeriod"/>
				<valuePeriod>
					<start value="2017-01-01"/>
					<end value="2018-02-01"/>
				</valuePeriod>
			</part>
			<part>
				<name value="includeIssues"/>
				<valueBoolean value="true"/>
			</part>
	</parameter>
	<parameter>
		<name value="includeResourceGroup:AllergyIntolerance"/>
			<part>
				<name value="includeEndedAllergies"/>
				<valueBoolean value="true"/>
			</part>
	</parameter>
</Parameters>
```

{% include tip.html content="Consumer guidance: it is advised that a single call is made to retrieve all structured data required. The parameter filters should be appiied to reduce the payload." %} 

{% include important.html content="Provider systems **SHALL** only expose `Patient` resources for patient's who have a valid PDS trace status." %}

On the wire a JSON serialised `$gpc.getstructuredrecord-1` request would look something like the following:

```json
{
  "id": {
    "value": "b28bbed9-55b1-46ea-b019-b984a156decc"
  },
  "meta": {
    "profile": {
      "value": "https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-AccessStructuredRecord-1"
    }
  },
  "parameter": [
    {
      "name": {
        "value": "patientNHSnumber"
      },
      "valueIdentifier": {
        "id": "4569871235"
      }
    },
    {
      "name": {
        "value": "includeResourceGroup:Medication"
      },
      "part": [
        {
          "name": {
            "value": "timePeriod"
          },
          "valuePeriod": {
            "start": {
              "value": "2017-01-01"
            },
            "end": {
              "value": "2018-02-01"
            }
          }
        },
        {
          "name": {
            "value": "includeIssues"
          },
          "valueBoolean": {
            "value": "true"
          }
        }
      ]
    },
    {
      "name": {
        "value": "includeResourceGroup:AllergyIntolerance"
      }
    }
  ]
}
```

The Provider system **SHALL**:

- return all data if no `timePeriod` parameter is specified for a section that can accept a time period.

#### Parameter Details ####

| Name                  | Type 		| Format 		| Comments |
|-----------------------|-----------|---------------|--------|
| `patientNHSnumber.id` | `integer` | | [NHS Number input and display](http://systems.digital.nhs.uk/data/cui/uig/inputdisplay.pdf) |
| `includeResourceGroup:Medication` | `n/a` | `n/a` | Resource group for Medications |
| `timePeriod.start` | `date` | `yyyy-mm-dd` | [Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `timePeriod.end` | `date` | `yyyy-mm-dd` | [Date display](http://systems.digital.nhs.uk/data/cui/uig/datedisplay.pdf) |
| `includeIssues.valueBoolean` | `boolean` | `true` or `false` | Include associated issues in response, or not |
| `includeResourceGroup:AllergyIntolerance` | `n/a` | `n/a` | Resource group for Allergies and Intolerances |
| `includeEndedAllergies.valueBoolean` | `boolean` | `true` or `false` | Include ended allergies in response, or not |

#### Error Handling ####

The Provider system **SHALL** return an error if:

- the `patientNHSNumber` is invalid (i.e. fails NHS number format and check digit tests).
- the `patientNHSNumber` is not associated with a `NHS Number Status Indicator Code` of `Number present and verified`.
- the GP organisation is not the patient's nominated primary care provider.
- the `includeResourceGroup` is invalid (i.e. isn't from the correct value set).
- an invalid `timePeriod` is requested (i.e. end date > start date).
- a `timePeriod` is specified for a `includeResourceGroup` that is time period agnostic (e.g. Allergies).
<br>

{% include important.html content="Provider systems **SHALL** return an [OperationOutcome](https://www.hl7.org/fhir/stu3/operationoutcome.html) resource that provides additional detail when one or more data fields are corrupt or a specific business rule/constraint is breached." %}

{% include important.html content="Provider systems **SHOULD** return informative messages if an error occurs (for example, Bad Request (400) - An invalid value was specified for one of the query parameters in the request)." %}

{% include tip.html content="Refer to [Development - FHIR API Guidance - Error Handling](development_fhir_error_handling_guidance.html) for details of error codes." %}

### Request Response ###

#### Response Headers ####

```http
HTTP/1.1 200 OK
Cache-Control: no-store
Content-Type: application/json+fhir; charset=utf-8
Date: Sun, 07 Aug 2016 11:13:05 GMT
Content-Length: 1464
```

#### Payload Response Body ####

Provider systems:

- **SHALL** return a `200` **OK** HTTP status code on successful retrieval of a care record section.
- **SHALL** return the care record section as valid XHTML inline with the [FHIR Narrative](https://www.hl7.org/fhir/stu3/narrative.html) guidance.
- **SHALL** include the relevant GP Connect `StructureDefinition` profile details in the `meta` fields of the returned response.
- **SHALL** include the `Patient`, `Practitioner` and `Organization` details for the retrieved care record in a searchset `Bundle`.

```json
{
      "resource": {
         "MedicationStatement": {
            "id": {
               "value": "MedicationStatement/idDrugA"
            },
            "identifier": {
               "value": "7CC4C6C6-BAE4-11E7-9E7A-E5292B8B50A1"
            },
            "basedOn": {
               "reference": {
                  "value": "MedicationRequestPlan/idDrugA"
               }
            },
            "status": {
               "value": "completed"
            },
            "medicationCodeableConcept": {
               "coding": {
                  "element": {
                     "code": "325278007",
                     "display": "Metformin hydrochloride 500mg tablet (substance)",
                     "system": "http://snomed.info/sct"
                  }
               }
            },
            "effective": {
               "start": {
                  "value": "20180123 13:30:00.000"
               },
               "end": {
                  "value": "20180130 13:30:00.000"
               }
            },
            "dateAsserted": {
               "value": "20180123 13:30:00.000"
            },
            "informationSource": {
               "reference": {
                  "value": "Organization/0001"
               }
            },
            "subject": {
               "refernce": {
                  "value": "Patient/0001"
               }
            },
            "taken": {
               "value": "y"
            },
            "note": {
               "value": "Oral administration of treatment (procedure)"
            },
            "dosage": {
               "text": {
                  "value": "500 mg - once a day"
               }
            }
         }
      }
   },
   {
      "resource": {
         "MedicationRequest": {
            "id": {
               "value": "MedicationRequestPlan"
            },
            "identifier": {
               "value": "EPS_id"
            },
            "intent": {
               "value": "plan"
            },
            "medicationCodeableConcept": {
               "coding": {
                  "element": {
                     "code": "325278007",
                     "display": "Metformin hydrochloride 500mg tablet (substance)",
                     "system": "http://snomed.info/sct"
                  }
               }
            },
            "subject": {
               "reference": {
                  "value": "Patient/0001"
               }
            },
            "note": {
               "value": "Oral administration of treatment (procedure)"
            },
            "dispenseRequest": {
               "quantity": {
                  "value": {
                     "value": "28"
                  }
               },
               "expectedSupplyDuration": {
                  "value": {
                     "value": "7"
                  },
                  "unit": {
                     "value": "days"
                  }
               },
               "performer": {
                  "reference": {
                     "value": "PharmacyReference/0001"
                  }
               }
            },
            "ExtensionForDigitalSignature": null
         }
      }
}
```

<!--
## Examples ##

### C# ###

{% include tip.html content="C# code snippets utilise Ewout Kramer's [fhir-net-api](https://github.com/ewoutkramer/fhir-net-api) library which is the official .NET API for HL7&reg; FHIR&reg;." %}

```csharp
var client = new FhirClient("http://gpconnect.fhir.nhs.net/fhir/");
client.PreferredFormat = ResourceFormat.Json;
var parameters = new Parameters();
parameters.Add("nhsNumber", new Identifier("http://fhir.nhs.net/Id/nhs-number","P003"));
parameters.Add("recordSection", new CodeableConcept("http://fhir.nhs.net/ValueSet/gpconnect-record-section-1","ALL"));
var resource = client.TypeOperation<Patient>("gpc.getcarerecord",parameters);
FhirSerializer.SerializeResourceToJson(resource).Dump();
```

### Java ###

{% include tip.html content="Java code snippets utilise James Agnew's [hapi-fhir](https://github.com/jamesagnew/hapi-fhir/
) library." %}

```java
FhirContext ctx = FhirContext.forDstu2();
IGenericClient client = ctx.newRestfulGenericClient("http://gpconnect.fhir.nhs.net/fhir/");
client.registerInterceptor(new LoggingInterceptor(true));

// Create the input parameters to pass to the server
Parameters inParams = new Parameters();
inParams.addParameter().setName("patientNHSNumber").setValue(new Identifier().setValue("P003").setSystem("http://fhir.nhs.net/Id/nhs-number"));
inParams.addParameter().setName("recordSection").setValue(new CodeableConcept().addCoding(new Coding().setCode("ALL").setSystem("http://fhir.nhs.net/ValueSet/gpconnect-record-section-1")));

Parameters outParams = client
		.operation()
		.onType(Patient.class)
		.named("gpc.getcarerecord")
		.withParameters(inParams)
		.execute();

Bundle responseBundle = (Bundle) outParams.getParameter().get(0).getResource();
System.out.println(ctx.newXmlParser().setPrettyPrint(true).encodeResourceToString(responseBundle));
```
-->
