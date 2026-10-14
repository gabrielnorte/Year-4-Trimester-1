We know that traditional ray tracing an be very expensive, **as we need to send rays for every single triangle on scene, while also taking into account many other reflections**

(intersection tests >= nº pixels $\times$ nº triangles)

# Bounding volumes
For a given object, we can define a simple volume containing the mesh (spheres, boxes, ...)
Thus, to test intersection with the mesh:
- First intersection with the bounding volume
- If the ray does not intersect the volume, it doesn't intersect the mesh

```ad-info
The bounding volumes are not meshes
```

## Ray Sphere intersection
![[T3_RayCasting_RRT.pdf#page=10&rect=42,74,733,489|T3_RayCasting_RRT, p.10]]
	Replacing $p$ with $r(t) = (o + td)$, thus, with the only variable being $t$, $t$ is found by solving a quadratic equation where $a, b, c$ are defined by the image above

- 1 solution: Single intersection, use that one
- 2 solutions: Get the one closest to the origin
- 0 solutions: No intersections

```ad-failure
The solutions must always imply $t > 0$, and the bounding box shouldn't be too big, just enough so that most intersections with the sphere actually end up as intersections in the actual mesh.
On other cases, a lot of extra intersections that don't collide with the mesh will be computed
```

## Limitations
The efficiency of this method is tied directly to how well the shape is enclosed by the circle, **which doesn't usually happen**
- We need something that gets adjusted to the shape of the object

*We use 3D structures that iteratively divide a bounding box*
See [[Acceleration Structures For Ray Tracing]]


# Ray casting
Just considering a scene with diffuse or glossy objects (as available in the phong model).
A ray is shot from the center of the pixel and, when intersecting with an object, it gets is color from the ray that gets reflected, based on light and the material itself

We will study light behavior with raycasts starting from the most simple light source
## (Diffuse) Point light sources
```ad-info
*Diffuse* because light is equally emitted in all irections
*Point* because they have no area 
```

They're characterized by a 3D position $p_{L}$ and an intensity 𝑰 (RGB)

We then denote **direct irradiance $E_{i}(p)$** at a shading point $p$ due to a light source $L$ with position $p_{L}$
- LIGHT'S INTENSITY DECREASES QUADRATICALLY
$$E_{i}(p) = \frac{I_{L}}{d^2}, \text{where } ||p_{L}-p||$$
# Law of reflection
Following this law, it is useful to consider the **perfect specular reflection as $w_{R}$**
![[T3_RayCasting_RRT.pdf#page=20&rect=27,76,876,535|T3_RayCasting_RRT, p.20]]
All of this calculations can be visually carried out (vector operations)

```ad-caution
This might appear in the exam
```

# Light - material interactions
- Reflections at the surface (specular (mirror), diffuse or glossy)
- Refraction (caustics)
- Subsurface scaterring

## Reflections at the surface
![[T3_RayCasting_RRT.pdf#page=22&rect=93,59,671,413|T3_RayCasting_RRT, p.22]]
	The more spread out the lights, the larger the specular reflection, leading to solid color

The phong model allows to visualize the first two
Considering **phong** illumination, **we differentiate different reflections**
![[T3_RayCasting_RRT.pdf#page=24&rect=49,77,833,372|T3_RayCasting_RRT, p.24]]
```ad-warning
(Specular reflection is often denoted as glossy, since specular relates to perfect specular reflections)
```

### Diffuse reflection
Incident light gets equally scattered in all possible directions, therefore, no matter the viewing direction, the radiated light will be same on all directions.
**Still, the intensity will be different**
$$L_{o}^{d} = E_{i}(p)(w_{i}·N)k_{d}$$
The use $w_{i}$ accounts for the shadow

### Glossy (Specular) reflection
Note that the equation is the same, but it includes a **specular color** $k_{s}$ with the dot product between the perfect reflection direction and the viewpoint. This dot product makes it so that the closer the viewer is to the perfect reflection, the bigger the dot product, thus the bigger the reflection.

How far the viewer must turn to stop seeing the glossy term is then determined by the *shininess coefficient* $s$ (size of the lobe).
- Being a dot product, viewing it perpendicurarly will have no reflection

THE SUM OF RGB COMPONENTS BETWEEN $k_{d}$ and $k_{s}$ SHOULDN'T BE MORE THAN 1

### Ambient term
Phong just assumes an ambient illumination of the form
$$L_{o}^{(a)} = k_{a}I_{a}$$
### All terms together
![[T3_RayCasting_RRT.pdf#page=28&rect=40,54,958,523|T3_RayCasting_RRT, p.28]]
With $V(p, p_{L})$ being the visibility term, where we use the shadow ray to determine if the point is actually seen or if it's black.

Ambient light is not multiplied by this function since it is not affected by present light sources

```ad-caution
Dot products are only done between vectors, RGB's are multiplied element wise
```


### Applied to phong reflection model (simplification)
We will denote the reflection function as
$$\color{SKYBLUE}f_{r}(w_{i}, w_{o}) = k_{d}+k_{s}(w_{r}·w_{o})^s$$
Which is part of $L_{o}(w_{o})$, leading to:
$$L_{o}(w_{o}) = V(p, P_{L})E_{i}(p)(w_{i}·N){\color{SKYBLUE}f_{r}(w_{i}, w_{o})}+k_{a}I_{a}$$
For multiple light sources then:
![[T3_RayCasting_RRT.pdf#page=30&rect=160,20,760,320|T3_RayCasting_RRT, p.30]]

# Recursive Ray Tracing
![[T3_RayCasting_RRT.pdf#page=34&rect=39,58,624,381|T3_RayCasting_RRT, p.34]]

# Specular Reflection
![[T3_RayCasting_RRT.pdf#page=36&rect=39,69,902,416|T3_RayCasting_RRT, p.36]]
# Specular Transmission
With tranmission, we need to compute the ray that gets transmitted through a medium. For that, we use **snell's law**
$$\frac{\sin \theta_{i}}{\sin \theta_{t}} = \frac{\eta_{t}}{\eta_{i}} = \eta = \mu_{t}$$
Similar to the specular reflection $w_{r}$, just with vector addition we can do:
![[T3_RayCasting_RRT.pdf#page=40&rect=70,72,888,367|T3_RayCasting_RRT, p.40]]
[[Full transmitted ray proof]]
$$w_{t} = N(\eta^{-1})$$
Given the square root term, it is negative for incident angles which are really large, **which indicates that there is no transmission happening given this angle of direction**