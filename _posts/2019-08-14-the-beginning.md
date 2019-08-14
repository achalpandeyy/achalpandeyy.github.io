---
layout: post
title: "The Beginning"
author: "Achal"
tags: [log]
---

A couple of weeks ago I started developing my physically-based renderer in my spare time.
Its pretty trivial at this point. I've implemented a (very) basic ray tracing engine capable of computing ray-sphere, ray-box and ray-triangle intersections. Any model loaded into the system is first triangulated and then is iterated over all the triangles to find the closest intersection point. There are no acceleration structures implemented at this stage nor there is any sort of multithreading, so polygon heavy meshes take quite some time to render.

As far as shading is concerned, there is no such thing implemented yet! I'm simply visualizing the result of intersections by calculating the facing ratio i.e. the dot product of view direction and normal at the intersection point. The images are being written in the .ppm format mainly because it is probably the easiest one to write to.

Here is a render of a spherical mesh "shaded" with face normals calculated for each triangle in the mesh:

![Face Normals Shaded](/assets/img/2019-08-14/faceNormals.png)

The faceted look is due to the same normal for each point inside the triangle. To mitigate this issue, we store normals at each vertex as a vertex attribute and interpolate these values
for the points inside the triangle using barycentric coordinates. This is known as Gouraud shading.

![Vertex Normals Shaded](/assets/img/2019-08-14/vertexNormals.png)

Note the rather sharp looking silhoutte of the sphere, this is because the sphere mesh is the same
we are just "shading" it differently i.e. using different set of normals.

I'm using [glm](https://glm.g-truc.net/0.9.9/index.html) as the math library and [tiny_obj_loader](https://github.com/syoyo/tinyobjloader) for loading .obj files.

I wanted to start logging about its development fairly early on in the process, so here we go.
My aim with this project is to learn about writing a production renderer the likes of which are used in VFX houses for CGI. Very much in the spirit of [mitsuba](https://www.mitsuba-renderer.org/), I'm planning to take this project in the direction of academia, using it as a "sandbox" for new rendering research.

Next, I'm planning to implement a simple light transport algorithm like unidirectional path tracing for global illumination and consequently more realism.

For the time being, here is another image rendered with my naive renderer:

![Low Poly Mill](/assets/img/2019-08-14/lowPolyMill.png)