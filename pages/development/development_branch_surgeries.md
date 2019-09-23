---
title: Branch surgeries
keywords: development 
tags: [development]
sidebar: overview_sidebar
permalink: development_branch_surgeries.html
summary: "Describes how GP Connect manages branch surgery data"
---

## GP practices with multiple surgeries

A GP practice may operate from a single surgery (location) or from multiple surgeries (multiple locations).

In GP Connect, a GP practice is represented by an `Organization` resource, and the surgeries are represented by `Location` resources.  The surgery `Location` is linked to the GP practice `Organization` via the `Location.managingOrganisation` element.

![image-title-here](images/appointments/branch-surgeries.png){:class="img-responsive"}

A GP practice operating multiple surgeries usually designates one of the surgeries as a *main* surgery and the rest as *branch* surgeries. The designation of surgeries as *main* and *branch* doesn't have significant impact on GP Connect other than the main surgery normally having the same name and address as the GP practice, and the branch surgeries having different names and addresses.

When a patient registers at a GP practice with multiple surgeries, they are assigned a 'preferred' surgery, even though the patient is formally registered to the GP practice (organisation) as a whole, and can usually attend appointments at any of the surgeries (locations).

### ODS codes

In GP Connect, an ODS code identifies a GP practice as a whole, and is populated in the `Organization.identifier` element.

{% include important.html content="While ODS *site* codes do exist to identify some branch surgeries, GP systems DO NOT use these and hence they are NOT available via the GP Connect interface, and cannot be used to route requests to individual surgeries." %}

#### Personal Demographics Service

The [Personal Demographics Service](integration_personal_demographic_service.html) is used by GP Connect consuming systems to verify a patient's identity, and also to retrieve the ODS code of a patient's registered GP practice.

The ODS code stored in a patient's PDS record represents the GP practice as a whole, and does not identify the patient's preferred surgery.

#### GP Connect routing

GP Connect uses ODS codes in order to route requests to a GP practice by including the practice's ODS code in the URL (see [Service Root URL](development_general_api_guidance.html#service-root-url)).

Therefore, when a GP Connect request is sent, it is sent to a practice as a whole, and not to a specific surgery.

The following query to read a `Patient` resource is being sent to the patient's GP practice identified by the ODS code `D82809`:

<code class="highlighter-rouge">https://provider.nhs.uk/<b>D82809</b>/STU3/1/gpconnect/Patient/1</code>

### Implications for Access Record HTML and Access Record Structured

There are no implications for Access Record HTML and Access Record Structured because the patient's record is requested from the GP practice as a whole and not from an individual surgery.

### Implications for Appointment Management

Because a GP practice's appointment book can hold appointments across multiple surgeries (locations), it is important to distinguish which surgery an appointment is held at, to allow the patient to decide where they wish to attend.

In order to do this, every `Schedule` resource has an associated `Location` resource which represents the surgery that the appointment will take place at, including the surgery's name, address and contact details.

To retrieve the patient's preferred surgery (assigned when they registered with the practice), a reference to the surgery `Location` is held in `Patient.registrationDetails.preferredBranchSurgery`.  This can be used to identify  appointment slots at the patient's preferred surgery by comparing its logical id with that of the `Location` resource referenced from the `Schedule.actor` element.
