---
title: Home
excerpt: This is my website. 
sitemap:
  changefreq: 'weekly'
---

This is my website.

{% for post in site.posts limit: 1 %}
## Latest Blog Post — {{ post.title }}

{{ post.date | date_to_long_string }}

{{ post.excerpt }}

[Continue Reading {{ post.title }}]({{ post.url }})

{% endfor %}

## Other Recent Blog Posts

{% for post in site.posts limit: 3 %}
  - [{{ post.title }}]({{ post.url }}) - {{ post.date | date_to_long_string }}{% endfor %}

[*View all blog posts*](/blog/)