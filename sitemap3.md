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
               <p><a href="/index.html">Introduction</a></p>
               <p><a href="/pages/support_faq.html">Frequently asked questions</a></p>
               <p><a href="/pages/overview/overview_glossary.html">Glossary</a> </p>
               <p><a href="/pages/support/support_communications.html">Communications channels</a> </p>
               
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
                
<p><a href="/pages/support_faq.html">Consumer suppliers</a></p>

<p><a href="/pages/support_faq.html">Clinical system suppliers</a></p>

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

<p><a href="/pages/support_faq.html">System demonstrator</a></p>

<p><a href="/pages/support_faq.html">Interactive API documentation</a></p>

<p><a href="/pages/support_faq.html">Postman examples</a></p>
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
               
<p><a href="/pages/support_faq.html">Developing with GP Connect</a></p>

<p><a href="/pages/support_faq.html">Development assets</a></p>

<p><a href="/pages/support_faq.html">FHIR library</a></p>

<p><a href="/pages/support_faq.html">FHIR implementation</a></p>

<p><a href="/pages/support_faq.html">General API guidance</a></p>

<p><a href="/pages/support_faq.html">Operations</a></p>

<p><a href="/pages/support_faq.html">Resources</a></p>

<p><a href="/pages/support_faq.html">Security guidance</a></p>

<p><a href="/pages/support_faq.html">Error handling</a></p>

<p><a href="/pages/support_faq.html">Volume and performance</a></p>

<p><a href="/pages/support_faq.html">Non-functional requirements</a></p>

<p><<a href="/pages/support_faq.html">First of type</a></p>
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
               
<p><a href="/pages/support_faq.html">Test and assurance</a></p>
             
<p><a href="/pages/support_faq.html">Testing assets</a></p>

<p><a href="/pages/support_faq.html">Test environments</a></p>

<p><a href="/pages/support_faq.html">Provider testing</a></p>

<p><a href="/pages/support_faq.html">Consumer testing</a></p>

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
                  <p><a href="/pages/support_faq.html">Deploying your system</a></p>
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


