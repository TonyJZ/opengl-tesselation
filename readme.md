# Introduction

This simple application is used to test opengl tesselation method as I'm looking to use it to solve my problem which is cutting off holes from polygon.

## Context

The context is I have polygons described by contours (outter boundarty). Some polygons contain holes which are also described by contours. Some hole contours are inside polygon but some are intersected with polygon contour. The requirement is cutting off holes from polygon and export the correct triangles.

## Tessellation

The `Polygon Tessellation` in opengl can be found [here](https://www.glprogramming.com/red/chapter11.html).

When I added it in my project, I can not get correct results for some polygons. For example,
**Type 1**
>
          h4---h1                q0------------q3
          |     |                |   h4---h1    |
      q0------------q3           |   |     |    |
      |   |     |    |           q1------------q2
      |   h3---h2    |               |     |
      q1------------q2               h3---h2

**Type 2**
>
          h4---h1                q0--h4---h1---q3
          |     |                |   |     |    |
      q0------------q3           |   |     |    |
      |   |     |    |           q1------------q2
      |   |     |    |               |     |
      q1--h3---h2---q2               h3---h2

I can get correct results for **Type 1** polygons but failed for **Type 2** polygons. For **Type 2** polygons, I usually get results like below. Seems the winding number is wrong. (see [winding rules](https://www.glprogramming.com/red/chapter11.html))
>         h4---h1                   hi---hj
>         |     |                   |     |
>         hi---hj                   h3---h2


I found this [ORIGINAL CODES](http://www.songho.ca/opengl/files/tessellation.zip) from SONHO's [website](http://www.songho.ca/opengl/gl_tessellation.html#winding_rules) and added a function `tessellate4` to test my polygon cases. Finally I solved this problem by using `gluTessNormal` which specifying the normal for Tessellator, very senseful but less examples can be found talking about it.


# Who may be interested in this application

If you are
* looking for a method to generate polygon with holes,
* looking for a method to implement polygon CSG operations,
* or just very curious about tesselation.

# Some instructions for Windows lover

To run this application on Windows, you need [MinGW-w64](https://www.mingw-w64.org/downloads/), [freeglut](https://sourceforge.net/projects/freeglut/), and [glew](https://sourceforge.net/projects/glew/files/glew/2.1.0/).

A good reference for the installation is [here](https://medium.com/@bhargav.chippada/how-to-setup-opengl-on-mingw-w64-in-windows-10-64-bits-b77f350cea7e).