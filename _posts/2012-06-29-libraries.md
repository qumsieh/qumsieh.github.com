---
layout: default
published: false
---
# Does Using a Library Waste Precious Memory?

At some point in your coding project, you will contemplate the pros and cons of using a library vs rolling out your own solution. The tradeoffs are always the same:

## Pros of Rolling Your Own Solution
* You can customize it to your own needs.
* You can control and optimize memory usage (which can be very helpful on mobile platforms).
* No learning curve as it's all your code.

## Cons of Rolling Your Own Solution
* It takes longer to develop.
* Your code won't be perfect at the beginning and you will waste precious time chasing bugs (which have already been fixed in existing libraries).

There will be cases when developing your own library makes more sense than developing your own:

* Your use case is very specific to your application, and there are no libraries that do exactly what you want.
* Existing libraries are too huge for your needs and implement too many features that just add bloat to your software.
* You really know what you are doing, and you are looking for a learning experience.

In my case, there are two areas where I contemplated the use of libraries:
1. OpenGL graphics: although my graphics is 2D and relatively simple, I had made the decision to go with OpenGL; mainly as a learning exercise.
2. Physics: although I don't need a full-fledged physics engine, I need a way to test for collision of non-trivial shapes.

I started by rolling my own code for both cases. It seemed to make sense since I realy need a small subset of what a library would offer. But, very quickly I changed my mind.

For the graphics part, the boiler-plate code necessary to create the simplest of operations (like rendering an image onto a specific location on the screen) consumed more lines of code than I expected. Since I'm not very well versed in OpenGL, it took me a while to figure out how to properly structure my code in a way that makes sense and leaves it somewhat easy to maintain. But that ease of maintenance quickly disappeared once my code became a bit more complex. At this point I started looking at existing libraries and experimented with LibGDX and AndEngine. I quickly converged on LibGDX, mainly due to the availability of good documentation. And since LibGDX hides a lot of OpenGL's mundane code, adopting it for RoboWars made my code much simpler, and easier to follow and maintain. As an added benefit, LibGDX allows you to develop your code in a platform-independent manner and then deploy on the desktop, Android and HTML. This makes for a faster testing cycle since there is no need to wait for the applicatin to load on the Android emulator or actual device.

For the physics part, I found myself googling way too many times for things like rotating an object about a point, testing for point inclusion within a polygon, etc. The worst part is that most solutions on the web are either too complex, not complex enough, or full of errors. Debugging someone else's code, especially if you're not familiar with the algorithms used, is not the most pleasant thing to do. So, again, I went looking for a library, and settled on Box2D, mainly because it integrates well with LibGDX and other OpenGL libraries. Again, this simplified my code to a great extent.

# TL;DR

For RoboWars, I'm using LibGDX for OpenGL graphics and Box2D for physics.