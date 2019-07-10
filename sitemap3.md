---
title: Sitemap
tags: [sitemap]
keywords: sitemap
permalink: sitemap3.html
sidebar:home_sidebar
toc: false
---


<div id="grid" class="row">


    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["getting_started"]'>

               <div class="panel panel-default">
               <div class="panel-heading">Getting started</div>
               <div class="panel-body">
                  If you're getting started with Jekyll, see the links in this section. It will take you from the beginning level to comfortable. 
                  <ul>
                {% for page in site.pages %}
                {% for tag in page.tags %}
                {% if tag == "getting_started" %}
                  <li><a href="{{page.url | remove: '/'}}">{{page.title}}</a></li>
                {% endif %}
                {% endfor %}
                {% endfor %} 
                  </ul>
               </div>
            </div>
    
    </div>
   

    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["content-types"]'>

        <div class="panel panel-default">
            <div class="panel-heading">Content types</div>
            <div class="panel-body">
                This section lists different content types and how to work with them.
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



    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["formatting"]'>

                <div class="panel panel-default">
               <div class="panel-heading">Formatting</div>
               <div class="panel-body">
                  These topics get into formatting syntax, such as images and tables, that you'll use on each of your pages: 
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

    <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["single_sourcing"]'>
         
      <div class="panel panel-default">
               <div class="panel-heading">Single Sourcing</div>
               <div class="panel-body">These topics cover strategies for single_sourcing. Single sourcing refers to strategies for re-using the same source in different outputs for different audiences or purposes.
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

       <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["publishing"]'>

           <div class="panel panel-default">
               <div class="panel-heading">Publishing</div>
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

        <div class="col-xs-6 col-sm-4 col-md-4" data-groups='["special_layouts"]'>

             <div class="panel panel-default">
               <div class="panel-heading">Special Layouts</div>
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


    </div><!-- /#grid -->

{% unless site.output == "pdf" %}
{% include initialize_shuffle.html %}
{% endunless %}

{{site.data.alerts.note}} This was mostly an experiment to see if I could break away from the hierarchical TOC and provide a different way of arranging the content. However, this layout is somewhat problematic because it doesn't allow you to browse other navigation options on the side while viewing a topic.{{site.data.alerts.end}}

