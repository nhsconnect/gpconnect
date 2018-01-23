---
title: GP Connect Specification Versions
keywords: about
tags: [getting_started]
sidebar: overview_sidebar
toc: false
permalink: overview_specification_versions.html
summary: "Published GP Connect spcification versions"
---

## Specification Versioning ##

### Historical versioning model ###

Versioning of the GP Connect specificationhas been historically done using a seperate version for each area of the specification, the cross funtional requiremnet have one version and each of the different capability packs, such as Appointment Mangement and Access Record HTML, have their own versions.

The spec has been in a rapid development cycle with lots of change and updates based on analysis of requirements and feedback. Throughout this rapid development cycle the analysis and validating has focused on one capability packs at a time, moving onto the next area of the specification when the previous one has been updated and validated. When we move from FHIR DSTU2 to STU3 the process of working on one area of the spec at a time resulted in a breaking miss match between different areas of the spec, this lead to a re-evaluation of the way GP Connect does specification versioning.


### Current versioning model ###

Rather than versioning the different parts of the spec with different release versions, GP Connect has moved to a model where the whole spec will be versioned under a single version which respresents a snapshot of the spec at that point in time.

{% include note.html content="GP Connect have not yet done a release of the specification with a single overarching version. The release table below only contains the releases that have previously been done, and that we expect consumers and providers to build against." %}


## Published Specification Versions ##

The table below contains the official releases of the GP Connect specification that consumers and providers should develope against.

<table>
	<tr>
		<th class="tableColumn15">Release Date</th>
		<th class="tableColumn30">Version</th>
		<th>Details</th>
		<th>Testing</th>
	</tr>
	<tr>
		<td>
			<a href="https://developer.nhs.uk/apis/gpconnect/" >Current Version</a>
		</td>
		<td>GP Connect Core rc.1,<br/>
			Foundations rc.4,<br/>
			Appointment rc.3,<br/>
			Access Record HTML rc.5
		</td>
		<td>The current published version are as specified but if you are building Appointments and Foundations you should build against the specification version published on 18th Jan 2018. If you are building HTML you should build against the specification released on 13th Oct 2017.<br/>
			<br/>
			<b>NOTE:</b> the core part of the specification between the two releases has changed from DSTU2 to STU3 and therefore are not compatible.
		</td>
		<td><a href="https://github.com/nhsconnect/gpconnect-provider-testing/tree/master">Automated Test Suite</a></td>
	</tr>
	<tr class="tableSubHeading">
		<th>STU3</th>
		<th/>
		<th/>
		<th/>
	</tr>
	<tr>
		<td><a href="https://developer.nhs.uk/apis/gpconnect-18Jan2018/">18 Jan 2018</a></td>
		<td>GP Connect Core rc.1,<br/>
			Appointments rc.3,<br/>
			Foundations rc.4
		</td>
		<td>STU3 Update profiles for Appointment Management, Foundations as well as a number of updates to the core, cross cutting, areas of the specification.</td>
		<td><a href="">Automated Test Suite</a></td>
	</tr>
	<tr class="tableSubHeading">
		<th>DSTU2</th>
		<th/>
		<th/>
		<th/>
	</tr>
	<tr>
		<td><a href="https://developer.nhs.uk/apis/gpconnect-13Oct2017/">13 Oct 2017</a></td>
		<td>Access Record HTML rc.5,<br/>
			Appointments rc.2,<br/>
			Foundations rc.3
		</td>
		<td>This version is the release of the specification you should use if you are building Access Record HTML rc.5 as a consumer or a provider.</td>
		<td><a href="https://github.com/nhsconnect/gpconnect-provider-testing/releases/tag/Foundations_RC3_Appointments_RC2">Automated Test Suite</a></td>
	</tr>
</table>