---
title: "A Good MTB Coil Calculator"
date: 2025-02-23 17:30:00 -0500
categories: dev bike
permalink: /best-mtb-coil-calculator
sitemap:
  lastmod: "2025-02-23"
  changefreq: "never"
---

This is a post about the [mtb coil calculator I
built](https://ryanberliner.com/coil-calculator/). Why I built it, and what it
does differently to existing calculators. I originally built it some years
back, and then a few months ago I added some more features to it. It's still
not showing up on any search engines or anything but if it does one day here is
an explanation of the tool for those interested.

When it comes to rear suspension on a mountain bike you have 2 options.

1. An air sprung shock
2. A coil shock

The first is dead simple... sure, there are some options to pick from, but you
choose something that fits your budget (and your bike) and maybe your favorite
color. When it arrives you can install it and set it up. Cake.

Where things get a little more complicated is the second option: A coil shock.
Unlike an air shock you actually gotta know a thing or 2 before you hit buy.
Yes, you need to know the specs of your bike, but you also need to know **the
correct spring rate** to choose. And you also need to know **your bikes
suspension platform**. And you also need to know **who is going to be riding
the bike**.

If you don't have a buddy or a friendly bike shop with an inventory of demos
your gonna be ordering new coils until you find the right one. There is no
setup step that can make the wrong coil right. Air shocks are infinitely
adjustable, coil shocks cannot be adjusted at all.

<details>
<summary>Why can't you use the preload adjuster?</summary>
<p>

Well, yeah, preload is an adjustment you can use. However, you need to
understand what preload actually does. When you add preload to your coil shock
you're increasing the <strong>initial</strong> force required to compress the
suspension. 

</p>
<p>

A coil shock with no preload is supple and responsive to miniscule amounts of
force, whereas a preloaded coil will sit you higher in the suspension with less
sensitivity. The rate, however, does not change. A coil that's heavily
preloaded out of necessity will have poor small bump compliance and will be
prone to bottom outs frequently.

</p>
<p>

<strong>A simplified example with math, ignoring leverage ratios, coil length,
weight distribution, etc.</strong> 

</p>
<p>

Lets say you you weigh 200lbs, and you've installed a 100lb/in coil
(unrealistic for many reasons, but easy math).  With no preload you sag the
suspension 2 inches. If you've only got 2 inches of suspension (lets assume you
do) then thats 100% sag. You bottom out the shock just by sitting on the damn
thing. An obvious sign you have the wrong coil.

</p>
<p>

But, you think to yourself "I'll just use that preload adjuster".  So you crank
the preload until you acheive a 25% sag. "Perfect" you think. You head out to
the driveway and do a couple bounce tests, only to realize that you still
bottom out the shock by bouncing up and down on the bike.

</p>
<p>

This is because the coil still compresses 1 inch for every 100lbs of force
added, and as a 200lb person, it is trivial to apply an additional 100lbs of
force. Meanwhile, a 50lb person, who this coil is actually intended for, would
struggle to apply 100lbs of force without hitting a big drop or doing something
extreme. You've bought a childrens coil, and there is nothing you can do about
it.

</p>
<p>

Preload should be looked at as a way to tune the ride characteristics of the
bike & shock, not to make a sag measurement acceptable. A preload adjuster will
not save you from the wrong coil.

</p>
</details>

Typically what you'll do is a quick web search for "mtb coil calculator" to try
figuring out what coil you need. You'll either land on some page with 1 or 2
inputs that makes you question how (or if) it actually works, or you'll find
the fox calculator with its 30 different form inputs, assume its black magic
industry secrets and blindy trust the output as the only acceptable answer.

What's missing is a calculator that lets you **test** a few spring rates for
your exact bike while giving you an intuition for what goes into picking a coil
in the first place. With intuition comes perspective and the confidence you can
only get from knowing what you're doing.

This is what the [mtb coil calculator I
built](https://ryanberliner.com/coil-calculator/) is supposed to do. Like the
others, it's still a theoretical approximation and is never going to be a
perfect predictor of reality. However, I think it's much better than the
alternative calculators available for a few reasons.

- **The calcuation produces a sag value, not a theoretical perfect coil.** By
  outputting sag instead of coil rate the user can play around with a few
  different coils and see how it does (or doesn't really) affect the sag.  Most
  calculators output a coil value like its the only one that'll work, and users
  don't realize how little affect on sag different coil rates may have.
- **Actual leverage ratio curves.** Some calculators ask for suspension
  platform ("single pivot" "4 bar" etc) as if they can assume a leverage curve
  from that. They cannot. Others ask for a static number, which is equally
  ridiculous. With the fully customizable leverage curve in this calculator you
  can **truthfully** match your bikes suspension kinematics.
- **It updates the sag in realtime.** This is particularly helpful in building
  an intuition around how leverage curves affect sag. Just drag the curve
  around and the sag will change with it. Most people say things like
  "progressive suspension platform" but don't actually understand what it means
  or what it affects.
- **A shock to test out (on desktop).** Admittedly this one is kinda a gimick.
  I mostly just wanted to draw a shock. But, it is a physically accurate
  simulation and helps ground what you're doing into a recognizable reality. 

Ultimately, it's still just a calculator, but its a bit different than the
others. I have some ideas to make it better too (a huck to flag metric for
conveying bottom out force, a database of bike leverage curves, visualization
of sag point on leverage curve, a rider weight vs coil rate chart, etc) but am
not sure when or if I'll get to those.  Give it try if you're interested, your
milage may vary.

If you like math or code go [tear it apart on
GitHub.](https://github.com/RyanBerliner/coil-calculator/) Factoring a fully
customizable leverage curve in to the calculation was particularly challenging
for me.
