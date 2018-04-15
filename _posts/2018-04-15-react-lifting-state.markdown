---
layout: post
title:  "Learning React - Lifting State"
date:   2018-04-15 10:00:00 -0400
categories: web dev
permalink: /learning-react-js-lifting-state
comments: true
comments_id: "UWMALGhTADFDEEWVh7cDKB"
sitemap:
  lastmod: '2018-04-15'
  changefreq: 'never'
---

The more things I build the more work-aroundy solutions I end up building out in
javascript, mostly using jQuery to make things go quicker. Becuase of this it is
making it look like learning [React JS][reactjs] is a good idea. So, in effort to allow
me to build cooler things quicker and more sustainably I've started learning React.

I've read through the quickstart docs and decided that I would give lifting state a
go. This is something I wanted to do because at first I always want to put all the
data in the state of the outermost container... which may not always be the best thing.
Also, updating parent state from child input is really important.

I built a really quick demo of 'Thoughts', that have a like button. You can click the
like for each one and it increments the like, also updating the progress bar towards
the arbitrary goal of 100 likes. There is also a simulation built in that will
randomly add likes to 'Thoughts' so you can just watch it go.  You can [check out the demo here][demo].

You can [checkout the code here][github], if you see anything really odd let me know.

[reactjs]:   https://reactjs.org/
[demo]:   /demo/reactjs-demo1/
[github]:   https://github.com/RyanBerliner/React-Lifting-State
