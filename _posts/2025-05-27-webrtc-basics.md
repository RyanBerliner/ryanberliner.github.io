---
title: "The Basics of WebRTC, Explaining the Jargon"
date: 2025-06-06 19:18:00 -0400
categories: dev
permalink: /webrtc-basics-explaining-jargon
sitemap:
  lastmod: "2025-06-06"
  changefreq: "never"
---

I've been prototyping a project at work involving WebRTC. I found the
vocabulary to be a distraction that prevented me from quickly understanding the
basics. This brief post is how I would have liked to been introduced to WebRTC
and it's corresponding jargon.

We'll start with the plain english example of how Joe and Mike would set up a
video call with each other using WebRTC, which is a common use case of the
technology. This example is the basis of this post.  On desktop it will be
interactively referenced and pinned to the top of the page.

<p class="mobile-only">
  <strong>You seem to be viewing this on small screen, its recommended it view
  on a desktop for the interactive experience.</strong>
</p>

<style>
  [data-type="example"] {
    background: var(--lightgrey);
    padding: var(--spacer);
    margin-bottom: var(--spacer);
  }

  @media screen and (min-width: 500px) {
    [data-type="example"] {
      position: sticky;
      top: 0;
    }
  }

  [data-type="example"] > p:last-child {
    margin-bottom: 0;
  }

  [data-type="example"] .highlight {
    outline: 3px solid red;
  }

  @media screen and (min-width: 500px) {
    [data-highlight] {
      text-decoration: underline;
      text-underline-offset: 0.17em;
      text-decoration-style: dotted;
      cursor: help;
    }
  }
</style>

<!-- start sticky container... we only want a portion of the article -->
<div>

<div data-type="example">
  <div data-type="negotiation">
    <p>
      <strong data-type="peer">Joe:</strong> <span data-type="offer">My name is
      Joe, I'd like to start a video call</span> <span
      data-type="send-offer">with you, Mike</span>
    </p>

    <p>
      <strong data-type="peer">Mike:</strong> <span
      data-type="accept-offer">OK.</span> <span data-type="answer">My name is
      Mike</span> and <span data-type="ice-1">here are some ways you can connect
      with me directly,</span> <span data-type="send-answer-ice">Joe.</span>
    </p>

    <p>
      <strong data-type="peer">Joe:</strong> <span
      data-type="accept-answer-ice">Excellent,</span> <span
      data-type="ice-2">here is how you can connect with me directly,</span>
      <span data-type="send-ice">Mike</span>
    </p>

    <p>
      <strong data-type="peer">Mike:</strong> <span
      data-type="accept-ice">OK.</span>
    </p>
  </div>

  <p data-type="streaming">
    Now that Joe and Mike have exchanged their information, they'll be able to
    see and hear each other on a video call.
  </p>
</div>

<script>
  const example = document.body.querySelector('[data-type="example"]');

  document.body.addEventListener('mouseover', function(event) {
    const highlight = event.target.getAttribute('data-highlight');

    example.querySelectorAll('[data-type]').forEach(el => {
      el.classList.remove('highlight');
    });

    if (!highlight) {
      return;
    }

    example.querySelectorAll(`[data-type="${highlight}"]`).forEach(el => {
      el.classList.add('highlight');
    });
  });
</script>

<p>
  The dialog between Joe and Mike prior to <span data-highlight="streaming">the
  video call itself</span> is called a <span
  data-highlight="negotiation">negotiation.</span> Each <span
  data-highlight="peer">peer</span> must configure their own peer connection to
  be able stream video and audio directly with each other.
</p>

<blockquote class="mobile-only">
  <p>
    My name is Joe, I'd like to start a video call
  </p>
</blockquote>

<p>
  Joe <span data-highlight="offer">creates an offer</span> that he saves in his
  peer connection configuration.
</p>

<blockquote class="mobile-only">
  <p>
    with you, Mike
  </p>
</blockquote>

<p>
  He <span data-highlight="send-offer">sends this offer to Mike.</span>
</p>

<blockquote class="mobile-only">
  <p>
    OK
  </p>
</blockquote>

<p>
  Mike <span data-highlight="accept-offer">accepts Joe's offer</span> and saves
  it in his peer connection configuration.
</p>

