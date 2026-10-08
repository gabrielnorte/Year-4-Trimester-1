```ad-info
General course goal: Photo realistic image synthesis
```

To achieve the goal, we will use **P**hysically **B**ased **R**endering, as a set of rendering technics that simulate physical behavior of light. 
- Highly realistic but huge rendering times

![[T1_Introduction.pdf#page=18&rect=222,78,678,375|T1_Introduction, p.18]]
*Raycasting is based on a view point and the use of two rays*
- Primary ray: Pixel in the viewport, directed to some part of a mesh
- Shadow ray: Pixel from the collision point of the primary ray to the sun
The lack or presence of intersection then determines if that point is hit by light or not

```ad-important
We use many primary rays for a single pixel, as that single pixel might cover different light sections. Therefore the color of the pixel is determined by the average of all the rays. Using only one ray causes aliasing

Lab implementation might differ
```

# Volume Graphics
We shoot a ray from the viewport, and once a volumetric surface is reached, we **accumulate density**. This is similar to *ray marching (marching along the mesh)*
	- For each marching step, we compute the light taking into account ALL the previous steps