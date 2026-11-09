Instead of talking about **functions**, we use fields as they bring more dimensionality.
Current framework is a function of a specific *direction*, while a field includes a full 3D space, and it's based on a *position* and a *direction*

```ad-info
**View synthesis**: Essentially create views of an image from a single view
```

---
# View synthesis
## Problem setup
Considering a pre-trained NeRF model (fit to a scene)
- Predicts color and density at each location, for each direction (All in 3D)

![[T8_NeRFs_And_Topics.pdf#page=8&rect=79,58,810,423|T8_NeRFs_And_Topics, p.8]]
	Both the output color and output density are similar to the values we can find when ray marching through **voxels**

From the graph on the right, we can tell that the first "object" to be found is the orange one, as it has the highest density at the closest distance

## Volume rendering and NeRFs
Using the volume rendering equation
$$C(r) = \int_{t_{n}}^{^t_{f}}\sigma(r(t))c(r(t))T(t)dt$$
- $\sigma(r(t))$: Absorption coefficient
- $c(r(t))$: Emissive radiance (color)
- $T$: Transmittance at point t
*It's treated as a volume rendering problem even though its a Computer Vision problem*

We can then discretize it as:
$$C(r) = \hat{C}(r) = \sum_{i=1}^N(1-\exp(-\sigma_{i}\delta_{i}))c_{i}T_{i}$$
# Model and training
## Training
![[T8_NeRFs_And_Topics.pdf#page=13&rect=53,134,902,399|T8_NeRFs_And_Topics, p.13]]
	Training can be done due to the fact that the original rendering equation for volumes is differentiable. The error is then evaluated using the measured color and the reference image
```ad-important
For this specific paper, we **overfit**
```

# Hierarchical sampling for improved performance
![[T8_NeRFs_And_Topics.pdf#page=16&rect=48,92,951,494|T8_NeRFs_And_Topics, p.16]]

# Results
![[T8_NeRFs_And_Topics.pdf#page=20&rect=80,79,753,390|T8_NeRFs_And_Topics, p.20]]
	Aside from the input data, nothing here is physically based, therefore, this result is usually worst. Nevertheless, the fact that we're able to obtain this glossy (view dependent radiance) information without a BRDF it's really nice


NerFs allow to recover mesh from point cloud, meaning I lose my job as a digital artist

---




