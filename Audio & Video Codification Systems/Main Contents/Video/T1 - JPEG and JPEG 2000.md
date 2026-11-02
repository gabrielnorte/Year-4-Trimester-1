**J**oint **P**hotographic **E**xperts **G**roup is a protocol that compresses images. It's a *lossy* compression method, and it can also be used as a file format (.jpeg)
- Support **true color** (24 bits)

```ad-info
The compression is mathematically based
```

The encoding diagram for images can be reduced to:
![[T1 - JPEG and JPEG 2000-1793635870298.webp]]
With the decoding as
![[T1 - JPEG and JPEG 2000-1793635884080.webp]]

As in audio, we will take human limitations for compression purposes. The human eye:
- We recognize objects equally well regardless of image size
- Recognition speed does not depend on image size

**JPEG** is heavily used in computing and internet, and its compression factor can be adjusted at will
- Though being lossy, the image can't really be recovered

# DCT (Discrete Cosine Transform)
The **raw** data of an image is just the value of all the pixels in the image discretized to a specific grid
- This grid will not have the same size as the pixels, instead, the grid values will behave as pixels, describing the content inside the grid square

Now, take a set of grid values in a row:
![[T1 - JPEG y JPEG 2000.pdf#page=28&rect=8,51,664,355|T1 - JPEG y JPEG 2000, p.28]]
DCT tries to find a $\cos$ setting so that it ressembles the curve as much as possible
Thus we compressed the entire sequence of numbers to just 3 values
![[T1 - JPEG y JPEG 2000.pdf#page=33&rect=51,142,721,321|T1 - JPEG y JPEG 2000, p.33]]
![[T1 - JPEG y JPEG 2000.pdf#page=38&rect=42,54,686,230|T1 - JPEG y JPEG 2000, p.38]]
This is all based on the formula:
![[T1 - JPEG y JPEG 2000.pdf#page=34&rect=30,102,708,239|T1 - JPEG y JPEG 2000, p.34]]

After this compression, we can then apply **run length** encoding, which encodes the image even further
## Run length encoding
![[T1 - JPEG y JPEG 2000.pdf#page=39&rect=74,163,678,253|T1 - JPEG y JPEG 2000, p.39]]
We then use a **serpentine pattern** to run over the entire image and compressing

```ad-note
For color images, this process is just multiplied by 3
```

Professionals at JPEG also introduced the YCbCr color model, imitating how the real eye looks at imaages:
- Y: Chroma luminance (grayscale image)
- Cb: Chroma blue difference
- Cr: Chroma red difference

![[T1 - JPEG y JPEG 2000.pdf#page=47&rect=85,38,610,305|T1 - JPEG y JPEG 2000, p.47]]

# JPEG 2000 - Quality loss problem
```ad-info
File extension `.jp2`
``` 
It is actually superior than standard JPEG:
- Superior compression at low bit rates
- Storage of multiple resolution in a single bitstream
- PRecise rate control without recompression
- Lossy and **lossless** compression
- Progression by resolution, component, spatial region or quality

*It failed to standarddize, it required hardware that adapted to the codec (+ backwards incompatible with JPEG)*

## Wavelet transform
Instead of the DCT, we use the **wavelet transform instead:**
![[T1 - JPEG y JPEG 2000.pdf#page=59&rect=107,159,606,222|T1 - JPEG y JPEG 2000, p.59]]
A problem that the DFT presents that gets fixed by the wavelet transform which applies filters based on the specific frequencies - LOW PASS AND HIGH PASS
$$T_{m, n} = \int_{-\infty}^\infty x(t)\psi_{m, n}(t) dt$$
```ad-summary
Say we want to separate flat areas from small details
- Low pass filters: Capture smooth and big areas
- High pass filters: Capture details, edges of objects or small textures
```

![[T1 - JPEG y JPEG 2000.pdf#page=84&rect=17,56,708,313|T1 - JPEG y JPEG 2000, p.84]]
Mixing all these images we can obtain the final compressed result
```ad-example
LL (Low low): 
LH (Low high):
HL (High low):
HH (High high): Tiny, diagonal details
```
### Downsampling
After using the filters, we have too much data to handle easily. So, we keep only every second sample (imagine throwing away half of the points), which is called downsampling. This makes the data smaller and easier to work with.

```ad-important
Depending on what output we want and how the original image is, we can consider iterating the filtering process or the downsampling, to obtain different levels of details
```
### Multiresolution analysis
This is a fancy way of saying that DWT lets us see the picture at different levels of detail, like looking at it with different levels of zoom. This is super helpful for things like compressing images, where we want to keep the important parts but get rid of unnecessary details to save space

![[T1 - JPEG y JPEG 2000.pdf#page=93&rect=135,34,575,341|T1 - JPEG y JPEG 2000, p.93]]
## Why JPEG2000 Failed
- Patents
- Microsoft being microsoft
- Browser support
- Hardware support
- Performance trade offs (at the time)

![[T1 - JPEG y JPEG 2000.pdf#page=96&rect=74,36,659,331|T1 - JPEG y JPEG 2000, p.96]]

# GIF (Graphics interchange format)
- Supports animation 
- Supports separate palette with 256 colors
- Compressed with LZW
- Less suitable for color photographs

# PNG (Portable Network Graphics)
- Non-patented, designed to substitute .gif
- Supports 24 bit RGB or 32 bit RGBA
- DEFLATE Encoding (Based on LZW)
