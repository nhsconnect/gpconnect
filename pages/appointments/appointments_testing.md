---
title: Testing Overview
keywords: Testing, Overview
tags: [appointments]
sidebar: appointments_sidebar
permalink: appointments_testing.html
summary: "Testing guidance"
---

Below is the suggested order in which the appointment capabilities should be implemented. The specified order has been recommended around the functionality of the GP Connect Automated Test Suite and any internal dependencies between the test scenarios for the different Appointment Management endpoints. The Appointment Management capability test scenarios are dependent on the foundation capabilities and therefore the foundation endpoints should be developed and tested before implementing the Appointment Management capabilities.

It’s recommended that you develop against the Automated Test Suite as this will help with creating a GP Connect compliant product. By implementing the endpoints in the order below, the Automated Test Suite set of tests for that endpoint can be run during development without you seeing errors due to pre-test API calls or post-test validation API calls relevant to the test being run and failing as they have not been developed yet.

| Order | API endpoint | Test suite endpoint dependencies | Reason for dependency |
| ------------- | ------------- | ------------- | ------------- |
| #1 | Search for free slots | Read an organization / Read a practitioner / Read a location | The `Search for free slots` test scenarios require some of the foundation endpoints to validate references within returned resources contained within the response bundle. |
| #2 | Book an appointment | Register a patient / Find a patient / Search for free slots / Read an organization / Read a location / Read a practitioner / Read a patient | The `Book an appointment` endpoint finds a slot which it then uses to book an appointment for a known patient. To find the logical IDs of the elements required to book an appointment it requires the `Find a patient` and `Search for free slots` endpoints to have been implemented and working. Some of the tests also require the `Register a patient` endpoint to have been implemented as it tests booking an appointment against a GP Connect temporary patient. |
| #3 | Retrieve a patient’s appointments | Search for free slots / Find a patient / Book an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test suite builds the appointments for a patient before testing the `Find a patient’s appointments` capability to make sure appointments exist to find. This requires the endpoints to find free slots, find a patient’s logical identifier, book an appointment and, in some tests, create a temporary patient against which to book the appointment. |
| #4 | Amend an appointment | Search for free slots / Find a patient / Book an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for the `Amend an appointment` capability require most of the foundation endpoints and most of the other appointment endpoints to be implemented to find or create the appointments which the tests are going to update as part of the `Amend an appointment` tests. |
| #5 | Cancel an appointment | Search for free slots / Find a patient / Book an appointment / Amend an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for the `Cancel an appointment` capability require most of the  foundation endpoints and the other Appointment Management endpoints to be implemented in order to find, create and amend the appointments required for the test scenarios and validation of the returned response. |
| #6 | Read an appointment | Search for free slots / Find a patient / Book an appointment / Amend an appointment / Cancel an appointment / Register a patient / Read an organization / Read a location / Read a practitioner / Read a patient | The test scenarios for `Read an appointment` require different foundation endpoints and all the other appointment endpoints to be implemented as the tests need to create appointments with different statuses if they are not available. The test must find the local identifiers for both the appointment it is trying to read and any steps it may need to do to create or validate the appointment. |

