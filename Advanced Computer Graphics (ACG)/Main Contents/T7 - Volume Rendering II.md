```ad-important
Midterm only up to T7
```

Reminder that the $\frac{dL}{dt}(t)$ equation is set up with a ray that traverses the volume from front to back (far to close to the cameras)
- In the lab, we shoot rays from the camera, thus **ray marching will be done in the opposite way**
$$t_{max} = t_{min}$$ Pseudocode would then be changed to
```c++
t_max = last_intersection_with_volume

// Traversal loop
tau = 0
Delta = computeStep()
t = Delta/2 //We want so sample the center of the rectangle (matches with the real curve) - reduces error
while t > t_max //Iteratively getting closer to the camera, t > t_max
	mu_a = getAborption(t)
	tau += mu_a x Delta
	t += Delta
```

# Emission-Absorption Model
Given the previous framework for the absorption model, we now consider this setup
- $\mu_{s}(t) = 0$ - NO SCATTERING
- $\mu_{t}(t) = \mu_{a}(t)+\mu_{s}(t) = \mu_{a}(t)$
- $L_{e} => 0$
![[T7_FullVolumeRendering.pdf#page=11&rect=50,68,646,251|T7_FullVolumeRendering, p.11]]

Using the 1st Order ODE for the **Radiative Transfer Equation**:
![[T7_FullVolumeRendering.pdf#page=13&rect=15,64,953,315|T7_FullVolumeRendering, p.13]]
$\color{GOLD}\mu_{a}(t')L_{e}(t') \to \text{Gain term}$
- Product of absorption and emitted light at the current step
- This light has to traverse all the volume
$\color{SKYBLUE}T(t', t)\to\text{Transmittance}$
- Attenuation of the light at the **current step $t'$**, which keeps advancing
- So for each infinitesimal position, we're going to take the gain term and the transmittance from that point to the end
- $T(t', t)$ gets smaller the further in we are into the volume, as less space has to be traversed for the light to go out t the viewer
- So gain at the beginning will get scaled up by a really small transmittance, as not much will get out from that point, while close to the end, transmittance will be big and gain won't be small
$\color{GREEN}BT(0, t)$
- Absorption term (from beginning to end)

## Riemann Sum approximation 
$$\sum_{i = 0}^{N-1} \mu_{a}(t_{i})L_{e}(t_{i})T(t_{i}, t)\Delta t + BT(0, t)$$
Where the first $T(t_{i}, t)$ is the cumulative transmittance from the current position till the end 
$$\sum_{i=0}^{N-1}\mu_{a}(t_{i})L_{e}(t_{i})e^{-\tau(t_{i}, t)}\Delta t +Be^{-\tau(0, t)}$$
```ad-important
When doing back to front, $\tau(t, t')$, this way, the integral is in the correct order
```

## Ray marching with emission absorption model
```c++
// FRONT TO BACK
t_far = last_intersection_with_volume
//Loop
tau = 0
Delta = computeStep()
t = first_intersection + Delta/2

while t < t_far {
	mu_a = get_absorbtion()
	tau = mu*Delta
	Le = getEmission()
	gain += mu_a*Le*exp(-tau)
	
	t += Delta
}
pixelColor = gain+B*exp(-tau) //Bg is static, multiply at the end
```
**Full correction**
```c++
t_max = intersectVolumeBoundaries(r)

//Traversal loop
pixelColor = 0
tau = 0
Deltat = ComputeStep()
t = t_max - Delta/2

while t > 0
	mu_a = getABsorption(t)
	L_e = getEmission
	pixelColor = mu_a*L_e * exp(-tau)*Delta
	tau += mu_a*Delta
	t -= Delta

pixelColor += Bexp(-tau)

```


![[T7_FullVolumeRendering.pdf#page=8&rect=39,59,956,374|T7_FullVolumeRendering, p.8]]

# Full Volume Rendering Model Set-up
![[T7_FullVolumeRendering.pdf#page=18&rect=53,61,942,364|T7_FullVolumeRendering, p.18]]
From which we arrive at the equation
$$\boxed{L(t) = {\color{ORANGE}Bt(0, t)+\int_{0}^t \mu_{a}(t')L_{e}(t')T(t', t) dt}+{\color{SKYBLUE}\int_{0}^t\mu_{s}(t')L_{s}(t')T(t', t)dt'}}$$
${\color{ORANGE}Bt(0, t)+\int_{0}^t \mu_{a}(t')L_{e}(t')T(t', t) dt}$
- Source term, doesn't depend on $L_{i}$ (incident light)
${\color{SKYBLUE}\int_{0}^t\mu_{s}(t')L_{s}(t')T(t', t)dt'}$
- In-scattering term
- Same as the previous gain, and also called by the transmittance
- This gain is defined by how much light arrives form all directions
$L_{s}(t) = \int_{S^2}f_{x}(w, w_{i})L_{i}(t, w_{i})dw_{i}$
- $f_{x}$: Phase function

**Important to note that the transmittance now gets modified to**
$$T(t_{a}, t_{b}) = e^{-\int_{t_{a}}^{t_{b}}u_{t}(t')dt'}$$
It can all be simplified to:
![[T7_FullVolumeRendering.pdf#page=20&rect=55,62,950,426|T7_FullVolumeRendering, p.20]]

```ad-info
For the labs, **we only consider direct illumination**.
Indirect illumination on the GPU gets too hard (volumetric path tracing)
```

## Phase functions
![[T7_FullVolumeRendering.pdf#page=21&rect=46,172,938,537|T7_FullVolumeRendering, p.21]]
It's sort of the volumetric equivalent to the phong's BRDF (See [[Advanced Computer Graphics (ACG)/Main Contents/T6 - Volume Rendering#In scattering (increase of radiance)]])

As in the **shininess coefficient**, we take a $\color{LIGHTGREEN}\text{Assymetric parameter}$ $\color{LIGHTGREEN}g$ that indicates where this circle will lay, indicating where all the light rays will get reflected
![[T7_FullVolumeRendering.pdf#page=24&rect=60,98,780,497|T7_FullVolumeRendering, p.24]]

See [[Additional assymetric parameter visualization]]

```ad-info
Negative parameter: Light scattering **out** (looks more solid, as in absorbed light)
Positive parameter: Light scattering **in**
$g = 0$: Diffuse, light scatters in all possible directions
```

# Voxels and uniform grids
Thanks to these, we can obtain a discrete value of the different coefficients $\mu_{a}, L_e, \dots$
```ad-abstract
Voxel: 3D pixel
- At the center, there's a $\mu_a, \mu_s, L_e$
```

The most important parameters are
- Spatial resolution
- The slices resolution related to the distance of two consecutive slices
- The temporal resolution, how often in time MRIs (or CTs) are obtained.

Due to the time dependency, it is likely that values between voxels changed while the ray was travelling between two of them. We can "smooth" out this changes through **interpolation**
## Linear interpolation
$$f(p) = (1-x)f(a)+xf(b)$$
- $x$ as a weighting factor

On **regular grids**, let $i$ be the index of the vertices in a 1D regular grid, and $s$ the distance between grid points. Thus for a point $p$ such $v_{i} \leq p \leq v_{i+1}$, the linear interpolation is
$$f(p) = (1-x)f(v_{i})+xf(v_{i+1})$$
	Where $x = \frac{d}{s}$, d as the distance between $v_{i}$ and p

## Bilinear interpolation
Used for bidimensional data, just simplify the 2D coordinates to 1D, and perform linear interpolation with each dimension separately

## Trilinear interpolation
Performs bilinear interpolation on two faces and then linearly interpolates the result 
- Directly available in the GPU
