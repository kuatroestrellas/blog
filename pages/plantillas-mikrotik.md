---
layout: page
title: Plantillas Mikrotik
permalink: "/plantillas-mikrotik/"
#image: assets/images/screenshot.png
---

Proximamente más plantillas
<h4 class="mt-5 mb-4 pb-2 border-bottom" id="{{ category[0] | replace: " ","-" }}"><span class="text-capitalize small font-weight-bold">Plantilla Gamer led RGB</span></h4>
<div class="row">

<div class="col-md-4 mb-5">
    <div class="card">
        <a href="{{ post.url | absolute_url }}">
            {% if post.image %} <img class="rounded mb-4" src="{{ site.baseurl }}/{{ post.image }}" alt="{{ post.title }}"> {% endif %}
        </a>
        <div class="card-block">
            <h2 class="card-title h4 serif-font"><a href="{{ post.url | absolute_url }}">plantilla 1</a></h2>
            <script src="https://www.mercadopago.com.mx/integrations/v1/web-payment-checkout.js"
                data-preference-id="301152529-b8f9b5fa-b854-4902-b183-816b36e58181" data-source="button">
            </script>


            <p class="card-text text-muted">{{ post.excerpt | strip_html | truncatewords:15 }}</p>
            <div class="metafooter">
                <div class="wrapfooter small d-flex align-items-center">
                    <span class="author-meta">
                    By  <span class="post-name"> {% if post.author %}{{ author.display_name }}{% else %}{{ site.author }}{% endif %}, </span>             
                    on <span class="post-date">{{ post.date | date_to_string }}</span>
                    </span>               
                    <div class="clearfix"></div>
                </div>
            </div>
        </div>
    </div>
</div>

<!--
<div class="col-md-4 mb-5">
    <div class="card">
        <a href="{{ post.url | absolute_url }}">
            {% if post.image %} <img class="rounded mb-4" src="{{ site.baseurl }}/{{ post.image }}" alt="{{ post.title }}"> {% endif %}
        </a>
        <div class="card-block">
            <h2 class="card-title h4 serif-font"><a href="{{ post.url | absolute_url }}">plantilla 2</a></h2>
            <p class="card-text text-muted">{{ post.excerpt | strip_html | truncatewords:15 }}</p>
            <div class="metafooter">
                <div class="wrapfooter small d-flex align-items-center">
                    <span class="author-meta">
                    By  <span class="post-name"> {% if post.author %}{{ author.display_name }}{% else %}{{ site.author }}{% endif %}, </span>             
                    on <span class="post-date">{{ post.date | date_to_string }}</span>
                    </span>               
                    <div class="clearfix"></div>
                </div>
            </div>
        </div>
    </div>
</div>

<div class="col-md-4 mb-5">
    <div class="card">
        <a href="{{ post.url | absolute_url }}">
            {% if post.image %} <img class="rounded mb-4" src="{{ site.baseurl }}/{{ post.image }}" alt="{{ post.title }}"> {% endif %}
        </a>
        <div class="card-block">
            <h2 class="card-title h4 serif-font"><a href="{{ post.url | absolute_url }}">plantilla 3</a></h2>
            <p class="card-text text-muted">{{ post.excerpt | strip_html | truncatewords:15 }}</p>
            <div class="metafooter">
                <div class="wrapfooter small d-flex align-items-center">
                    <span class="author-meta">
                    By  <span class="post-name"> {% if post.author %}{{ author.display_name }}{% else %}{{ site.author }}{% endif %}, </span>             
                    on <span class="post-date">{{ post.date | date_to_string }}</span>
                    </span>               
                    <div class="clearfix"></div>
                </div>
            </div>
        </div>
    </div>
</div>
-->

</div>
