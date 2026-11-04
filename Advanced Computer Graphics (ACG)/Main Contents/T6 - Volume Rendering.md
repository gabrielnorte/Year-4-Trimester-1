# Motivation
All the surfaces till now have been solid, and all the light rays propagated in a vacuum (constant radiance between surfaces).
With this, the following can't be modeled:
- Fog and smoke (attenuating light)
- Light scattered in the atmosphere makes the sky look blue

```ad-info
The following effects can be modeled using physically based rendering
- Volumetric shadows
- Fog
- ...
```

Similar to surface materials, **volumes exhibit different appearances and features**. When light interacts with media
- *Absorption*: Reduction in radiance due to the conversion of light to another form of energy - **dissapears**
- *Emission*: When radiance is added to the environment from luminous volume particles
- *Scattering*: When radiance heading in one direction is scattered to other directions due to collisions
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=12&rect=54,87,721,416|T6_RTE_VRE_AbsorptionOnly, p.12]]

# Participating media 
## Attenuation
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=15&rect=48,108,927,412|T6_RTE_VRE_AbsorptionOnly, p.15]]
## Emission
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=16&rect=49,117,914,411|T6_RTE_VRE_AbsorptionOnly, p.16]]

## Scattering
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=17&rect=56,109,904,409|T6_RTE_VRE_AbsorptionOnly, p.17]]

# Problem formalization
We will consider the following setup:
1. Ray through medium
2. Medium composed of particles that absorb, scatter or emit radiance

Aside from the ray direction, we now consider $p_{0} = r(0)$ as the first position of the volume touched by the ray, and $p_{max} = r(t_{max})$

```ad-important
We will consider that the light at $p_0$ is the same light that they ray was carrying in the first place
$$L(0) = B$$
	(boundary condition)
```

## Absorption
Consider an infinitesimal segment of the ray $dt$, with $L(T)$ as the amount of light going in
- Medium characterized by absorption coefficient $\mu_{a}$
	- Probability density that light is absorbed per unit distance traveled in the medium $(m^{-1})$
	- $\frac{1}{\mu_{a}}$ as the average distance at which an absorption event occurs

```ad-summary
Larger values of 𝜇𝑎 → more absorption → darker appearance
```

See [[Absorption visualizations]]

---
Along the infinitesimal segment, radiance is reduced due to absorptions by an amount $\Delta L$, such that:
$$L' = L-(\mu_{a}\Delta t)L$$
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=25&rect=34,38,941,278|T6_RTE_VRE_AbsorptionOnly, p.25]]

## Emission
Increased radiance along a ray due to chemical, thermal, or nuclear processes that convert energy into visible light
- Characterized by the relation between how efficiently an object absorbs light ($\mu_{a}$) and how efficiently it emits light $L_{e}$
- Emission is maximized when 𝐿𝑒 is large while absorption 𝜇𝑎 is low

See [[Emission Visualizations]]

---
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=28&rect=24,80,935,524|T6_RTE_VRE_AbsorptionOnly, p.28]]

## Scattering 
### Out scattering (reduction of radiance)
Now take a **scattering coefficient** $\mu_{s}$ which determines how much the light will scatter.
We can denote the change in radiance as 
$$\frac{dL}{dt} = -\mu_{s}(t)L(t)$$
### In scattering (increase of radiance)
This is light that gets scattered inside the volume
$$\frac{dL}{dt} = \mu_{s}L_{s}(t)$$Where the total amount of light that gets scattered ($L_{s}$) (*scattered radiance*), collects the incident radiance from all directions no the unit sphere, such that
$$L_{s}(t) = \int_{S^2}f_{t}(w, w_{i})L_{i}(t, w_{i}dw_{i})$$
- Like in the BRDF, $f_{r}$ is the phase function, which characterizes the directional density of light scattered at a point 𝑡 in a medium 

See [[Scattering Visualization]]

---
```ad-summary
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=34&rect=69,95,815,429|T6_RTE_VRE_AbsorptionOnly, p.34]]
```


