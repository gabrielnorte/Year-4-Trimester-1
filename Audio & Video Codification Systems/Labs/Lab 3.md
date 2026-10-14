# Creating filters
We divide the spectrum in M different bands. Depending on the filter we want to apply, bands will be treated differently ()

## Cosine modulation
Just shifting a filter so it's centered on a frequency $f_{C}$
$$filter·\cos(2\pi f_{c})$$
This already creates both the positive and negative counterpart

```ad-important
So we can create a filter centered at zero and the shifting it to the different bands
```

So for each band (filter), we would have the signal length duplicated as the number of filters.
- By critically sample, we can make it so that **the sum of samples in the filters is no more than the signal lenght** - DECIMATE

## Decimation
For decimation, we only get `[::M]`, leading to $\frac{fs}{M}$ (downsampling by M)
*Of course, with downsampling, even if most samples are valued zero, information is still being lost*

# Hop sizes and band lengths
Depending on the length of the filter with non-zero samples, **the amount of bands and their length gets adjusted so that the filters advance in different $f_{c}$ without creating empty spaces or overlaps**

# LAB CONTENTS
## `firwin` (FIR filter and windowing)
taps: Length in samples
Order: Length-1