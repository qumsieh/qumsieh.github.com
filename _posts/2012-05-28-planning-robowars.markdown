---
title: RoboWars - Planning the Game
layout: post
category : blog
tags : [android, programming, robowars]
---
In my [previous post](/blog/2012/05/17/robowars-android/), I briefly outlined my plans
to build an Android gamed. In this post, I will give more details about my thought
process.

## Designing for Android #

The concept of the game (programming a robot to compete against other robots) is
not a new one. There are a variety of computer games/simulations that offer a similar
plot (Googling is left as an exercise for the reader). What is different though is the
platform. Programming for Android (or any other touch-screen based OS for that matter)
offers a few challenges that don't exist in the PC world:
* Small Screen
* Touch-based Input
* Limited Memory

### Small Screen #

If you are targeting the PC game market, you can be sure that 99% of your users will
have an 18" screen or larger, with a resolution of at least 1280 x 1080 or so. This
makes it easy to just add another button or widget if you need one (Disclaimer: you
should always follow good UX/UI design principles, but this is a topic for another post).

On a mobile device though, you are usually confined to a screen that is somewhere in
the range of 4" long diagonally. The resolutions can also vary quite widely, especially
with the new devices boasting retina-grade displays. Still, irrespective of the actual
resolution, the "hit points" of the UI should be large enough for finger tapping, which
leads me to the second challenge:

### Touch-based Input #

Tapping a screen with your finger is way less accurate than clicking with a mouse.
In Apple's iOS Human Interface Guideline, Apple advises to give tappable elements at
least a 44px x 44px area for comfortable interaction. Furthermore, you need this
interaction to be simple, intuitive and logical so users don't create unnecessary
usability issues for your user. With these constraints, you need to think differently
and iterate multiple times on your UI design to get it right (at least I do).

### Limited Memory #

In the early days of ubiquitous computing (mid 80s to early 90s), proper memory
management was a corner-stone of good programming. Unfortunately, as Moore's law
offered more RAM at lower prices, this constraint went away. Usually this is a good
thing, but the problem is that most programmers (from the mid 90s onwards) got spoiled
by this luxury and started producing bloated software without any regard to proper
memory management. Now, the explosion of mobile computing, has brought us back to the
olden days where good memory management can make a difference in the overall experience.

***

In the next few posts, I will talk more about the challenges above and how I'm
approaching them. Stay tuned.