# CIS 566 Project 1: Noisy Planets

Jamie Schwartz (jamiesch)

Resources:
https://en.wikipedia.org/wiki/Trilinear_interpolation

Demo: http://jamie2719.github.io/homework-1-noisy-planets-jamie2719

4 screenshots of the planet are below in the repository.


First I generated basic 3D Perlin noise in the vertex shader of the planet to determine the terrain on the planet. I ended up using summed Perlin noise for the height of the terrain; once I got the final Perlin noise value for a particular position using trilinear interpolation, I multiplied that value by the position vector to get a new position for the terrain that grew radially outward from the center of the sphere. I also calculated 3D Perlin noise to create a moving pattern for the ocean; before passing the initial position into the Perlin noise function, I multiplied it by a scaled version of the sine of the current time so that the Perlin noise values for the ocean would oscillate back and forth to mimic waves.

Once I had the basic shape of the terrain, I determined the colors of the different parts of the terrain based on the Perlin noise height value at that point on the terrain. The ocean had the smallest height offset, then sand, then grass, then mountains, and then snow at the very tops of the mountains. I colored the terrain differently above and below certain y positions to create snowy icecaps at the two poles of the planet. I used Lambert shading on all of the terrain except for the water, for which I used Blinn-Phong shading in order to get a specular highlight. I also gave the water and ice a lower transparency value than the rest of the terrain.

The 3 modifiable attributes are mountain height, ocean material, and amount of global warming. The mountain height changes the initial amplitude of the Perlin noise used in calculating the summed noise value for the height of the terrain. For the ocean material, I just changed the color of the ocean from blue (water) to red (lava). The amount of global warming is on a scale from -2 to 2, where -2 is total ice age, -1 is partial ice age, 0 is neutral, 1 is partial global warming, and 2 is total global warming. In total ice age, all of the land turns to ice and snow and all of the ocean turns icy. In partial ice age, this same effect occurs but only on around half of the planet, radiating from the poles. In partial global warming, the ice caps at the poles begin to shrink (the ice becomes regular terrain) and the water level of the ocean rises). In total global warming, the ice caps completely disappear and the water level of the whole ocean rises even more.






## Objective
- Continue practicing WebGL and Typescript
- Experiment with noise functions to procedurally generate the surface of a planet
- Review surface reflection models

## Base Code
You'll be using the same base code as in homework 0.

## Assignment Details
- Update the basic scene from your homework 0 implementation so that it renders
an icosphere once again. We recommend increasing the icosphere's subdivision
level to 6 so you have more vertices with which to work.
- Write a new GLSL shader program that incorporates various noise functions and
noise function permutations to offset the surface of the icosphere and modify
the color of the icosphere so that it looks like a planet with geographic
features. Try making formations like mountain ranges, oceans, rivers, lakes,
canyons, volcanoes, ice caps, glaciers, or even forests. We recommend using
3D noise functions whenever possible so that you don't have UV distortion,
though that effect may be desirable if you're trying to make the poles of your
planet stand out more.
- Implement various surface reflection models (e.g. Lambertian, Blinn-Phong,
Matcap/Lit Sphere, Raytraced Specular Reflection) on the planet's surface to
better distinguish the different formations (and perhaps even biomes) on the
surface of your planet. Make sure your planet has a "day" side and a "night"
side; you could even place small illuminated areas on the night side to
represent cities lit up at night.
- Add GUI elements via dat.GUI that allow the user to modify different
attributes of your planet. This can be as simple as changing the relative
location of the sun to as complex as redistributing biomes based on overall
planet temperature. You should have at least three modifiable attributes.
- Have fun experimenting with different features on your planet. If you want,
you can even try making multiple planets! Your score on this assignment is in
part dependent on how interesting you make your planet, so try to
experiment with as much as you can!

For reference, here is a planet made by your TA Dan last year for this
assignment:

![](danPlanet.png)

Notice how the water has a specular highlight, and how there's a bit of
atmospheric fog near the horizon of the planet. This planet used only simple
Fractal Brownian Motion to create its mountainous shapes, but we expect you all
can do something much more exciting! If we were to grade this planet by the
standards for this year's version of the assignment, it would be a B or B+.

## Useful Links
- [Implicit Procedural Planet Generation](https://static1.squarespace.com/static/58a1bc3c3e00be6bfe6c228c/t/58a4d25146c3c4233fb15cc2/1487196929690/ImplicitProceduralPlanetGeneration-Report.pdf)
- [Curl Noise](https://petewerner.blogspot.com/2015/02/intro-to-curl-noise.html)
- [GPU Gems Chapter on Perlin Noise](http://developer.download.nvidia.com/books/HTML/gpugems/gpugems_ch05.html)
- [Worley Noise Implementations](https://thebookofshaders.com/12/)


## Submission
Commit and push to Github, then submit a link to your commit on Canvas.

For this assignment, and for all future assignments, modify this README file
so that it contains the following information:
- Your name and PennKey
- Citation of any external resources you found helpful when implementing this
assignment.
- A link to your live github.io demo (we'll talk about how to get this set up
in class some time before the assignment is due)
- At least one screenshot of your planet
- An explanation of the techniques you used to generate your planet features.
Please be as detailed as you can; not only will this help you explain your work
to recruiters, but it helps us understand your project when we grade it!

## Extra Credit
- Use a 4D noise function to modify the terrain over time, where time is the
fourth dimension that is updated each frame. A 3D function will work, too, but
the change in noise will look more "directional" than if you use 4D.
- Use music to animate aspects of your planet's terrain (e.g. mountain height,
  brightness of emissive areas, water levels, etc.)
- Create a background for your planet using a raytraced sky box that includes
things like the sun, stars, or even nebulae.