<blockquote class="mobile-only">
  <p>
    My name is Mike and here are some ways you can connect with me directly
  </p>
</blockquote>

<p>
  Mike <span data-highlight="answer">creates an answer</span> to the offer he
  received from Joe. He saves it in his peer connection details.  He also
  figures out a few ways that Joe might connect with him directly. These are
  <span data-highlight="ice-1">Mike's ice candidates.</span>
</p>

<blockquote class="mobile-only">
  <p>
    Joe
  </p>
</blockquote>

<p>
  Mike <span data-highlight="send-answer-ice">sends his answer and his ice
  candidates to Joe.</span>
</p>

<blockquote class="mobile-only">
  <p>
    Excellent
  </p>
</blockquote>

<p>
  Joe <span data-highlight="accept-answer-ice">saves Mikes answer and ice
  candidates</span> in his own peer connection configuration.
</p>

<blockquote class="mobile-only">
  <p>
    here is how you can connect with me directly
  </p>
</blockquote>

<p>
  Joe <span data-highlight="ice-2">generates his ice candidates</span> that
  explain how Mike might connect with him directly.
</p>

<blockquote class="mobile-only">
  <p>
    Mike
  </p>
</blockquote>

<p>
  Joe <span data-highlight="send-ice">sends his ice candidates to Mike.</span>
</p>

<blockquote class="mobile-only">
  <p>
    OK
  </p>
</blockquote>

<p>
  Mike <span data-highlight="accept-ice">saves Joe's ice candidates</span> to his
  own peer connection configuration.
</p>

<p>
  At this point both Joe and Mike have each others ice candidates, which they
  should have saved to their respective peer connection configurations. This
  allows <span data-highlight="streaming">peer to peer streaming of video,
  audio, or arbitrary data directly to each other</span> to begin.
</p>

</div>
<!-- end stick container -->

## Questions you likely have

### How is this negotiation happening?

If the negotiation is required to set up direct lines of connections, how are
Joe and Mike communicating prior to those direct lines existing?

Most documentation states that negotiation can happen "however you'd like".
I'll provide some examples to put it plainly.

- Joe and Mike could meet up at the park and exchange information on sticky
  notes
- Call each other on the phone with a pen and paper ready
- They could communicate via email

...or **maybe** as the developer of the video chat app, you set up a server
for them to communicate in realtime with each other.

The information sharing that occurs outside of the direct WebRTC peer to peer
connection is called
[signalling.](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API/Signaling_and_video_calling)
Sometimes people will refer to the negotiation process itself as signalling
too.  It's common practice to set up a signalling **server** in which peers can
signal to each other. Picture a simple websocket server, for example.

Know though that **setting up a server is NOT required in the base case.** My
first "hello world" demo was simply me calling myself in another browser. For
this demo, I copy and pasted messages to each browser using `prompt()` and
`alert()`. Feeling the mechanics of the negotiation was important to me.
Setting up automatic signaling was, once again, another distraction.

In some other "hello world" demos you'll see folks use [Broadcast
Channels](https://developer.mozilla.org/en-US/docs/Web/API/BroadcastChannel) as
their simple signalling mechanism. Anything goes, really, but in production for
your typical call-type apps you're most likely going to see a websocket
signalling server.

### Whats the point of WebRTC if I still need a server?

If you have to provide Joe and Mike realtime communication for signaling, why
use WebRTC at all? **Because of the benefits of direct, peer to peer
communication.**

- Low latency. If Joe and Mike in are in the next town over why bother passing
  through your datacenter in Virginia? With a peer to peer communication they
  theoretically take the shortest route to reach each other.
- Low (no) bandwidth. Video and audio data is large. Not footing the bill for
  that bandwidth means cost savings.
- Its a developed standard. WebRTC is [built into all modern browsers
  now.](https://caniuse.com/?search=webrtc) This means by using it you get
  universal compatability for free (without having to understand all the
  different edge cases yourself).
- ...and more


## Going beyond the basics

With this baseline knowledge, I've found the rest of the documentation (and
even the jargon) online to be excellent. Everything I've run into since forming
this understanding has been fairly clear.

If you're a WebRTC pro and have corrections or suggestions to any of the above,
please reach out and I'll be sure to update the post to be accurate as possible.
