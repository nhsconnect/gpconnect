---
title: Task Management Resources
keywords: development
sidebar: tasks_sidebar
toc: false
permalink: datalibrarytasks.html
summary: "The fhir prifles and interactions required for the Task Management capability"
---

The following profiled FHIR resources are used in the current version of the Task Management capability, see "API Use Cases" in the menu on the left. Full details of profiled FHIR resources and worked examples are available on the [Task Management DMS Bundle](https://data.developer.nhs.uk/fhir/candidaterelease-170816-tasks/Chapter.1.About/index.html).

---
## ***Send A Task*** ##
### Request ###
* [gpconnect-task-order-1](https://data.developer.nhs.uk/fhir/candidaterelease-170816-tasks/Profile.TaskManagement/gpconnect-task-order-1.html) (based on [FHIR Order](https://www.hl7.org/fhir/DSTU2/order.html))
  * [gpconnect-task-description-basic-1](https://data.developer.nhs.uk/fhir/candidaterelease-170816-tasks/Profile.TaskManagement/gpconnect-task-description-basic-1.html) (based on [FHIR Basic](https://www.hl7.org/fhir/DSTU2/basic.html))

### Response ###
* [gpconnect-task-order-1](https://data.developer.nhs.uk/fhir/candidaterelease-170816-tasks/Profile.TaskManagement/gpconnect-task-order-1.html) (based on [FHIR Order](https://www.hl7.org/fhir/DSTU2/order.html))
  * [gpconnect-task-description-basic-1](https://data.developer.nhs.uk/fhir/candidaterelease-170816-tasks/Profile.TaskManagement/gpconnect-task-description-basic-1.html) (based on [FHIR Basic](https://www.hl7.org/fhir/DSTU2/basic.html))

---
## ***Errors*** ##

If there is a problem with the request or an error occurs during processing of the request then the provider should return a http error along with an "OperationOutcome" Resource within the response payload. Details of the required error responses are available on the [Error Handling Guidance](/development_fhir_error_handling_guidance.html) page within the specification.

### Response ###
* [gpconnect-operationoutcome-1](https://data.developer.nhs.uk/fhir/candidaterelease-170816-getrecord/Profile.GetRecordQueryResponse-HTMLView/gpconnect-operationoutcome-1.html) (based on [FHIR OperationOutcome](https://www.hl7.org/fhir/DSTU2/operationoutcome.html))
