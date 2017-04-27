---
layout: post
title:  "I figured out how to add Images"
date:   2017-04-26 21:20:00 -0400
categories: random web dev
permalink: /image-with-jekyll
featured-image: /img/2017-04/sunset-high-up.jpg
type: featured
---

This website was looking really boring, so I thought this would be a good time
for me to figure out images. Well, not the image part, the how to organize and
access them in jekyll's file organization.

I decided the best route was just to make an `img` directory at the root of my
repo and I could implement my own organizational system from there. In order to
access the pictures in posts and through out the side I will just need to prefix
the path path with `{ site.baseurl }`. To my knowledge this gets the correct number
of `../` to the root of the site.

The entire reason I wanted to figure this out was to make the front page look less
boring. My thought was that some posts would have images to show with them. My next
problem here would be how to know if the post had an image to show, and where to
get it. I was going to do something with the excerpt and custom delimeter, but then
found a much better solution by adding another 'field' (i think it'd be called) to
the post header. For instance, here is what the header of this post looks like.

{% highlight markdown %}
layout: post
title:  "I figured out how to add Images"
date:   2017-04-26 21:20:00 -0400
categories: random web dev
permalink: /image-with-jekyll
featured-image: /img/2017-04/boltonryan2.jpg
type: featured
{% endhighlight %}

By adding the `featured-image` field I can then make a check when printing out post
as to whether or not to show and image. Here's whats that looks like.

{% highlight markdown %}
if post.featured-image and post.featured-image != ""
  // Print out the version with the image
else
  // Print out the version without the image
endif
{% endhighlight %}

As a bonus I also wanted to be able to print out a post with emphasis, so there is
a `type: featured`. Again, I just need to check if that's there, and if it is
I will print out the featured version. As the time of this writing that just makes
the post wider.
