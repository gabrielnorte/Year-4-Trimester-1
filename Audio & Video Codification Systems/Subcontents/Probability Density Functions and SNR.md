![[2-Quantization-and -entropy-coding.pdf#page=7&rect=24,65,682,307|2-Quantization-and -entropy-coding, p.7]]
With PDF's, we can of course obtain
$$\mu = E[X] = \int xp(x)dx$$
$$\sigma^2_{X}\int_{-\infty}^\infty(x-\mu_{X})^2p(x)dx=E[(X-\mu_{X})^2]$$
The X axis contains the frequency


We take **per-band measures** (a frequency range). BIT ALLOCATION IS DONE PER BAND AS WELL
- It doesn't make sense to allocate a lot of bits on 10 HZ because it would be pointless to assign that many amplitude values to a frequency that won't even be heard
- The best place to put many bits would be $1000Hz$

```ad-info
When an audio says 16 bits, **it refers to the whole thing**. It's a time domain measure that indicates that we use 16 bits for every single sample.
Whenever we use frequency domain we can differentiate between different bits for different bands 
```

![[2-Quantization-and -entropy-coding.pdf#page=9&rect=21,25,692,337|2-Quantization-and -entropy-coding, p.9]]
	Noise won't be heard as long as it lies below the masking threshold
![[2-Quantization-and -entropy-coding.pdf#page=10&rect=13,8,690,262|2-Quantization-and -entropy-coding, p.10]]