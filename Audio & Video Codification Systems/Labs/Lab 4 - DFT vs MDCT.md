![[MDCT per band 6 bits.wav]]Check lab - DFT-DCT

# DFT VS MDCT
DFT
- Complex valued
- Phase and amplitude can be separated
MDCT
- Just coefficients (real function), no separate phase (integrated into weights)
	- Each coefficient is a weight of the base cosine function - *CAN BE NEGATIVE*
	- Sort of similar to DFT but this one uses COSINES specifically
![[Lab 4 - DFT vs MDCT-1792500923860.webp]]
	On stft, identical magnitudes (phase info goes separately)
	On MDCT, phase is mixed with magnitudes, thus differences in weights

![[Lab 4 - DFT vs MDCT-1792500738519.webp]]

# MDCT and time domain quantization

**Original**
![[Original.wav]]

**Per band**: Less quantization noise
![[MDCT per band 6 bits.wav]]

**Global quantization**: Not band aware, less accurate
Since MDCT has a lot of values close to zero, they might get quantized to higher values, leading to more noise
![[MDCT global 6 bits.wav]]

**Time domain quantization**: Takes time domain information, values don't get clipped to extreme values like MDCT, less quantization noise.
![[TimeDomainQuantization.wav]]


