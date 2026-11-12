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
	
	//This is just a single sample, this whole section should be repeated N times and then averaged by N (or spp)
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

## Pure path tracing limitations
- Slow
- Requires too many samples 

As suggestions, we will consider:
- Separate radiance into direct and indirect - Increases speed
- Compute the two components separately - More organized
- Sample light sources area for the direct component (more efficient) - REDUCES NOISE
# Path Tracing with next event estimation
We first shoot a ray and, from the intersection, 
$$L_{i}(\text{pixel}, r.d ) = L_{o}(x. -r.d) = L_{e}(x, -r.d)+L_{r}(x, -r.d)$$
- $L_{e}$: Emissive material light
- $L_{r}$: Light information, which we divide into **direct** and **indirect**
$$L_{i}() = L_{e}(x, w_{o}) + L_{r}(x, w_{i})$$
$$L_{r}(x, w_{i}) = L_{d}(x, w_{i})$$

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

```ad-info
Essentially, pure path tracing "included" direct illuminations when the ray hit an emissive surface at depth one. Thus, when we separate direct and indirect on the nee shader, since these emission surfaces can get counted twice due to both direct and indirect handling it, **emissive surfaces are only counted once** (outside both direct and indirect)
![[T5 - Indirect Illumination and Path Tracing-1794418948268.webp]]

On the recursive step in IndirectIllumination(), if the material is emissive, we return 
```

# NEE and Pure path tracing
Pure path tracing:
- Mainly indirect, though due to hemispherical approach, direct illumination can happen at depth 1
- Noisy (hemispherical algorithm)
- Slow

NEE:
- Separate direct and indirect
- Emission handled else where, counted only once
- Direct uses area sampling less noise (**and less samples needed, at least for direct illumination**)

# Advanced Path Tracing
Any integral can be approximated with MONTECARLO
- The expected value of montecarlo is the theoretical value of the integral:
![[T5_PathTracing.pdf#page=38&rect=70,42,843,393|T5_PathTracing, p.38]]
	An estimator so that $E[\hat{I}] = I$ is unbiased, it tries to approximate the actual integral with the only source of error being the variance
	Biased estimators present a systematic error $B$, which drifts montecarlo approximations away from the integral

As for the variance, **it indicates how all the different samples change on hemisphere**, and applying montecarlo, THE NOISE DUE TO VARIANCE REDUCES WITH A FACTOR OF N, while the noise's standard deviation changes with a factor of $\sqrt{ N }$ 
- **Montecarlo converges slowly due to this factor of N and $\sqrt{ N }$**

To reduce the variance, we need to find a pdf that has the same shape as the integrant, obtained by setting $p(x) = \frac{f(x)}{I}$, *but we don't know neither f(x) or I*

In real applications, we will "guess" the shape of the integrand based on prior knowledge
- We need to find the **most important samples**

## Importance Sampling
![[T5_PathTracing.pdf#page=49&rect=51,115,909,476|T5_PathTracing, p.49]]
In our case, with $f(x)$ being $L_{i}(x, w_{0})$, the function has a higher value where there's light involved. Through hemispherical sampling, only sampling the light areas would be perfect to avoid noise, thus we need a pdf that ressembles this

```ad-failure
A bad PDF can be worse than a uniform, unbiased PDF
![[T5_PathTracing.pdf#page=50&rect=49,60,907,405|T5_PathTracing, p.50]]
```

Given that the integrand is based off $fr$ and $(w_{i}·\cos \theta_{i})$, we can use this information. Focusing on the BRDF function
## Diffuse BRDF
![[T5_PathTracing.pdf#page=52&rect=37,5,852,390|T5_PathTracing, p.52]]

## Specular (Glossy) BRDF
![[T5_PathTracing.pdf#page=53&rect=44,61,768,390|T5_PathTracing, p.53]]

```ad-info
It can be assumed that the new montecarlo estimator with a pdf based on importance sampling is unbiased
```