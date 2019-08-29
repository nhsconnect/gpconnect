---
title: Sitemap for Access Record Structured
tags: [sitemap]
keywords: sitemap
permalink: sitemap_structureddel.html
sidebar: home_sidebar
toc: false
---


<div id="grid" class="row">


    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["overview"]'>

               <div class="panel panel-default">
               <div class="panel-heading">Overview</div>
               <div class="panel-body">
               <p><a href="/accessrecord_structured.html">Introduction</a></p>
               <p><a href="/accessrecord_structured_requirements.html">Business requirements</a> </p>
               <p><a href="https://gpc-spec-restructure.netlify.com/pages/accessrecord_structured/GP%20Connect%20Req%20Cat%20-%20Access%20Record%20Structured%20Data%20v1.4.xlsx">Requirements catalogue</a> </p>
               <p><a href="/accessrecord_structured_design.html">Design decisions</a> </p>
                <p><a href="/accessrecord_structured_known_issues.html">Known issues</a> </p>
                                   <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "overview" %}
                  <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %}
                  </ul>
               </div>
            </div>
        </div>


    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["development"]'>

        <div class="panel panel-default">
            <div class="panel-heading">Development</div>
            <div class="panel-body">

<p><a href="/accessrecord_structured_development.html">Overview</a></p>

<p><a href="/accessrecord_structured_development_allergies_guidance.html">Allergies guidance</a></p>

<p><a href="/accessrecord_structured_development_medication_resource_relationships.html">Medication resource relationships</p>

<p><a href="/accessrecord_structured_development_medication_guidance.html">Medication guidance</p>

                <ul>
                    {% for page in site.pages %}
                    {% for tag in page.tags %}
                    {% if tag == "development" %}
                    <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                    {% endif %}
                    {% endfor %}
                    {% endfor %}
                </ul>
            </div>
        </div>

    </div>



    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["resources"]'>

                <div class="panel panel-default">
               <div class="panel-heading">FHIR&reg; resources</div>
               <div class="panel-body">
                  <p><a href="/accessrecord_structured_development_resources_overview.html">Overview</a></p>

<p><a href="/accessrecord_structured_development_allergyintolerance.html">AllergyIntolerance</a></p>

<p><a href="/accessrecord_structured_development_medication.html">Medication</a></p>

<p><a href="/accessrecord_structured_development_medicationstatement.html">MedicationStatement</a></p>

<p><a href="/accessrecord_structured_development_medicationrequest.html">MedicationRequest</a></p>

<p><a href="/accessrecord_structured_development_list.html">List</a></p>

<p><a href="/accessrecord_structured_development_bundle.html">Bundle</a></p>

                  <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "resources" %}
                  <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %}
                  </ul>
               </div>
            </div>

    </div>

    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["examples"]'>

      <div class="panel panel-default">
               <div class="panel-heading">FHIR&reg; examples</div>
               <div class="panel-body">

<p><a href="/accessrecord_structured_development_fhir_examples_allergies.html">Allergies</a></p>

<p><a href="/accessrecord_structured_development_fhir_examples_medication.html">Medication</a></p>


               <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "examples" %}
                  <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %}
               </ul>
            </div>
         </div>

    </div>

       <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["definition"]'>

           <div class="panel panel-default">
               <div class="panel-heading">API definition</div>
               <div class="panel-body">

<p><a href="/accessrecord_structured_development_retrieve_patient_record.html">Retrieve a patient's structured record</a></p>


                   <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "definition" %}
                  <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %}
                   </ul>
               </div>
            </div>
    </div>

        <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["spare"]'>

             <div class="panel panel-default">
               <div class="panel-heading">Spare</div>
               <div class="panel-body">
                  <p><a href="/overview_deployment.html">Deploying your system</a></p>
                  <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "spare" %}
                     <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %}
                  </ul>
               </div>
            </div>
    </div>

          <!-- sizer -->
      <div class="col-xs-6 col-sm-4 col-md-1 shuffle_sizer"></div>          




{% unless site.output == "pdf" %}
{% include initialize_shuffle.html %}
{% endunless %}
