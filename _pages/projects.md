---
layout: page
title: projects
permalink: /projects/
description: Projects by students and faculty of the Pitt Scheduling Group.
---

{% for project in site.projects %}
<h3>
    <a href="{{ project.url | prepend: site.baseurl | prepend: site.url }}">
        {{ project.title }}
    </a>
</h3>
<p>{{ project.description }}</p>
<hr>

{% endfor %}
