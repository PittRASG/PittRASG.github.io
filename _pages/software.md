---
layout: page
title: software
permalink: /software/
description: Open-source software tools developed by members of Pitt RASG.
---

{% for software in site.software %}
<div class="project ">
    <div class="thumbnail">
        <a href="{{ software.url | prepend: site.baseurl | prepend: site.url }}">
        {% if software.img %}
        <img class="thumbnail" src="{{ software.img | prepend: site.baseurl | prepend: site.url }}"/>
        {% else %}
        <div class="thumbnail"></div>
        {% endif %}
        <span>
            <h1>{{ software.title }}</h1>
            <hr class="smallmargin"/>
            <p>{{ software.description }}</p>
        </span>
        </a>
    </div>
</div>
{% endfor %}
