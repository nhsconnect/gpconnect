---
title: Referrals
keywords: getcarerecord, view, section, referrals
tags: [view,getcarerecord]
sidebar: accessrecord_sidebar
permalink: accessrecord_view_referrals.html
summary: "Referrals HTML view"
---


| Section code | Section name | TPP | EMIS | Vision | Microtest |
| ------------ | ------------ |-----|------|------|-----------|
| REF | Referrals | Yes | Yes | Yes | Yes |

## Clinical narrative ##

This is a request for transfer of care or request to provide assessment, treatment or clinical advice on the care a patient.

## Purpose ##

The purpose of this section is to provide details of any referrals to other care providers.

## Sections and subsections ##

There is only a single main section for Referrals with no subsections.

## Section title ##

The section title **SHALL** be "Referrals".

## Date filter ##

A date filter is applicable for the Referrals section.


## Section content banner ##

Provider's message describing at a summary level how they have populated this section:

<div class="panel-group" id="accordion">
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseOne">EMIS message descriptions (click here to expand/collapse) </a>
						</div>
                        <div id="collapseOne" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>Always displays this text:</b></p>
									<ul>
										<li>Contains referrals related to the patient.</li>
									</ul>
								<p><b>Only displayed if a date filter is applied:</b></p>
									<ul>
										<li>For the selected date range DD-MMM-YYYY to DD-MMM-YYYY subject to patient preferences and/or Royal College of General Practitioners (RCGP) exclusions.</li>
									</ul>
                            </div>
                        </div>
                    </div>
                    <!-- /.panel -->
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseTwo">TPP message descriptions (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseTwo" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>If data is hidden due to sharing preferences (only shows if data is contained within current date range):</b></p>
									<ul>
										<li>Some patient data is hidden by sharing rules. The data in this section may be incomplete.</li>
									</ul>
								<p><b>Displayed dependent on date range:</b></p>
									<ul>
										<li>Data for the period DD-MMM-YYYY to DD-MMM-YYYY.</li>
										<li>All Data Items from DD-MMM-YYYY.</li>
										<li>All Data Items until DD-MMM-YYYY.</li>
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
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseThree">INPS message descriptions (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseThree" class="panel-collapse collapse noCrossRef">
                            <div class="panel-body">
								<p><b>Only displayed if a date filter is not applied:</b></p>
									<ul>
										<li>All relevant items subject to patient preferences and/or RCGP exclusions.</li>
									</ul>
								<p><b>Only displayed if a date filter is applied:</b></p>
									<ul>
										<li>For the period DD-MMM-YYYY to DD-MMM-YYYY.</li>
									</ul>
                            </div>
                        </div>
                    </div>
                    <!-- /.panel -->
                    <div class="panel panel-default">
                        <div class="panel-heading">
                                <a class="noCrossRef accordion-toggle" data-toggle="collapse" data-parent="#accordion" href="#collapseFour">Microtest message descriptions (click here to expand/collapse)</a>
                        </div>
                        <div id="collapseFour" class="panel-collapse collapse">
                            <div class="panel-body">
								<p><b>Always displays this text:</b></p>
									<ul>
										<li>Contains items relating to 'Referral for Further Care'; may include repeated entries due to duplicated data in the source system.</li>
									</ul>
								<p><b>Only displayed if a date filter is not applied:</b></p>
									<ul>
										<li>All relevant items.</li>
									</ul>
								<p><b>Only displayed if a date filter is applied:</b></p>
									<ul>
										<li>For the period DD-MMM-YYYY to DD-MMM-YYYY.</li>
									</ul>
                            </div>
                        </div>
                    </div>
</div>


## Table columns ##

Providers must return all the columns as described in the table below:

| Order | Name | Description | Value details &nbsp;&nbsp;&nbsp; |
| ------------ | ------------ | ------------ |
| <center>1</center> | `Date` | The date of the referral | `dd-Mmm-yyyy` |
| <center>2</center> | `From` | Practitioner or Organization referred from | `free-text` |
| <center>3</center> | `To` | Practitioner or Organization referred to | `free-text` |
| <center>4</center> | `Priority` | The priority of the referral | `free-text` |
| <center>5</center> | `Details` | Longer human readable details for the referral | `free-text` |


## HTML view ##

{% include accessrecord/referrals.html %}


## Example view ##

<p data-height="580" data-theme-id="light" data-slug-hash="jYPVxN" data-default-tab="result" data-user="tford70" data-embed-version="2" data-pen-title="Referrals" class="codepen">See the Pen <a href="https://codepen.io/tford70/pen/jYPVxN/">Referrals</a> by gp_connect (<a href="https://codepen.io/tford70">@tford70</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://production-assets.codepen.io/assets/embed/ei.js"></script>

{% include tip.html content="Please see [CodePen](https://codepen.io/gpconnect/pen/jYPVxN) for example of using AngularJS to generate table content." %}
