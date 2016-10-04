---
title: Order Resource Delta
keywords: development, fhir, resource, order
tags: [fhir,development]
sidebar: datalibrary_sidebar
permalink: datalibrary_delta_order_resource.html
summary: "Order resource delta between GP Connect and the base FHIR resource."
---

Overview of changes made to the standard FHIR&reg; DSTU2 [Order](https://www.hl7.org/fhir/DSTU2/order.html){:target="_blank"} resource for use as a Task for use within the GP Connect APIs. (Note: Consumer = Task Sender, Provider = Task Receiver)

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
			<td>	0..* 	</td>
			<td>	0..1	</td>
			<td>	Single local business identifier to be assigned by the Provider system.	</td>
		</tr>
		<tr>
			<td>	subject	</td>
			<td>	1..1 <br>Reference(<br>Patient|Group|Device|Substance) 	</td>
			<td>	1..1 <br>Reference(Patient)	</td>
			<td>	All tasks are (currently) to be linked to a Patient resource. .	</td>
		</tr>
		<tr>
			<td>	source	</td>
			<td>	0..1 <br>Reference(<br>Practitioner|Organization)	</td>
			<td>	0..1 <br>Reference(Practitioner|Organization)	</td>
			<td>	All tasks are (currently) to be sent from a shared Organisation inbox (Practitioner has not been profiled out but is not supported yet).	</td>
		</tr>
		<tr>
			<td>	target 	</td>
			<td>	0..1 <br>Reference(<br>Organization|Device|Practitioner)	</td>
			<td>	1..1 <br>Reference(Organization)	</td>
			<td>	All tasks are (currently) to be addressed to an Organisation-level inbox.	</td>
		</tr>
		<tr>
			<td>	reason	</td>
			<td>	0..1	</td>
			<td>	1..1	</td>
			<td>	Field has been modified to only allow the distinction between the two task types to be expressed.	</td>
		</tr>
		<tr>
			<td>	when	</td>
			<td>	0..1	</td>
			<td>	0..0	</td>
			<td>	Not required. Tasks are not (currently) time bound.	</td>
		</tr>
		<tr>
			<td>	detail	</td>
			<td>	1..*	</td>
			<td>	1..1	</td>
			<td>	All tasks must contain task details as a single free-text narrative.	</td>
		</tr>
	</tbody>
</table>

{% include roadmap.html content="In the near future tasks will include the ability to send to an organisation without patient context but this breaking change to the exiting specification will most likely be implemented alongside a move towards the DSTUv3 'task' resource when it is released." %}


Overview of changes made to the standard FHIR&reg; DSTU2 Basic resource for use as a Task Description within the GP Connect Order resource.

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
			<td>	0..0	</td>
			<td>	No requirement - removed as the basic resource is used as a contained resource and will not be retrieved independently.	</td>
		</tr>
	</tbody>
</table>

