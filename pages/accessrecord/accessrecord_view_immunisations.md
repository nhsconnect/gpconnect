---
title: Immunisations
keywords: getcarerecord, view, section, immunisations
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_immunisations.html
summary: "Immunisations HTML View."
---

## Immunisations ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| IMM | Immunisations | Yes | Yes | Yes | Yes |

### Clinical Narrative ###

Immunisation is the process whereby a person is treated to provide immunity or resistance to an infectious disease, typically by the administration of a vaccine.

### Purpose ###

The purpose of this section is to provide the health care professional with information about any immunisations that have been administered to the patient.

### Sections and Subsections ###

There is only a single main section for the Immunisations section with no subsections.

### Date Filter ###

Date filters are not supported for this section all relevant records shall be returned.

### Section Banner Content ###

Providers message describing at a summary level how they have populated this section:

<div class="panel-group" id="accordion">
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseOne">EMIS banner content (click here to expand/collapse) </a>
						</div>
                        <div id="collapseOne" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>Always displays this text:</b></p>
									<ul>
										<li>Contains coded immunisations on the patient record; some immunisations may exist as issued medications also.</li>
										<li>Content and Part not supported.</li>
									</ul>
                            </div>
                        </div>
                    </div>
                    <!-- /.panel -->
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseTwo">TPP banner content (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseTwo" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>Displayed dependent on date range:</b></p>
									<ul>
										<li>All relevant items.</li>
									</ul>
								<p><b>If GP2GP in progress:</b></p>
									<ul>
										<li>Record is in transit and may be incomplete.</li>
									</ul> 
                            </div>
                        </div>
                    </div>
                    <!-- /.panel -->
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseThree">INPS banner content (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseThree" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>Always displays this text:</b></p>
									<ul>
										<li>All relevant items subject to patient preferences and/or RCGP exclusions.</li>
									</ul>
                            </div>
                        </div>
                    </div>
                    <!-- /.panel -->
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseFour">MicroTest banner content (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseFour" class="panel-collapse collapse">
                            <div class="panel-body">
                                	No section banner text displayed.
                            </div>
                        </div>
                    </div>
</div>


### Table Construction Requirements ###

Providers must adhere to the table construction requirements listed below:

- Table header **SHALL** be "Immunisations".
- Table columns **SHALL** be ordered left-to-right (1..N).
- Table content **SHALL NOT** be truncated.
- Table rows **SHALL** be ordered by date descending (i.e. most recent date/time first).


### Table Columns ###

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value Details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` | The date of the immunisation | `dd-Mmm-yyyy` |
| <center>2</center> | `Vaccination` | A short human readable free-text title for the immunisation | `free-text` |
| <center>3</center> | `Part` | Part number of immunisation | `integer` |
| <center>4</center> | `Contents` | Contents of the immunisation | `free-text` |
| <center>5</center> | `Details` | Longer human readable details for the immunisation | `free-text` |


### HTML View ###

{% raw %}
```html
<div>
	<h2>Immunisations</h2>
	<table>
		<thead>
			<tr>
				<th>Date</th>
				<th>Vaccination</th>
				<th>Part</th>
				<th>Contents</th>
				<th>Details</th>
			</tr>
		</thead>
		<tbody>
			<tr ng-repeat="item in items">
				<td>{{item.date}}</td>
				<td>{{item.vaccination}}</td>
				<td>{{item.part}}</td>
				<td>{{item.contents}}</td>
				<td>{{item.details}}</td>
			</tr>
		</tbody>
	</table>
</div>
```
{% endraw %}

{% include custominfocallout.html content="**Important:** AngularJS tags (e.g ng-repeat) are present merely to indicate to a developer the structure of the table content. Presence of these tags are not intended to imply use of any specific technology." type="warning" %}

## Example View ##

<p data-height="425" data-theme-id="light" data-slug-hash="MXxLwX" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Immunisations" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/MXxLwX/">Immunisations</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/MXxLwX) for example of using AngularJS to generate table content" %}