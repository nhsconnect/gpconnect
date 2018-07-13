---
title: Summary
keywords: getcarerecord, view, section, summary
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_summary.html
summary: "Summary HTML View."
---

## Summary ##

| Section Code | Section Name | TPP | EMIS | INPS | Microtest |
| ------------ | ------------ |
| SUM | Summary | Yes | Yes | Yes | Yes |


### Clinical Narrative ###

Clinicians work in busy and time-pressured environments. They need access to high quality, relevant and wherever possible consistent information to support safe, effective and efficient assessment of their patients.

Timely sharing of clinical information is key to the delivery and improvement of safe and effective clinical care.

### Purpose ###

The purpose of this section is to provide a summarised view of the pertinent clinical information regarding a patient within a single screen. This allows a clinician to efficiently peruse key information from the patient’s clinical record and supports clinical decision making.

### Sections and Subsections ###

There is only a single main section for the Summary section with 5 subsections:

 - [Active Problems and Issues](accessrecord_view_summary.html#active-problems-and-issues)
 - [Current Medication Issues](accessrecord_view_summary.html#current-medication-issues)
 - [Current Repeat Medications](accessrecord_view_summary.html#current-repeat-medications)
 - [Current Allergies and Adverse Reactions](accessrecord_view_summary.html#current-allergies-and-adverse-reactions)
 - [Last 3 Encounters](accessrecord_view_summary.html#last-3-encounters)
 
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
										<li>Non - BNF designated items e.g. local mixtures, have been excluded.</li>
										<li>Past medications may include prescriptions which have been cancelled or discontinued before the original prescribed end date.</li>
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
								<p><b>If data is hidden due to sharing preferences (only shows if data is contained within current date range):</b></p>
									<ul>
										<li>Some patient data is hidden by sharing rules. The data in this section may be incomplete.</li>
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


## Active Problems and Issues ##

This section is an exact replica of the Active Problems and Issues section, which is the first subsection within the Problems and Issues section. Further detail about this subsection can be found there including any date range filtering and business rules.

{% include callout.html content="Please see HTML guidance in the [Active Problems and Issues](accessrecord_view_problems.html#active-problems-and-issues) section. " type="primary" %} 


## Current Medication Issues ##

This section is an exact replica of the Current Medication Issues section, which is the first subsection within the Medications section. Further detail about this subsection can be found there including any date range filtering and business rules.

{% include callout.html content="Please see HTML guidance in the [Current Medication Issues](accessrecord_view_medications.html#current-medication-issues) section. " type="primary" %} 


## Current Repeat Medications ##

This section is an exact replica of the Current Repeat Medications section, which is the second subsection within the Medications section. Further detail about this subsection can be found there including any date range filtering and business rules.

{% include callout.html content="Please see HTML guidance in the [Current Repeat Medications](accessrecord_view_medications.html#current-repeat-medications) section. " type="primary" %} 


## Current Allergies and Adverse Reactions ##

This section is an exact replica of the Current Allergies and Adverse Reactions section, which is the first subsection within the Allergies and Adverse Reactions section. Further detail about this subsection can be found there including any date range filtering and business rules.

{% include callout.html content="Please see HTML guidance in the [Current Allergies and Adverse Reactions](accessrecord_view_allergies.html#current-allergies-and-adverse-reactions) section. " type="primary" %} 


## Last 3 Encounters ##

This section is an exact replica of the Encounters section with a filter applied to show the three most recent encounters. Further detail about this section can be found there including any date range filtering and business rules.

{% include callout.html content="Please see HTML guidance in the [Encounters](accessrecord_view_encounters.html) section. " type="primary" %} 

{% include important.html content="the Section title for Encounters on the Summary View should explicitly state 'Last 3 Encounters'.  The columns and content should be as per the HTML guidance for Encounters with the exception of only 3 rows in the table." %}  



## Example View ##

<p data-height="2500" data-theme-id="light" data-slug-hash="opXBjM" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Patient Summary" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/opXBjM/">Patient Summary</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/opXBjM) for example of using AngularJS to generate table content" %}