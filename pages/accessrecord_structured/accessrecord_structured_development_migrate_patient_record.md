---
title: Migrate a patient's structured record
keywords: getstructuredrecord, view
tags: [design,structured]
sidebar: accessrecord_structured_sidebar
permalink: accessrecord_structured_development_migrate_patient_record.html
summary: "Migrate a patient's record in structured format"
---

## Use case ##

Migrate a patient's record from one organisation to another in FHIR&reg; structured format.

## Security ##

- GP Connect utilises TLS Mutual Authentication for system level authorization
- GP Connect utilises JSON Web Tokens (JWT) to transmit clinical audit and provenance details

## Prerequisites ##

### Consumer ###

The consumer system:

- **MUST** have previously resolved the organisation's Access Record Structured FHIR endpoint base URL through the [Spine Directory Service](integration_spine_directory_service.html)
- **MUST** have previously traced the patient's NHS Number using the [Personal Demographics Service](integration_personal_demographic_service.html) or an equivalent service

## API usage ##

### Interaction diagram ###

<img style="height: 400px;" alt="Get structured record interaction diagram" src="images/access_structured/migrate-structured-record-interaction-diagram.png"/>

### Request operation ###

#### FHIR&reg; relative request ####

```http
POST /Patient/$gpc.migratestructuredrecord
```

#### FHIR&reg; absolute request ####

```http
POST https://[proxy_server]/https://[structured_provider_server]/[structured_fhir_base]/Patient/$gpc.migratestructuredrecord
```

#### Request headers ####

Consumers **MUST** include the following additional HTTP request headers:

| Header               | Value |
|----------------------|-------|
| `Ssp-TraceID`        | Consumer's Trace ID (a GUID or UUID) |
| `Ssp-From`           | Consumer's ASID |
| `Ssp-To`             | Provider's ASID |
| `Ssp-InteractionID`  | `urn:nhs:names:services:gpconnect:fhir:operation:gpc.migratestructuredrecord-1`|

Example HTTP request headers:

```http
Accept: application/fhir+json;charset=utf-8
Content-Type: application/fhir+json;charset=utf-8
Ssp-TraceID: 629ea9ba-a077-4d99-b289-7a9b19fd4e03
Ssp-From: 200000000115
Ssp-To: 200000000116
Ssp-InteractionID: urn:nhs:names:services:gpconnect:fhir:operation:gpc.migratestructuredrecord-1
```


#### Authorisation ####

{% include important.html content="The following may need to be moved to the Patient Switching Standard" %}

This interaction can only be used when patient's information is being migrated between GP practices. When a request to migrate the patient's record is made, the provider system **MUST** check that the consumer system is the patient's registered GP practice by checking this against PDS. The following steps will need to be performed:
- The consuming system will need to perform a PDS trace to retrieve the patient's current registered practice
- The consuming system **MUST** record the patient's current registered practice
- The consuming system updates PDS as the patient's registered practice
- The consuming system looks up the previously registered practice's endpoint on SDS
- The consuming system makes a request to migrate the patient's record
- The providing system **MUST** check that the ODS code supplied in the `requesting_organization` claim in the JWT matches the patient's registered practice on PDS

#### Availability of data ####

