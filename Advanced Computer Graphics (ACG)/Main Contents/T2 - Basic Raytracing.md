As an intuition, **raytracing is similar to rasterization (object ordered rendering)**![[T2_BasicRayTracing.pdf#page=6&rect=59,31,895,398|T2_BasicRayTracing, p.6]]
Using the view projection matrix, all objects get flattened onto the projection plane, and using a depth buffer, everything is painted onto the frame buffer

See [[Depth Buffer Reminder]]

# Ray tracing basic methodology
Compared with the **depth buffer approach** (object order approach), where we paint based on the order in the Z buffer:
- Start from all the objects directly, all on the same layer rather than one on top of another (pixel order approach)
![[T2_BasicRayTracing.pdf#page=17&rect=29,55,734,435|T2_BasicRayTracing, p.17]]
- We shoot a ray to *TEST INTERSECTION* with the three triangles
- Based on the triangle the ray intersects with, the assign the color of that pixel 
- If ==🔵several intersections== are found, **keep the closest intersection as in the Z buffer**

```ad-info
Remember that we often use more than 1 ray per frame buffer pixel
```

Due to the parallel work this involves between pixel, the GPU might find this a bit expensive
![[T2 - Basic Raytracing-1791299645334.webp]]
- **Ray tracing loop checks for intersection rather than if the pixel is covered or not**
	- Ray tracing: Pixel based
	- Rasterization: Object based
---
# Raycasting
```ad-info
title: Basic ideas about rays / Assumptions
1. Light travels in a straight line
2. Light rays don't interact with each other
3. Light travels from light sources to the eye, it can be "reversed" as if it went from the eye to the light - RECIPROCITY
```

![[T2_BasicRayTracing.pdf#page=39&rect=40,216,747,381|T2_BasicRayTracing, p.39]]
With the parametric form defined as 
$$r(t) = o+td \quad 0\leq t < \infty$$
	t indicates the current point in the ray, $d$ is the direction of the ray

According to Apple on 1968, we send rays from the POV to the light source, and using intersections with objects we can define if the light reaches the camera or not.
![[T2_BasicRayTracing.pdf#page=41&rect=51,33,938,416|T2_BasicRayTracing, p.41]]
![[T2_BasicRayTracing.pdf#page=42&rect=58,34,928,404|T2_BasicRayTracing, p.42]]

- - - 
# Recursive Ray Tracing
![[T2 - Basic Raytracing-1791300468498.webp]]

# Distribution (Stochastic) Ray Tracing
Instead of shooting a single secondary ray at an intersection point, we can shoot many different secondary rays
- **Allows us to simulate area light sources**
- This is accurate as long as the material of the object allows for it
![[T2_BasicRayTracing.pdf#page=50&rect=163,44,657,429|T2_BasicRayTracing, p.50]]

```ad-warning
Not all materials reflect multiple rays, the material of the sphere was changed between the examples
Perfect mirror: Single reflection
Diffuse material: Range of reflections
```

## Glossy Materials
![[T2_BasicRayTracing.pdf#page=52&rect=34,60,743,497|T2_BasicRayTracing, p.52]]

# Path Tracing
- Trace random paths from the camera throughout the scene
- The paths can have a varying number of segments and do not end when a diffuse material is hit
- Several paths are generated for each pixel
- The paths’ contribution is averaged to get the final pixel color
![[T2_BasicRayTracing.pdf#page=56&rect=75,45,743,443|T2_BasicRayTracing, p.56]]

Not sending enough rays can result in the pixel missing some color information

```ad-summary
**Ray casting**: Casting a single ray (Direct lightning)
**Ray tracing**: From a single ray, creating creating others recursively (mirror and transmissive) until hitting diffuse material
**Path tracing**: Creating different paths from multiple rays on a single pixel (Indirect lightning, /spp needed) until *max_depth*
```

---
# Rays intersection
## Ray scene intersection
It will be done many times, as it encompasses all the objects in the scene and all its triangles. These have to be compared to all the other triangles not only of its own mesh, but also the rest of the scene meshes
## Ray-plane equation
![[T2_BasicRayTracing.pdf#page=64&rect=53,166,673,402|T2_BasicRayTracing, p.64]]
$$p:(p-p')·N = 0$$
	$p-p'$ will be a vector inside the plane, $N$ the normal vector, thus their dot product is 0
	All points $p$ that verify the equation are points in the plane

With the parametric equations for both the plane and the ray, the *ray-plane intersection is*
We write as $p = r(t)$ (point is a point in the ray)
$$(p-p')·N = (o + td-p')·N = 0$$
$$t = \frac{(p'-o)·N}{dN}$$
```ad-danger
Even if it cancels, the $N$ is required as it turns the vector into scalar value
```
## Ray Triangle Intersection
Since a triangle is always contained in a plane, we can just**:**
**Step 1:** Compute the intersection of the ray with the plane containing the triangle
**Step 2:** Determine whether the intersection point is inside the triangle

### Triangle in a plane  
Consider vertices $v_{1}, v_{2}, v_{3}$, to determine the plane we need $p'$ and $N$
- $p'$: Can be any vertex
- $N$: Cross product between triangle vectors
```ad-info
By the right hand rule
- Index: First multiplying vector
- Ring: Second multiplying vector
- Normal: Facing outside (UP)
```

![[T2_BasicRayTracing.pdf#page=68&rect=472,158,961,529|T2_BasicRayTracing, p.68]]

```ad-failure
title: Careful
Normal should be facing upwards
```

The thing is, **we have defined the plane on which the triangle lies**, but the intersection is still defined plane-wise.
Therefore, to verify if the intersection point obtained is inside the triangle we perform *inside / outside test*
![[T2 - Basic Raytracing-1794308886036.webp]]


FOR ALL THESE CALCULATIONS, ASSUME THE RIGHT HAND RULE AXIS (y as middle finger, pointing down-left, index to the left, z up)

## Performance challenges
Basic ray-scene intersection:
- Test intersection with all the scene objects

How costly is this?
- nº intersection tests ≥ nº pixels ≈ $10^6$ x nº triangles (?) (intersection checked for all triangles until reaching the **first** intersection)
- How many triangles on a complex scene? - > 20 MILION

Due to this, this an incredibility expensive computing intensive approach
