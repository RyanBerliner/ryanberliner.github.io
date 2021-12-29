---
title:  "Bike Image Geometry Adjuster (version 0)"
date:   2021-12-28 17:00:00 -0500
categories: dev bike
permalink: /v0-js-bike-geometry
sitemap:
  lastmod: '2021-12-28'
  changefreq: 'never'
---

A couple years ago I started working on a project that would allow adjusting the geometry of bikes in images. No real purpose, just thought it would be interesting. After a couple years of doing nothing on it, I picked it back up and got the proof of concept working.

Here is the proof of concept <strong>(which is very slow fyi)</strong> that has 2 distortions maps and 1 control input. The control input changes the head tube angle while keeping the saddle level. Try changing the value of the slider and watch the image change.

<iframe src="/demo-js-bike-geometry-v0" style="border:none;width:100%;height:100vh;" frameborder="0" id="geo-demo"></iframe>

Not performant, not informative, not nessescarily useful at all by itself, but building this demo answered a few questions and thought out the concepts that will make this work for more bikes and more geometry adjustments in the future. (seat tube angle, reach, bb height, etc)

<h2>How It Works</h2>

There are 2 primary ideas that allow this to work. Distortion maps, and distortion types. Distortion maps are what are painted over the image and say "this is the area of the picture I want to distort". Distortion types take those maps and say "apply this type of distortion to it". I've implenented and prove both a rotational distortion, and translation distortion (x, y, both). However, this demo only utilitizes the rotation distortion type along with 2 distortion maps.

<h3>Distortion Maps</h3>

These are how you tell it what parts of the picture to distort. For example, here is what the distortion maps for the saddle tilt looks like. The map is in red, overlayed on the image.

<img src="/img/2021-12/saddle-distortion-map.png" alt="distrtion map of the saddle" />

You'll see for most of the saddle, the map is solid red. However, for the areas closer the the rails and clamp, it becomes more opaque. This is important. The mor opaque a distortion map is, the less the distortion applied to that map affects that area. This means you get a nice "fade" or "smooth warp" or "stretch" and less like someone just cut of parts of a magizine picture and taped them back together. In the context of the saddle map, it means that the saddle itself rotates 1:1 as it should, and the rails and clamp will "bend" ever so slight to meet up wit hthe seeatpost.

The same principle applies to the head tube disctortion maps. The map is solid red in places where 1:1 distortion should be applied, but faded in to the head tube itself so the welds in the frame and the tubes seem to bend appropriately to line up.

<h4>Drawing Distortion Maps</h4>

This turned out to be one of the trickiest parts, because I needed to support stroke "fading". Under the hood this uses HTML Canvas, which supports lines. However, these lines don't support fading, and certainly don't tell you pixel for pixel what the fade value is. So, I ended up building this from scratch. The text you see under the brush in the video is size/fade/mode.

<video controls autoplay muted loop>
  <source src="/vid/2021-12/brush-fading-demo.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>

I used photoshop a fair bit a long time ago, and recall how nice it was to be able to change brush fade, size, and exclude/include using the keyboard and mouse movements... so I implemented basically the same thing as what I remember. Holding down the command key and moving the mouse around changes size and fade, and hitting "r" changes from additive to subractive (erase).

The thing that made this difficult was the resolution of mouse movements being fairly low. For instance, if you move your mouse quickly, the points that make up your stroke may be very var apart, and you need to "fill in the blanks" between the stroke points. If you didn't do this, you would just see a bunch of spaced out circles where easy mouse location was recorded.

<h3>Distortion Types</h3>

Once the areas to distort have been defined with distortion maps, its time to apply distortions to them. Initially I've implemented both rotational distortions around an origin, and translational distortions in x and y directions. These distortions can be layer on top of each other if nessescary. Here is what these look like on a square area, with faded distortion maps to "easy in" "stretch" or "bend" the edges.

This first one is an example of rotation disotrtion.

<video controls autoplay muted loop>
  <source src="/vid/2021-12/rotation-example.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>

This is x and y distortion

<video controls autoplay muted loop>
  <source src="/vid/2021-12/translation-example.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>

Finally, this is multiple distortions being applied to the same area. I've hard coded 2 for this example but you could have more.

<video controls autoplay muted loop>
  <source src="/vid/2021-12/both-example.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>

<h3>Applied to a Bike</h3>

Technically, that's all that's needed to distort a picture of a bike to changes its geometry. You can create the distortion maps, and the apply the correct distortions. To figure out what distortions you need to apply, you need to collect some information about the image. Things like head tube, axles, etc. These allow you to place your origins of rotations in the correct sports. In addition, with this imporation you can also calculate how angles and distances between points changes. Here is a look under the covers at how the distortion types are calculated based on the points of interest on the bike. This is only changing the head tub angle.

<video controls autoplay muted loop>
  <source src="/vid/2021-12/geo-overlay.mov" type="video/mp4">
  Your browser does not support the video tag.
</video>

This example video fails to correctly show how change of head tube effects other parts of the geometry, but it illustates the points of interest recorded on the bike that allow these calculations to occur.

In the context of the <a href="#geo-demo">demo at the top of the page,</a> the saddle distortion type knows how much to rotate based on how much the head tube change tilts the bike forward. It's a lot of trigonometry and figuring out how a change to one angle affects the other angles, and lengths. This can be extended to other parts of the bike to like seat tube, reach, etc.

<h2>Improvements & Ideas</h2>

For any next version there are a couple obvious things to deal with.

<ol>
  <li>An interface to add any number of distortion map/type layers on top of each other. Right now the 2 are hardcoded. This leads into #2</li>
  <li>More geometry adjustments. Seat tube angle, reach, chainstay length, etc</li>
  <li>Some sort of read out of geometry numbers after adjustments.</li>
  <li>An optomized "animation" mode that pre-calculates each bit of a specific adjustment and lets you smoothly slide between the two in real time. Right now its all calculated  on demand and is slow beacuse of it. Likely this would be a bunch of pre-computed image tags.</li>
  <li>I wrote the initial interface for this 3 years ago in react. I think I was just starting to learn about react then, and wanted to practice... otherwise there is no good reason to use it here. Its a bit of a PITA for something like this because you are working directly with dom elements. I would probably want to drop react out of this.</li>
</ol>

There is also a far out thought that somehow you could technically train a model to accurately mark points of interest on the bike, and draw the distortion maps for you. This means you could just upload an image and BOOM start adjusting the geometry instantly. Would need to label a bunch of bikes by hand first to get some training data.

<h3>Ideas</h3>

While this is all mostly doesn't have a purpose, I do think it would be cool to have a website that walks through the evolution of different bike models. Imagine scrolling a webpage and seeing a 2010 trek session, then scrolling down a bit more and seeing the image start animating with the head tube slacking out then BOOM 2011 trek session... then scroll down more and see the geo animating slightly again and BOOM 2012 and so on. You could have an animated timeline of different bikes by model, or industry average, or popularity. Certainly far off but currently the only semi-useful thing I can imagine being done with this.

<script>
  const iframe = document.getElementById('geo-demo');
  iframe.addEventListener('load', function() {
    iframe.style.height = `${iframe.contentDocument.body.scrollHeight}px`;
    iframe.style.width = `${iframe.contentDocument.body.scrollWidth}px`;
  });
</script>

