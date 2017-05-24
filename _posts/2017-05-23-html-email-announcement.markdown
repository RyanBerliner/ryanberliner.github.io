---
layout: post
title:  "HTML Email Announcement."
date:   2017-05-23 10:00:00 -0400
categories: web dev
permalink: /html-email-announcment
sitemap:
  lastmod: '2017-05-23'
  changefreq: 'never'
---

After wrestling with an html email bug for 3+ hours today, I think I have found
the cause. Some of the inline styling and formatting was sending really inconsistantly
and I wasn't sure why.

I swapped all `<br>` tags for `<br />`. That seems to be the fix.
