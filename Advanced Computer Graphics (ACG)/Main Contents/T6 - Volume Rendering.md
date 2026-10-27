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







# FINAL PROJECT IDEA
God rays from cloud formations