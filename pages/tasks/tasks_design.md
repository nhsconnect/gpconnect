---
title: Tasks Design
keywords: tasks design
tags: [design,tasks]
sidebar: tasks_sidebar
permalink: tasks_design.html
summary: "Overview of the design decisions made in relation to the Task Management capability."
---

## Task Communication ##

Two task communication styles are possible:

- <span class="label label-success">SELECTED</span> One-way / Requires No Acknowledgement.
- Two-way / Requires Acknowledged.

## Task Sender ##

Two task sender types are possible:

- Practitioner sender.
- <span class="label label-success">SELECTED</span> Organisation sender.

## Task Receiver ##

Two task receiver types are possible:

- Practitioner targeted.
- <span class="label label-success">SELECTED</span >Organisation targeted.

## Task Subject ##

A number of task subject options are possible:

- <span class="label label-success">SELECTED</span> Always Patient targeted.
- Potentially Patient targeted.
- Organisation targeted.
- Other

## Task Types ##

Two broad task types are possible:

- <span class="label label-success">SELECTED</span> Informational Only / Notification.
- <span class="label label-success">SELECTED</span> Activity Ordering / Action Expected.<sup>1</sup>

<sup>1</sup> Each expected action needs to be considered in the clinical context as this could be a legal obligation or have clinical safety implications.

### Activity Expected ###

<span class="label label-primary">ACTION</span> We need more clinically validated user stories in-order to provide good quality guidance to the implementers (and end users) of tasks.

## Notification Types ##

Two types of notifications:

- <span class="label label-success">SELECTED</span> Manual / Human Triggered.
- Automated / System Triggered.<sup>1</sup>

<sup>1</sup> We need to consider if automated tasks are desirable (i.e. they have enough clinical benefit vs. the noise they generate).

### Manually Triggered ###

<span class="label label-info">DECISION</span> The provenance of a human initiated task MUST be clear. Hence, the system SHALL supply the details of the user who authored the task.

### Automatically Triggered ###

*Example:* A patient is seen in an acute care setting and the system automatically sends a notification task back to the person's usual GP on the close of the acute encounter.

<span class="label label-danger">RISK</span> There is a potential risk with automated task creation that this could become very spammy within a big federation (and hence lead to important tasks being missed).

## Task Acceptance ##

A patient record (identified by NHS Number) MUST exist in the receiving system to successfully receive a task.

<span class="label label-info">DECISION</span> Tasks without a valid patient reference SHALL be rejected by the receiving system.

### Data Sharing ###

<span class="label label-info">DECISION</span> A local sharing agreement MUST be in place to safely receive tasks.

Two possible approaches:

- Enforced by the Provider system.
- <span class="label label-success">SELECTED</span> Enforced centrally by the Spine Security Proxy.

<span class="label label-info">DECISION</span> Preferred approach is to enforce centrally (i.e. SSP).

### Task Jurisdictions ###

- <span class="label label-success">SELECTED</span> Local Area (i.e. CCG).
- <span class="label label-success">SELECTED</span> From A&E, GP Practice to GP Practice or extended access Hub.
- Out of Area.

<span class="label label-info">DECISION</span> We are not covering Out of Area tasks (as this would be considered from an unsolicited source). This is potentially unsafe as they won't always have the contact details for the organisation who sent the task etc.

# Candidate Design FoT #

## In Scope for FoT ##

For FoT we will only be supporting one-way Patient centric tasks of type "Informational" or "Action Required".

### Generic User Story ###

> Send a task from organisation A to organisation B for patient C."

## FoT Requirements ##

A Task:

- SHALL be one-way only.
- SHALL be of type either Informational or Action based.
- SHALL contain the date/time the task was authored.
- SHALL contain a free-text description/reason.
- SHALL be for a single patient.
   - Subject `Patient`
- SHALL have clear provenance.
   - Sender `Organization`
   - Sender `Practitioner`
- SHALL be addressed to a single target organization.
   - Target `Organization` 
- SHALL NOT be used for time bound orders.
- SHALL NOT be used for variable priority orders.
- SHALL NOT be used for referrals/tariff attracting orders.
- SHALL NOT be used be categorised beyond informational vs. action.

<br/>

<span class="label label-warning">QUESTION</span> Add support for resolving `Practitioner` by GMC/MNC code (as requested by TPP)?

### Clinical Safety ###

- <span class="label label-primary">ACTION</span> Clinical Guidance needs to be provided in relation to clinically safe usage.
 - <span class="label label-default">QUESTION</span> What is the clinical/legal responsibility for actioning certain tasks?
   - <span class="label label-danger">RISK</span> Currently anything can be sent which is potentially dangerous.
     - What is the acceptable level of risk/who manages the risk?



