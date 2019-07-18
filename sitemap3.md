---
title: Sitemap
tags: [sitemap]
keywords: sitemap
permalink: sitemap3.html
sidebar:home_sidebar
toc: false
---


<div id="grid" class="row">


    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["overview"]'>

               <div class="panel panel-default">
               <div class="panel-heading">Overview</div>
               <div class="panel-body">
               <a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a> 
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
   

    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["getting-started"]'>

        <div class="panel panel-default">
            <div class="panel-heading">Getting started</div>
            <div class="panel-body">
                
<p><a href="https://gpc-spec-restructure.netlify.com/overview_consumer_supplier.html">Consumer suppliers</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/overview_clinical_system_supplier.html">Clinical system suppliers</a></p>

<p><a href="https://digital.nhs.uk/services/gp-connect">End-user organisations</a> (external site)</p>

                <ul>
                    {% for page in site.pages %}
                    {% for tag in page.tags %}
                    {% if tag == "content-types" %}
                    <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                    {% endif %}
                    {% endfor %}
                    {% endfor %}
                </ul>
            </div>
        </div>
        
    </div>



    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["explore"]'>

                <div class="panel panel-default">
               <div class="panel-heading">Explore</div>
               <div class="panel-body">
                  <p><a href="https://gpc-spec-restructure.netlify.com/overview_explore.html">Exploring GP Connect</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/system_demonstrator.html">System demonstrator</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/system_swagger.html">Interactive API documentation</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/system_reference_postman.html">Postman examples</a></p>
                  <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "formatting" %}
                  <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %}
                  </ul>
               </div>
            </div>

    </div>

    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["Develop"]'>
         
      <div class="panel panel-default">
               <div class="panel-heading">Develop</div>
               <div class="panel-body">
               
<p><a href="https://gpc-spec-restructure.netlify.com/overview_development.html">Developing with GP Connect</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_deliverables.html">Development assets</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_fhir_open_source_guidance.html">FHIR library</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_fhir_api_guidance.html">FHIR implementation</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_general_api_guidance.html">General API guidance</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_fhir_operation_guidance.html">Operations</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_fhir_resource_guidance.html">Resources</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_api_security_guidance.html">Security guidance</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_fhir_error_handling_guidance.html">Error handling</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/development_api_volume_and_performance.html">Volume and performance</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/evelopment_api_non_functional_requirements.html">Non-functional requirements</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/overview_first_of_type.html">First of type</a></p>
               <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "single_sourcing" %}
                  <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %} 
               </ul>
            </div>
         </div>

    </div>

       <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["test-assure"]'>

           <div class="panel panel-default">
               <div class="panel-heading">Test and assure</div>
               <div class="panel-body">
               
<p><a href="https://gpc-spec-restructure.netlify.com/overview_test_and_assurance.html">Test and assurance</a></p>
             
<p><a href="https://gpc-spec-restructure.netlify.com/testing_deliverables.html.html">Testing assets</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/testing_environments.html">Test environments</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/testing_api_provider_testing.html">Provider testing</a></p>

<p><a href="https://gpc-spec-restructure.netlify.com/testing_api_consumer_testing.html">Consumer testing</a></p>

                   <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "publishing" %}
                  <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %}
                   </ul>
               </div>
            </div>

    </div>

        <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["deploy"]'>

             <div class="panel panel-default">
               <div class="panel-heading">Deploy</div>
               <div class="panel-body">
                  <p><a href="https://gpc-spec-restructure.netlify.com/overview_deployment.html">Deploying your system</a></p>
                  <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "special_layouts" %}
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


