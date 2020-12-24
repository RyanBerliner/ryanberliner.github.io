---
layout: post-2020-12-23-legacy
title:  "Site upgraded to bootstrap."
date:   2017-04-23 22:00:00 -0400
categories: web dev
permalink: /jekyll-site-upgraded-to-bootstrap
comments: true
comments_id: "UWMALGhTMVh7cDKB"
sitemap:
  lastmod: '2017-04-23'
  changefreq: 'never'
---

I was recently introduced to bootstrap, and I want to practice using their classes
a bit. So, I scrapped the default 'minima' theme that jekyll offers, and created
this instead.

As of the time of this writing there are only about 60 lines of scss that I have wrote.
Most of it is just colors and small tweaks here and there. It's crazy how little
you need to do to get a functioning site with bootstrap. That said, I noticed that
the syntax highlighting on the web that came with the minima theme was no longer
going to be available to me. To replace it, I found a site called [highlightjs.org][highlightjs]
which not only provides easy to use syntax highlight, but a bunch of cool themes to choose from.

For example (2 in one here), this is all the code I needed to get a cool syntax highlighting
theme.

{% highlight html %}
<!-- highlight.js -->
<link rel="stylesheet" href="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/styles/darcula.min.css">
<script src="//cdnjs.cloudflare.com/ajax/libs/highlight.js/9.11.0/highlight.min.js"></script>
{% endhighlight %}

The first link to the stylesheet is where you can put the theme you want. They have
alot of really cool ones.

[highlightjs]:   https://highlightjs.org/
