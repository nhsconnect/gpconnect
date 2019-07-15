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
                  [Exploring GP Connect](overview_explore.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[System demonstrator](system_demonstrator.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Interactive API documentation](system_swagger.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Postman examples](system_reference_postman.html)
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
               <div class="panel-body">[Developing with GP Connect](overview_development.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Development assets](development_deliverables.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[FHIR library](development_fhir_open_source_guidance.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[FHIR implementation](development_fhir_api_guidance.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[General API guidance](development_general_api_guidance.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Operations](development_fhir_operation_guidance.htm)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Resources](development_fhir_resource_guidance.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Security guidance](development_api_security_guidance.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Error handling](development_fhir_error_handling_guidance.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Volume and performance](development_api_volume_and_performance.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Non-functional requirements](development_api_non_functional_requirements.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[First of type](overview_first_of_type.html)
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
               <div class="panel-body">[Test and assurance](overview_test_and_assurance.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Testing assets](testing_deliverables.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Test environments](testing_environments.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Provider testing](testing_api_provider_testing.html)

<a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>[Consumer testing](testing_api_consumer_testing.html)

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
                  <a href="https://gpc-spec-restructure.netlify.com/index.html">Introduction</a>Deploying your system](overview_deployment.html)
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


