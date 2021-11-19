---
title:  "Gmade r1 crab walk mod"
date:   2021-11-18 22:00:00 -0500
categories: dev rc
permalink: /gmade-r1-crab-walk-mod-servo-reversing
sitemap:
  lastmod: '2021-11-18'
  changefreq: 'never'
---

Remote control crawlers (like the gmade r1 I'm using in this project) sometimes offer 4 wheel steering. From what I could find, there is no way to toggle between standard 4 wheel steering, and crab walk steering. Basically... how do you create a toggle to reverse servo direction of just the rear steering? Thats what this does. It uses the switch on a standard traxxas controller to toggle between standard and crab walk.

<div class="youtube-16-9">
  <iframe src="https://www.youtube-nocookie.com/embed/_udrgzlhfoo" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" title="crab walking rc car video" allowfullscreen></iframe>
</div>

[View the code on github](https://github.com/RyanBerliner/rc-car-controller/) or read on to see more about the hardware involved. I'll start off by saying I know next to nothing about electricity. My solution is also completely impractical in its current form for actual rc crawling.

The crux of this problem is reversing a servo with a switch. I'm using the thumb switch on [this traxxas remote control.](https://traxxas.com/products/parts/transmitters/6507Rtqitraxxaslink4ch) Typical servos like the ones in rc cars are controled use a signal which rapidly turns on, and off, called PWM (pulse width modulaltion). The longer the signal is "on" the wider the pulse width, the shorter the signal is on, the shorter the pulse width. When servos receive a specific pulse width, they move to a specific position. For example, lets say a pulse thats on 20% of the time may have the servo at a 10 degree angle, and when the pulse is on 80% of the time, its rotated all the way to 60 percent. These are just made up numbers... but they illustrate how servos like this work. This PWM signal is typically the white cable, while red and black are there usual positive and negative.

<figure>
  <img src="/img/2021-11/receiver-cables.jpg" alt="an rc car reciever with a bunch of cables coming out of it" />
  <figcaption>The receiver has 4 channels. 1 has its PWM (white) signal affected by throttle, one by the thumb switch, and 2 (identically) by the steering.</figcaption>
</figure>

Since 2 of the channels have identical PWM signals affected by the steering, the issue became making them different... or "opposite". But whats opposite of a 20% PWM signal? 80%? Not always... its dependent on other factors like the "center" "max" and "min" ranges of the servo, what their [duty cycle range is.](https://en.wikipedia.org/wiki/Duty_cycle) To take all these considerations into account I decided I'd take the route of reading the signal on the receiver (on the car) and then conditionally "reversing" it.

The only hardware I had to work with was a rasperry pi, a breadboard and some wires to testing things without soldering. This is stuff left over from a [github integrated desk led setup](/desk-led-github-integration-raspberry-pi) I built a couple years ago. I struggled to "read" the signal for processing on the pi... there gotta be some piece of hardware that would allow me to get a high quality and accurate signal... I still want to figure that out but for now I just used [a software hack of detecting "on" and "off" signals](https://forums.raspberrypi.com/viewtopic.php?t=48592) and estimating a pulse width from that. You can actually see the volitility of that estimation in the video. Occasionally you'll see the back wheels wiggle a little bit.

<figure>
  <img src="/img/2021-11/pi-servo-passthrough.jpg" alt="a raspberry pi and breadboard with cables all over the place" />
  <figcaption>You'll see the white + grey being the "reading" of the stearing signal, then outputting an adjusted signal in the yellow cable to the servo. The white + purple is "reading" the thumb switch signal. The power for the servo is passed through the breadboard too. Why the breadboard? I didn't have the right cables.</figcaption>
</figure>

As pictured I also read the thumb switch signal into the pi too so the output signal to the servo could be conditionally reversed. It's incredibly inneficient to try parsing the PWM signal the software hack way (go figure)... so I only sampled the thumb switch once every second. You can see the side effect of this in the video - after hitting the thumb switch it takes a second for the wheels to reverse. Another reason I gotta figure out the correct (probably hardware?) way to read the signals.

Its rough, but it works. The last bit was unplugging the pi from the outlet to mount it on the car. Luckily, the pi operates off of 5v, which the receiver on the car ouputs to each of its channels. Very convenient. I was able to cut a power cable and splice it onto some servo plugs. Works well enough... no smoke, and no low voltage warnings. Taped everthing to the car and voila.

<img src="/img/2021-11/gmade-r1-mod.jpg" alt="a gmade r1 with a raspberry pi and cables tabled to it" />

If you've got any info about how to properly read PWM signals into a pi... let me know. Or if there is some obvious hardware solution to reverse a signal like this and remove the need for software all together, even better.
