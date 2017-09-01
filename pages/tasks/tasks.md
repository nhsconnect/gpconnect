---
title: Task Management
keywords: tasks
tags: [tasks]
sidebar: tasks_sidebar
permalink: tasks.html
summary: "All about the task management capability."
---

{% include todo.html content="This capability pack is published as a **work in progress** version and as such is subject to change. It has been published to show the direction of travel and to serve as a discussion document for parties involved with the implementation and consumption of GP Connect FHIR based APIs." %}

## Purpose ##

Demonstrates the ability to manage tasks across care settings and organisational boundaries to improve the quality and timeliness of care being provided to patients by enabling health professionals to share information or request a task be performed in real time:

## Scenarios ##

- A user can send a notification which is for information purposes only.
- A user can send a task requesting a user perform an activity.
- A health professional at a patients registered GP practice sends a task or notification to an extended access hub.
- A health professional at an extended hub is able to identify the patient’s own GP practice and can send a task or notification to that organisation.
- Users are presented with confirmation that a task is successfully delivered to the organisation or that it has failed in real time so they can retry or use an alternative channel.
- Users can make use of notifications and tasks across a range of care settings to demonstrate it applicability across care domains. Any of; 111, A+E, Physio, Acute, Social, Community etc.

Example clinical scenarios for FoT and beyond can be found on the [Tasks Clinical Scenarios](tasks_clinical_scenarios.html) page.

## Use Cases ##

- [Send a task](tasks_send_a_task.html)
{% comment %}
- [Receive a task](tasks_receive_a_task.html)
{% endcomment %}

## Profiled Fhir Resources ##

Please refer to the [Task Management FHIR Resources](datalibrarytasks.html) page for details of the FHIR profiles utilised for the Task Management capability.

## SPINE Interactions

The Tasks capability message set includes the following set of spine interactions:

| Operation                 | InteractionID             | 
|---------------------------|---------------------------| 
|  [Create Task](tasks_use_case_send_a_task.html)               | `urn:nhs:names:services:gpconnect:fhir:rest:create:order` |
