---
title: Appointment Resource Delta
keywords: development, fhir, resource, appointment
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_appointment_resource.html
summary: "Appointment resource delta between GP Connect and the base FHIR resource."
---

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
			<td>	start	</td>
			<td>	0..1	</td>
			<td>	1..1	</td>
			<td>	Date/Time that the appointment is due to take place	</td>
		</tr>		
		<tr>
			<td>	end	</td>
			<td>	0..1	</td>
			<td>	1..1	</td>
			<td>	Date/Time that the appointment is due to conclude	</td>
		</tr>
		<tr>
			<td>	slot	</td>
			<td>	0..*	</td>
			<td>	1..*	</td>
			<td>	XPath of element(s) related to appointment - uses 'gp-connect-slot-1' profile	</td>
		</tr>
		<tr>
			<td>	participant	</td>
			<td>	1..*	</td>
			<td>	1..*	</td>
			<td>	Participants involved in appointment - actor reference fulfilled through use of 'gpconnectpractitioner-1' or 'gpconnect-location-1' or 'gpconnect-patient-1' profile</td>
		</tr>

	</tbody>

</table>

{% include links.html %}