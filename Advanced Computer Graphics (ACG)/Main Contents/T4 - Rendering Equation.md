```ad-important
title: Reminder
Raycasting: Determining visibility
Raytracing: Checking ray behavior
- For each intersection we first consider perfect reflection and perfect transmission ray, and we continue this recursive process until a non-transmissive or reflective material is reached

The current approach does not provide soft shadows, which will be obtained using **non-point lights**
```

# Light
![[T4_REq_MC_Direct.pdf#page=8&rect=49,135,952,415|T4_REq_MC_Direct, p.8]]
Remember that color is not a property of an object, it's a sensation that our brain detects a certain way, in color
- The physical quantity that our eyes perceive is denoted as **radiation**

See [[Angles and Solid angles]]

# Spherical Directions
A direction can be characterized by 2 angles within a sphere, thus:
![[T4_REq_MC_Direct.pdf#page=12&rect=56,87,955,440|T4_REq_MC_Direct, p.12]]

## Spherical to Cartesian and viceversa
$$x = \sin \theta \cos \phi$$
$$y = \sin \theta \sin \phi$$
$$z = \cos \theta$$
And from cartesian to spherical
$$\theta =\cos^{-1}z$$
$$\phi = \tan ^{-1} \frac{y}{x}$$

# Differential solid angles
A differential solid angle is an infinitesimally small (dw) solid angle around a given direction
![[T4_REq_MC_Direct.pdf#page=14&rect=50,126,941,449|T4_REq_MC_Direct, p.14]]

We will use this measure for directions

# Radiance measures
*Radiance is one a set of radiometric quantities used to describe the interaction of visible electromagnetic radiation with matter*

| Radiometric Magnitude | Symbol | Units              |                                                                |
| --------------------- | ------ | ------------------ | -------------------------------------------------------------- |
| Flux                  | $\Phi$ | W (J/s)            | How many light traverses a surface in a given time             |
| Irradiance            | E      | W/m^2              | Used for surface lights (either sources or receiving surfaces) |
| Radiant intensity     | $I$    | W/sr (steradiants) |                                                                |
| Radiance              | $L$    | $W / (m² s r)$     | The amout of light an an infinitessimal direction              |
![[T4_REq_MC_Direct.pdf#page=17&rect=57,156,720,440|T4_REq_MC_Direct, p.17]]

# The rendering equation
To get the amout of light on a given pixel, we will get the intersection point and check the light that gets bounced back onto that same pixel
## Hemispherical Formulation
$L_{e}$: Self emitted light on the same direction (only for emissive objects)
![[T4_REq_MC_Direct.pdf#page=19&rect=116,42,929,309|T4_REq_MC_Direct, p.19]]

[Video demo](https://www.youtube.com/watch?v=eo_MTI-d28s)

# BRDF $f_{r}(w_{0},w_{i})$
The Bidirectional Reflectance Distribution Function just indicates how the material behaves when hit by light (*models reflectance of light at a surface)*
- Invariant result when $w_{0}$ and $w_{i}$ are swapped ($f_{r}(w_{0}, w_{I}) = f_{r} (w_{i}, w_{0})$)
- Must respect the energy conservation light
$$\forall w_{o} = \int_{\Omega_{2\pi}} f_{r}(w_{0}, w_{i})(N·w_{i})dw_{i} \leq 1$$
The **phong reflection model**:
![[T4_REq_MC_Direct.pdf#page=22&rect=51,103,754,375|T4_REq_MC_Direct, p.22]]
Thus, **we use a modified version of it, that normalizes the coefficients**
![[T4_REq_MC_Direct.pdf#page=23&rect=57,199,748,337|T4_REq_MC_Direct, p.23]]

## Solving the rendering equation
Due to the recursive nature of this process, **obtaining an analytical solution is almost impossible** - USE MONTECARLO INTEGRATION

# Montecarlo integration
Our objective is computing an integral of a PDF over a range $[a, b]$. We will estimate it by randomly sampling the integral
$$\hat{I} = \frac{1}{N}\sum_{j=1}^{N} \frac{f(x_{j})}{p(x_{j})}$$
- N as number of used samples
- $x_{j}$ sample location (random)
- $f(x_{j})$ is the sample value
- $p(x_{j})$ is the probability of sample value

```ad-info
**Advantages**
- Simple
- Dimension independent
- Works for complex function
  
**Disadvantages**
- Slow convergence (needs many samples for accurate results)
```
![[T4_REq_MC_Direct.pdf#page=30&rect=62,195,737,432|T4_REq_MC_Direct, p.30]]
	The artifacts are due to wrong estimations between pixels 
	The more uniform the pdf, the less error (as random samples will look like actual pixel)

With montecarlo, we will estimate the second half of the BRDF equation as follows:
![[T4_REq_MC_Direct.pdf#page=31&rect=151,65,632,373|T4_REq_MC_Direct, p.31]]

# Direct & indirect illumination
- **Direct Illumination**: the light that arrives at a surface directly from a light source
	- Hard transitions, sharp variations
	- We know where it comes from (light sources)

- **Indirect illumination:**
	- All the light that arrives after bouncing at least once  Smooth, slow variations
	- Can come from any direction above the surface

## Splitting the RE into direct and indirect lightning
![[T4_REq_MC_Direct.pdf#page=34&rect=52,76,881,369|T4_REq_MC_Direct, p.34]]

## Estimating Direct Illumination 
At each visible point we generate a set of uniformly distributed random directions over the hemisphere ($p(w) = \frac{1}{2\pi}$), then if it touches a light source, account for its distribution
If not, $L_{i}^{dir}(x, w_{0}) = 0$, that is, no direct light

![[T4_REq_MC_Direct.pdf#page=37&rect=170,12,795,491|T4_REq_MC_Direct, p.37]]
```ad-caution
There's a clear noise issue due to the fact that many rays are not directed towards the light source, thus ending up in zero
To solve this, we will check which points of the light source reach the object, then only study rays that come from this - WE USE **SOLID ANGLES**
```

### Area formulation of the direct component - AREA SAMPLING
$V(x, y)$ as the visibility term
![[T4_REq_MC_Direct.pdf#page=39&rect=35,61,919,384|T4_REq_MC_Direct, p.39]]
![[T4_REq_MC_Direct.pdf#page=40&rect=50,59,748,379|T4_REq_MC_Direct, p.40]]
![[T4_REq_MC_Direct.pdf#page=41&rect=2,205,955,541|T4_REq_MC_Direct, p.41]]
