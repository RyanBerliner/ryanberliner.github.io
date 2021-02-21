---
title: Home
excerpt: This is my website. 
sitemap:
  changefreq: 'weekly'
---

{% for post in site.posts limit: 1 %}
## {{ post.title }}

{{ post.date | date_to_long_string }}

{{ post.excerpt }}

<a href="{{ post.url }}" aria-label="Continue Reading {{ post.title }}">Continue Reading &raquo;</a>

{% endfor %}

## Other Recent Blog Posts

{% for post in site.posts limit: 4 %}{% if forloop.index > 1 %}
  - [{{ post.title }}]({{ post.url }}) - {{ post.date | date_to_long_string }}{% endif %}{% endfor %}

[View all blog posts &raquo;](/blog/)