The record migration use case requires that information is always available regardless of whether the [structured capability has been enabled](development_api_non_functional_requirements.html#enablement), or whether clinical areas have been turned off using [configuration for clinical areas](accessrecord_structured_development_clinical_area_config.html).


#### Payload request body ####

The payload request body comprises a `Parameters` resource, conforming to the [GPConnect-MigrateStructuredRecord-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-MigrateStructuredRecord-Operation-1/_history/1.15) `OperationDefinition` profile.

The `Parameters` resource is populated with the parameters shown below.  Note: The ↳ character indicates a part parameter.

<table>
  <thead>
    <tr>
      <th>Name</th>
      <th>Type</th>
      <th>Optionality</th>
      <th>Cardinality</th>
      <th>Comments</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code class="highlighter-rouge">patientNHSNumber</code></td>
      <td><code class="highlighter-rouge">Identifier</code></td>
      <td>Mandatory</td>
      <td>1..1</td>
      <td>NHS Number of the patient for whom to retrieve the structured record.</td>
    </tr>


    <tr>
      <td><code class="highlighter-rouge">includeFullRecord</code></td>
      <td><code class="highlighter-rouge"></code></td>
      <td>Mandatory</td>
      <td>1..1</td>
      <td>Include the patient's full clinical record in the response.</td>
    </tr>
    <tr>
      <td><span style="white-space: nowrap;">&nbsp;&nbsp;&#8627; <code class="highlighter-rouge">includeSensitiveInformation</code></span></td>
      <td><code class="highlighter-rouge">Boolean</code></td>
      <td>Mandatory</td>
      <td>1..1</td>
      <td>
        Include confidential and sensitive information in the response, this parameter has a default value of 'true'. This parameter can only be set to true if an appropriate `requested_scope` value is provided in the JWT, more guidance is available in the  <a href="integration_cross_organisation_audit_and_provenance.html#requested_scope-claim">Cross-organisation audit and provenance page</a>
        <p><i>Part parameter: may only be provided if <code>includeFullRecord</code> is set.</i></p>        
      </td>
    </tr>



  </tbody>
</table>


The example below shows a fully populated `Parameters` resource as a request to the `$gpc.migratestructuredrecord` operation:

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
      "name": "includeFullRecord",
      "part": [
        {
          "name": "includeSensitiveInformation",
          "valueBoolean": true
        }
      ]
    }
  ]
}
```

#### Error handling ####

The provider system **MUST** return a [GPConnect-OperationOutcome-1](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-OperationOutcome-1/_history/1.2) resource that provides additional detail when one or more data field is corrupt or a specific business rule/constraint is breached.

The table below shows common errors that may be encountered during this API call, and the returned Spine error code.  Please see [Error handling guidance](development_fhir_error_handling_guidance.html) for additional information needed to create the error response, or to determine the response for errors encountered that are not shown below.

Errors returned due to parameter failure **MUST** include diagnostic information detailing the invalid parameter.

|-------------------------|-------------------|
| Error encountered        | Spine error code returned |
|-------------------------|-------------------|
| The `Parameters` resource passed does not conform to that specified in the [GPConnect-GetStructuredRecord-Operation-1](https://fhir.nhs.uk/STU3/OperationDefinition/GPConnect-GetStructuredRecord-Operation-1/_history/1.13) `OperationDefinition` | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The provider could not parse the `Parameters` resource.  | [`INVALID_RESOURCE`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| No recognised parameters are provided | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `patientNHSNumber` parameter is not provided | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| The `patientNHSNumber` parameter value is invalid, for example it fails format or check digit tests | [`INVALID_NHS_NUMBER`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The patient has dissented to sharing their clinical record | [`NO_PATIENT_CONSENT`](development_fhir_error_handling_guidance.html#security-validation-errors) |
| A patient could not be found matching the `patientNHSNumber` provided | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| An unauthorised request has been made for sensitive information  | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The patient's NHS number in the provider system is not associated with a NHS number status indicator code of 'Number present and verified' | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| The request is for a sensitive patient | [`PATIENT_NOT_FOUND`](development_fhir_error_handling_guidance.html#identity-validation-errors) |
| A part parameter is passed without a value | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
| An unrecognised parameter is included in the request | [`INVALID_PARAMETER`](development_fhir_error_handling_guidance.html#resource-validation-errors) |
|-------------------------|-------------------|


### Request response ###

#### Response headers ####

```http
HTTP/1.1 200 OK
Cache-Control: no-store
Content-Type: application/fhir+json; charset=utf-8
Date: Sun, 07 Aug 2016 11:13:05 GMT
Content-Length: 1464
```

#### Payload response body ####

Provider systems **MUST**:

- return a `200` **OK** HTTP status code to indicate successful retrieval of a patient's structured record
- return a `Bundle` conforming to the [`GPConnect-StructuredRecord-Bundle-1`](https://fhir.nhs.uk/STU3/StructureDefinition/GPConnect-StructuredRecord-Bundle-1/_history/1.3) profile definition
- return the following resources in the `Bundle`:
  - `Patient` matching the NHS Number sent in the body of the request
  - `Organization` matching the patient's previously registered GP practice, where their record is being migrated from, referenced from `Patient.generalPractitioner`
  - `Organization` matching the organisation serving the request, if different from above, referenced from `Patient.managingOrganization`
  - `Practitioner` matching the patient's usual GP, if they have one, referenced from `Patient.generalPractitioner`
  - `PractitionerRole` matching the usual GP's role
  - resources holding consultations, problems, immunisations, allergies, intolerance, medications, uncategorised data, referrals, investigations and diary entries according to the rules below:

Provider systems **SHOULD**:

- provide a consistent order to elements within the `Bundle` resource.  It is recommended to follow the order described in the [Bundle population illustrated](accessrecord_structured_development_retrieve_patient_record.html#bundle-population-illustrated) diagram.

Consumers systems **MUST NOT**:

- rely on order or index of elements within the `Bundle` resource in order to parse encapsulated resources.

##### Full record #####

Provider systems **MUST** include the following in the response `Bundle`:

- when the `includeFullRecord` parameter is not set:

  - no clinical information shall be returned

- when the `includeFullRecord` parameter is set:

- A [`List`](accessrecord_structured_development_list.html) resource for each clinical area referencing resources that have been returned
- A [`List`](accessrecord_structured_development_list.html) resource for secondary lists referencing resources contained in requested problems and consultations

- [`MedicationStatement`](accessrecord_structured_development_medicationstatement.html), [`MedicationRequest`](accessrecord_structured_development_medicationrequest.html), [`Medication`](accessrecord_structured_development_medication.html) resources representing the patient's medication
- [`AllergyIntolerance`](accessrecord_structured_development_allergyintolerance.html) resources representing the patient's allergies and intolerances
- [`List`](accessrecord_structured_development_list.html), [`Condition`](accessrecord_structured_problems.html), [`Encounter`](accessrecord_structured_development_encounter.html), [`List - Consultation`](accessrecord_structured_development_list_consultation.html) and [`Observation - narrative`](accessrecord_structured_development_guidance_observation_narrative.html) resources representing the patient's consultations
- [`Condition`](accessrecord_structured_problems.html) resources representing the patient's problems
- [`Immunization`](accessrecord_structured_development_immunization.html) resources representing the patient's immunisations
- [`Observation - uncategorised`](accessrecord_structured_development_observation_uncategorisedData.html) resources representing the patient's uncategorised data
- [`DiagnosticReport`](accessrecord_structured_development_DiagnosticReport.html), [`Observation - Test Group Header`](accessrecord_structured_development_observation_testGroup.html), [`Observation - Test Result`](accessrecord_structured_development_observation_testResult.html), [`Observation - Filing Comments`](accessrecord_structured_development_observation_filingComments.html), [`ProcedureRequest`](accessrecord_structured_development_ProcedureRequest.html), [`Specimen`](accessrecord_structured_development_specimen.html), [`DocumentReference`]() resources representing the patient's test results
- [`ReferralRequest`](accessrecord_structured_development_referralrequest.html) resources representing the patient's referrals will be returned.
- [`ProcedureRequest`](accessrecord_structured_development_diaryentry.html) resources representing the patient's diary entries will be returned.
- [`DocumentReference`]() resources representing the patient's documents.

- and when the `includeSensitiveInformation` parameter is set to `false`:

  - only non confidential information will be returned

- and when the `includeSensitiveInformation` parameter is set to `true`:

  - confidential and sensitive information will be returned

##### Documents #####
 `DocumentReference` resources containing document metadata including location will be returned as part of the response `Bundle`. Retrieval of these **MUST** be performed using the [Retrieve a document](access_documents_development_retrieve_patient_documents.html) API in the [Access Document capability](access_documents.html).
