---
layout: default
published: false
---

# Evolutionary Image Replication using Perl

A few days ago, someone on [HackerNews](http://news.ycombinator.com/item?id=4912964) linked to [Roger Alsing's "Evolution of Mona Lisa"](http://rogeralsing.com/2008/12/07/genetic-programming-evolution-of-mona-lisa/) post. In it, Roger describes how he wrote a program that painted a replica of the Mona Lisa using only 50 semi transparent polygons.

I've always found evolutionary algorithms to be very intriguing. A few years ago, I wrote [AI::Genetic](http://search.cpan.org/~aqumsieh/AI-Genetic-0.05/) which is pure Perl implementation of Genetic Algorithms. Since I'm always looking for an excuse to play with it, I decided to write my own implementation of Roger's program. Although Roger [released his source code](http://rogeralsing.com/2008/12/11/genetic-programming-mona-lisa-source-code-and-binaries/), I did not look at it and proceeded to write everything from scratch.

The algorithm is really simple, and boils down to this:

    create initial population of randomly generated solutions
    for a set number of iterations {
        combine and mutate solutions based on their ranks
        construct an image from each solution
        rank each solution based on how similar it is to target image
        take a snapshot of best solution so far
    }