# Radiative Transfer Equation (Microlevel)
By adding all the previous effects into a single equation, we can then denote
$$\frac{dL}{dt}(t) = -\mu_{a}(t)L(t)-\mu_{s}(t)L(t) + \mu_{s}L_{s}(t)+\mu_{a}(t)L_{e}(t)$$
$$\Delta L(t) = \text{Absorbtion+Out scattering+Inscattering+Emission}$$
For simplification, we can then take $\boxed{\mu_{t} = \mu_{a}+\mu_{s}}$, simplifying the equation to
$$\boxed{\frac{dL}{dt}(t) = -\mu_{t}(t)L(t)+\mu_{s}(t)L_{s}(t)+\mu_{a}(t)L_{e}(t)}$$

# From the RTE to the Volume Rendering equation


---
# Absortion-Only model Set up
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=44&rect=54,73,843,377|T6_RTE_VRE_AbsorptionOnly, p.44]]
Now, if we use the chain rule and set $f(t) = \ln(t)$ and $g(t) = L(t)$
$$\frac{d}{dt}\ln L(t) = \frac{1}{L(t)} \frac{dL}{dt}(t)$$
Continuing to isolate $L(t)$ (check proof on notebook) results in
$$L(t) = Be^{-\int_{0}^t\mu_{a}(t')dt'}$$
Which makes sense, as the light $B$ that goes in, gets altered by $\mu_{a}$ at time $t$
- The integral is known as the **optical thickness $\tau$**
- The whole exponent term is called **Transmittance $T$**

With this, the equation can be simplified to
$$\boxed{L(t) = Be^{-\tau(0,t)}}$$
$$L(t) =BT$$
- $T(t_{a}, t_{b}) = e^{-\tau(t_{a}, t_{b})}$ - *Beer-Lambert law*

## Approximation
As to estimate this equation, we can either go with ray marching or montecarlo integration


---
```ad-info
A medium / volume is **homogeneous** when its coefficients are constant
- $\mu_a(t) = \bar{\mu}_a$
- The self emitted light is also consatnt ($L_e(t) = \bar{L}_e$)
  
In **heterogeneous** media, these coefficients change
```

Thus, when the medium is homogeneous, it can be proven that
$$L(t) = Be^ {-\tau(0,t)} = Be^{-\tau \bar{\mu}_{a}}$$
However, on heterogeneous cases:
- $\tau$ is actually the integral of $\mu_a$, thus, it's just the sum of the area under it
- It can be simplified to a simple sum with **Riemann sum**
$$\tau(t_{a}, t_{b}) \approx \sum_{i=0}^{N-1}\mu_{a}(t_{i})\Delta t$$
With $\Delta t$ being the time jump, the accuracy of the result improves when this jump is small

This process is computed using **Ray Marching**
- March along the ray, and sample the $\mu_{a}$ at each step
- At each position $t_{i}$, sample $\mu_{a}$

# Ray marching
Ray marching comes with some assumptions
![[T6_RTE_VRE_AbsorptionOnly.pdf#page=55&rect=44,31,955,522|T6_RTE_VRE_AbsorptionOnly, p.55]]

```ad-info
Due to the raymarching process being a sum, the ray marching process can be done from the front to the back or the back to the front
- Front (closer to viewer)
- Back (further from viewer)
```

```c++
// Ray setup
Ray r;
r.shoot()
start_point = r.intersection()



// Ray marching algorithm
step = 1/10;
tau = 0.0;

for (i = start_point; i < start_point+1; i+step)) {
	mu_a = get_mu(i*back)*(step*back)
	tau += mu_a;
}
Lo = B*e^(tau)
```
![[T7_FullVolumeRendering.pdf#page=8&rect=39,59,956,374|T7_FullVolumeRendering, p.8]]

```ad-missing
Check one is better, front to back or back to front, in terms of computational power
(at what point is it useless to continue?)
```



























# FINAL PROJECT IDEA
God rays from cloud formations