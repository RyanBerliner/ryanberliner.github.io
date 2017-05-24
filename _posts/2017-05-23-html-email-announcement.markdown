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

(next day, another 2 hours) NOPE. Not the fix. I literally tried everything, casting things
to strings, swapping p tags for breaks, piecing out my inline styling as much as possible,
and it was still unpredictably messed up. THEN I FOUND IT. As this piece of gold on stack overflow
explains, the mail function for some reason adds a space every 900 or so characters (which is why it was random because each email was different).

The fix then became adding `\r\n` to then of EVERY single line of my html email to be safe. It appears this is
the actually problem and actually solution. I knew my styles were breaking because of spaces (for instance if I inspected the email in chrome it
  would look like `border-bottom: so lid 1px #efefef;`), but couldn't figure out why. This is why. By why? Why add a new
  space every 900 characters?
