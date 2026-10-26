Now using an **non-point light**, this lab tries to emulate indirect lightning and caustics

# New classes and framework
`hemisphericalsampler.cpp`:
- `getSample()` Given a normal n at the surface of point x, generate a spherical direction on the hemisphere centered on n.

*Emissive materials are already created, and have the getRadiance function defined*
```c++
Vector3D Emissive::getEmissiveRadiance() const {
    return Ke;
}
```

# Direct illumination
## Clean up code that removes the noise
With this approach, we will still consider the ray that goes from the camera to the first intersection point $x$. But then, **instead of shooting a random ray from the intersection point and then checking if the result is a light or not, WE SHOOT A RAY FROM THE LIGHT TO THE POINT**
- We generate random position  $y$ on the light source (`sampleLightPosition`)
- The random vector is then $y-x$ rather than a random generated with hemisperical sampler

- For the equation, instead of taking `dot(n, wi)`, we take $G(x, y) = \frac{(N_{x}·w_{i})((-w_{i}·N_{y}))}{||y-x||^2}$
	- In the code, done with $max$ to ensure that dot products are positive

The reason this works is that now most rays will actually connect with the light in some way. Imagine the current pixel and the intersection with the ray shooting from it and a light source on top of it, with a sphere blocking 1/4 of the way.
**With just direct illumination code**
- From intersection ray, many second rays are generated
- Only a fraction of the total `spp` rays touch the light source
- Upon averaging by spp the pixel may be dark, or really bright, depending on how lucky we were with the random rays
**With area fomulation**
- From random point at the light source, generate vector towards existing intersection
- *ONLY IF AN OCCLUSION HAPPENS WITH THE SPHERE, THE RESULT WILL BE BLACK*
- On no other cases rays fail to touch the light source, thus result in a more consistent color between pixels.

