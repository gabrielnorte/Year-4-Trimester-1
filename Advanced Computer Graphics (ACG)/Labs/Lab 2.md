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

