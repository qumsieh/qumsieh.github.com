---
published: true
title: Evolutionary Image Replication Using Perl
layout: post
category : blog
tags : [perl, programming, Genetic Algorithms]
---

A few days ago, someone on [HackerNews](http://news.ycombinator.com/item?id=4912964) linked to [Roger Alsing's "Evolution of Mona Lisa"](http://rogeralsing.com/2008/12/07/genetic-programming-evolution-of-mona-lisa/) post. In it, Roger describes how he wrote a program that painted a replica of the Mona Lisa using only 50 semi transparent polygons.

I've always found evolutionary algorithms to be very intriguing. A few years ago, I wrote [AI::Genetic](http://search.cpan.org/~aqumsieh/AI-Genetic-0.05/) which is pure Perl implementation of Genetic Algorithms. Since I'm always looking for an excuse to play with it, I decided to write my own implementation of Roger's program. Although Roger [released his source code](http://rogeralsing.com/2008/12/11/genetic-programming-mona-lisa-source-code-and-binaries/), I did not look at it and proceeded to write everything from scratch. I was surprised at how easy it turned out to be.

## Prerequisites

* A sufficiently recent Perl installation
* [AI::Genetic](http://search.cpan.org/~aqumsieh/AI-Genetic-0.05/)
* [GD](http://search.cpan.org/~lds/GD-2.46/GD.pm)

## The algorithm

The algorithm is really simple, and boils down to this:

    create initial population of randomly generated solutions
    for a set number of iterations {
        combine and mutate solutions based on their ranks
        construct an image from each solution
        rank each solution based on how similar it is to target image
        take a snapshot of best solution so far
    }

For my polygons, I opted to use simple triangles to simplify my code. All triangles had an alpha value of 50%. Each individual solution was made up of 50 triangles. Each triangle was encoded using 9 "genes":

    x1     the x-coordinate of the first triangle vertex (from 0 to IMG_WIDTH - 1)
    y1     the y-coordinate of the first triangle vertex (from 0 to IMG_HEIGHT - 1)
    x2     the x-coordinate of the second triangle vertex (from 0 to IMG_WIDTH - 1)
    y2     the y-coordinate of the second triangle vertex (from 0 to IMG_HEIGHT - 1)
    x3     the x-coordinate of the third triangle vertex (from 0 to IMG_WIDTH - 1)
    y3     the y-coordinate of the third triangle vertex (from 0 to IMG_HEIGHT - 1)
    r      the Red component of the color of the triangle (from 0 to 255)
    g      the Green component of the color of the triangle (from 0 to 255)
    b      the Blue component of the color of the triangle (from 0 to 255)

So, each solution consisted of (50 x 9) = 450 genes (the alpha was fixed).

In order to rank each solution, I needed to plot it onto a canvas. For that, I used GD to create one GD::Image object per solution, iterated through each of the triangles and drew it. Then, I compared the resulting image of each solution to the reference image. The comparison was done pixel by pixel:

    diff = 0
    for x (0 to IMG_WIDTH - 1) {
        for y (0 to IMG_HEIGHT - 1) {
            ref_color = color of pixel(x, y) in reference img
            sol_color = color of pixel(x, y)
            
            d_red   = ref_color_red_component   - sol_color_red_component
            d_green = ref_color_green_component - sol_color_green_component
            d_blue  = ref_color_blue_component  - sol_color_blue_component
            
            diff += d_red**2 + d_green**2 + d_blue**2
        }
    }
    rank = -diff

Note that the rank is the negative of the difference between the two images. The reason is that AI::Genetic tries to maximize the rank of the fittest solution, so I needed a measure that increases for more fit solutions. Alternatively, I could have set the rank to 1/diff and achieved the same effect.

I chose to iterate for a predefined number of generations. Another way would have been to keep on evolving until the rank of the best solution is within a given threshold. But, I really had no idea what that number would be.

## Results

For the GA parameters, I used the following:

* Population size = 100
* Crossover rate = 0.91
* Mutation rate = 0.01
* Number of generations = 5000

To keep runtime short, I used a small image. The program took around 12 hours to go through the 5000 generations. The album below shows the reference image, along with images at generations 0, 1250, 2500, 3750 and 5000.

As you can see, since the algorithm started from completely random triangles, the best solution of generation 0 has absolutely no resemblance to the final image. By the 1250th generation, though, the main color regions are well-defined. The change from there to the 5000th generation is not as obvious but little details are getting better defined.

## Code

Coming soon to github.

## Conclusion

It was surprisingly easy to write the program, and it performed relatively well. Just like evolution in real life, GAs are really slow. 5000 generations was enough to get a general outline of the final image, but to get a more accurate result, we need to run it for a much longer time. I'm currently running the same algorithm for 25000 generations to see what happens.

Also, the GA parameters that I chose were pretty much random. More thought (and trial & error!) should go into choosing them.
Moreover, the alpha value of all trianlges was hard-coded at 50%. A simple extension would be to add this parameter to the genome.

<div>
<iframe class="imgur-album" width="100%" height="300" frameborder="0" src="http://imgur.com/a/AYCXF/embed" />
</div>
