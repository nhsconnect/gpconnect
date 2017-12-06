---
title: Task Management
keywords: tasks
tags: [tasks]
sidebar: tasks_sidebar
permalink: tasks.html
summary: "Overview of the task management capability pack"
---

## Purpose ##

Demonstrates the ability to manage tasks across care settings and organisational boundaries to improve the quality and timeliness of care being provided to patients by enabling health professionals to share information or request a task be performed in real time:

## Scenarios ##

- a user can send a notification which is for information purposes only
- a user can send a task requesting a user perform an activity
- a health professional at a patient's registered GP practice sends a task or notification to an extended access hub
- a health professional at an extended hub is able to identify the patient’s own GP practice and can send a task or notification to that organisation
- users are presented with confirmation that a task is successfully delivered to the organisation or that it has failed in real time so they can retry or use an alternative channel
- users can make use of notifications and tasks across a range of care settings to demonstrate its applicability across care domains, such as 111, A&amp;E, Physio, Acute, Social, Community

Example clinical scenarios for FoT and beyond can be found on the [Tasks Clinical Scenarios](tasks_clinical_scenarios.html) page.

## Use cases ##

- [Send a task](tasks_use_case_send_a_task.html)
{% comment %}
- [Receive a task](tasks_receive_a_task.html)
{% endcomment %}

## Profiled Fhir Resources ##

Please refer to the [Task Management FHIR Resources](datalibrarytasks.html) page for details of the FHIR&reg; profiles utilised for the Task Management capability pack.


## SPINE interactions

The Tasks Management capability message set includes the following set of Spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
|  [Create Task](tasks_use_case_send_a_task.html)               | `urn:nhs:names:services:gpconnect:fhir:rest:create:order` |
