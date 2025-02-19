---
title: "Solution Quality vs Simulation Quality"
date: 2025-02-18 20:30:00 -0500
categories: dev random
permalink: /solution-quality-simulation-quality
sitemap:
  lastmod: "2025-02-18"
  changefreq: "never"
---

Your ability to simulate a problem almost always affects how well you solve
that problem. In many cases the best way to improve a solution is to make
simulating the problem easier, quicker, etc.  The solution should naturally
improve afterwards.

I'd go so far as to say that the quality of a solution is **capped** by how
well the problem can be simulated. Consider the following chart.

![A solution quality vs simulation quality chart with a line up and to the
right, showing above the line being impossible and below the line being
possible.](/img/2025-02/solution-vs-simulation.jpeg)

All features, projects, or products lie somewhere on the bottom half of this
chart. A product development team with X simulation capabilities produces a solution of
Y quality. It suggests that sometimes your solution is as good as you can get
it without first creating a better simulator. This invisible upper bound is
everywhere and I would bet that if you spent a day looking you might find that
many solutions are hitting that boundary.

Software people often think about the users or programs happy path. This is the
path that you anticipate a user or program staying in through an expected user
workflow or program execution.

Discussed far less though is the **development** happy path. The
features that are easy for the people building the product to test, the data
they have available to them, the system state they can easily reproduce, and
the parts of problem space that are easiest to explore. The part of the product
with the highest quality is almost always in the development happy path, and
visa versa.

After I thought about this for some time I came across the company antithesis,
particularly [this blog post and the story of
FoundationDB](https://www.antithesis.com/blog/is_something_bugging_you/).  A
couple of quotes from that post about the story of building FoundationDB stuck
out to me.

> ... the part that seemed hardest was how on earth you could test or validate
> such a thing, and how you could gain confidence in its correctness.

> So we did something crazy, which turned out to be the best decision we made
> in the whole history of the company. Before we even started writing the
> database, we first wrote a fully-deterministic event-based network simulation
> that our database could plug into.

This is exactly it. While not all of us work on problems that require
incredibly low level simulation with an explodingly large state space, there is
a lot to learn from the tactic.

In the case of FoundationDB the value proposition is an ACID compliant
distributed database which works under all imaginable failure states
distributed systems are subject to. Building a network simulator was crucial to
align *their* development happy path with *their* value proposition. 

I'll end with a clip of a guy named Bret Victor, giving a talk he called
Inventing on Principle. I recommend you watch the entire video when you have
the time, but for now I'll highlight one section.  [The discussion and
demos from 10:33 to 14:35](https://youtu.be/PUv66718DII&t=633) is exactly what
I'm writing about.  If you want to be able to solve something well, you need to
be able to simulate the problem well. What he shows is an example of this.

There are many problems with mediocore solutions in need of exceptional
simulators.
