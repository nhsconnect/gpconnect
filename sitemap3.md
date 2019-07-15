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
                [Consumer suppliers](overview_consumer_supplier.html)

[Clinical system suppliers](overview_clinical_system_supplier.html)

[End-user organisations](https://digital.nhs.uk/services/gp-connect) (external site)
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

[System demonstrator](system_demonstrator.html)

[Interactive API documentation](system_swagger.html)

[Postman examples](system_reference_postman.html)
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

[Development assets](development_deliverables.html)

[FHIR library](development_fhir_open_source_guidance.html)

[FHIR implementation](development_fhir_api_guidance.html)

[General API guidance](development_general_api_guidance.html)

[Operations](development_fhir_operation_guidance.htm)

[Resources](development_fhir_resource_guidance.html)

[Security guidance](development_api_security_guidance.html)

[Error handling](development_fhir_error_handling_guidance.html)

[Volume and performance](development_api_volume_and_performance.html)

[Non-functional requirements](development_api_non_functional_requirements.html)

[First of type](overview_first_of_type.html)
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
               <div class="panel-body">When you're building, publishing, and deploying your Jekyll site, you might find these topics helpful.
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
                  These pages highlight special layouts outside of the conventional page and TOC hierarchy.
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


