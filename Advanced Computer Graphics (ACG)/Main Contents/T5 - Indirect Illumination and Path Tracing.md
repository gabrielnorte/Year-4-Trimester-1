Just with direct illumination, all the points that don't receive a direct light will be left black. The resulting images are not really realistic, *as indirect light always lights up these dark areas*

# Indirect illumination
Light that arrives at a given scene point after bouncing more than once through the scene
- Implies simulating light paths with three or more rays
![[T5_PathTracing.pdf#page=12&rect=114,194,739,518|T5_PathTracing, p.12]]
```ad-info
All scenes that receive light directly from the light source only have direct light
- This is why the ceiling is dark, as light only goes down
```

We can see that the more bounces occur, the less light appears due to the current bounce, therefore, **having many bounces becomes irrelevant** $\to$ The image with 3 bounces is darker, so it doesn't add much, which can be seen with how the 0+1+2+3 bounces image doesn't change compared to the previous one

### [[Bouncing lights demo]]

As the number of bounces increases, we will take more and more samples, which becomes expensive and can add noise.
*Ideally, the average would be the average of all paths, but looking for all of them is really difficult*

```ad-note
title: Exercise
- Can we generate all possible paths
Yes, though extremely expensive, specially with area lights and many objects
- What strategy should we take?
Random rays that hit a point with light and then average like in montecarlo?
```
 **We can use information from the BRDF (how rays will reflect off a surface)**

- Compute intersection
- Generate random direction
- ComputeRadiance(r)
- Uniformly random for the sake of simplicity

```c++
ComputeRadiance(Ray r) {
	x = intersectScene(r); // Test intersection
	L_0 = x.emittedLight(-r.d); //r.d is wo (from point to camera)
		#L_0 is just in case the material in which it bounced emits light
	wi, pdf = getRandomDIrection(); //pdf as probability for that direction
	r_sec = Ray(x, wi);
	L_o += ComputeRadiance(r_sec)*x.brdf(wi, -r.d)*dot(x.normal, wi) / pdf //Montercalo -> L_0 + (1/N)sum (L_i*cos)/pdf * f_r*
	return L_o;
```

We can also use the ray's depth to handle infinite recursion
```c++
	x = intersectScene(r); // Test intersection
	L_0 = x.emittedLight(-r.d); //r.d is wo (from point to camera)
		#L_0 is just in case the material in which it bounced emits light
	wi, pdf = getRandomDIrection(); //pdf as probability for that direction
	if (r.depth < maxDepth)
		r_sec = Ray(x, wi);
		L_o += ComputeRadiance(r_sec)*x.brdf(wi, -r.d)*dot(x.normal, wi) / pdf //Montercalo -> L_0 + (1/N)sum (L_i*cos)/pdf * f_r*
	return L_o;
```

```ad-info
The concept of samples per pixel in spp now it's more like **paths** per pixel, as the path can diverge into many different rays, with the final color being the average of all of the rays
``` 

```ad-summary
Even though many rays are generated per intersection, that's kinda simulated by the fact that we shoot many rays from a single pixel (which all fall on the same point)
For now we don't consider rays from a single pixel that start from different origins within the same pixel, thus all the rays from the center fall in the same position
- PRONE TO ALIASING THOUGH.
```

- Since we're taking emission as part of the indirect illumination algorithm, we don't consider it on the direct illumination one
# Path Tracing with next event estimation
We first shoot a ray and, from the intersection, 
$$L_{i}(\text{pixel}, r.d ) = L_{o}(x. -r.d) = L_{e}(x, -r.d)+L_{r}(x, -r.d)$$
- $L_{e}$: Emissive material light
- $L_{r}$: Light information, which we divide into **direct** and **indirect**
$$L_{r}() = L_{D}$$

```c++
DirectRadiance(x, ωo) 
	Le, y, pdf = light.getRandomPointOnLight // Area light sampling
	wi = Direction(x, y);
	if (Scene.shadowINtersection(x, y)) //If intersect with object, no light
		return 0
	else:	
		return Le*x.brdf(wi, wo)*G(x, y) / pdf; 

IndirectRadiance(x, ωo, depth) 
	wi, pdf = getRandomDirection();
	L_ind = 0;
	if (depth < maxDepth)
		secRay = Ray(x, wi, depth+1);
		y = interesctScene(secRay);
		light_at_x =  ReflectedRadiance(y, -wi) //Light reflected from surface from which it 
		L_ind = light_at_x * x_brdf * dot(wi, wo);
	
	return L_ind;
```

# Advanced Path Tracing
Any integral can be approximated with MONTECARLO
```ad-missing
The expected value of MONTECARLO is equal to the integral, check proof
```

The thing is, we can reduce the error by trying to emulate a function that ressembles the pdf
- We need to find the **most important samples**
- 
