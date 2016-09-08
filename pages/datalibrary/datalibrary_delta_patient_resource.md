---
title: Patient Resource Delta
keywords: development, fhir, resource, patient
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_patient_resource.html
summary: "Patient resource delta between GP Connect and the base FHIR resource."
---

Overview of changes made to the standard FHIR&reg; DSTU2 [Patient](https://www.hl7.org/fhir/DSTU2/patient.html){:target="_blank"} resource for use within the GP Connect APIs.

<table>
	<thead>
		<tr>
			<th>Field</th>
			<th>Baseline</th>
			<th>Change</th>
			<th>Description</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>	identifier	</td>
			<td>	0..*	</td>
			<td>	1..*	</td>
			<td>	A mandatory NHS Number identifier for the patient with option to include other identiers for the patient.	</td>
		</tr>
		<tr>
			<td>	photo	</td>
			<td>	0..*	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	animal	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	careProvider	</td>
			<td>	Reference(Practitioner|Organization)	</td>
			<td>	Reference(Practitioner)	</td>
			<td>	Patient's nominated primary care GP.	</td>
		</tr>
		<tr>
			<td>	managingOrganization	</td>
			<td>	Reference(Organization)	</td>
			<td>	Reference(Organization)	</td>
			<td>	Organisation that is the custodian of the patient record.	</td>
		</tr>
		<tr>
			<td>	link	</td>
			<td>	0..*	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
	</tbody>
</table>


{% include links.html %}