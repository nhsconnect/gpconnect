---
title: Composition Resource Delta
keywords: development, fhir, resource, composition
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_composition_resource.html
summary: "Composition resource delta between GP Connect and the base FHIR resource."
---

Overview of changes made to the standard FHIR&reg; DSTU2 [Composition](https://www.hl7.org/fhir/DSTU2/composition.html){:target="_blank"} resource to allow its usage as a Patient Care Record for use within the GP Connect APIs.
								
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
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	subject	</td>
			<td>	0..1<br>Reference(Any)	</td>
			<td>	1..1<br>Reference(Patient)	</td>
			<td>	The patient this care record is about.	</td>
		</tr>
		<tr>
			<td>	author	</td>
			<td>	0..1<br>Reference(Practitioner|Device|Patient|RelatedPerson)	</td>
			<td>	0..1<br>Reference(Device)	</td>
			<td>	The author (source system) of the patient care record.	</td>
		</tr>
		<tr>
			<td>	attester	</td>
			<td>	0..*	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	event	</td>
			<td>	0..*	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	encounter	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	No requirement.	</td>
		</tr>
		<tr>
			<td>	section	</td>
			<td>	0..*	</td>
			<td>	1..1	</td>
			<td> 	Composition is broken into the following text sections: Patient Details, Allergies and Sensitivities, Summary, Administrative Items, Clinical Items, Encounters, Immunisations, Investigations, Medications, Observations, Problems, Referrals.	</td>
		</tr>
	</tbody>
</table>

{% include links.html %}