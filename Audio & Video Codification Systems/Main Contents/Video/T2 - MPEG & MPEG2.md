 # Basic concepts
 Display Aspect ratio is specific for displays
## Pixel aspect ratio
It's the proportionality between pixel's width and height, **usually $1:1$**

## Bit rate
$$\text{bit rate } = \text{width · height· bit depth · FPS}$$
- If constant: **Constant Bit Rate (CBR)**
- If variable: **Variable aspect ratio (VBR)**

```ad-info
Variable can be used to save up bit rate in scenes that don't require it, like in quantization
If a black screen is shown, no need to send much bitrate
```

## In the past - 2000s ERA (CHECK FOR TFG)
**Interlaced video** was used to double the frame rate of a video display without consuming extra 
bandwidth

## Present
**Progressive scanning**

---
---
---
# MPEG (Moving People Experts Group)
A **lossy** compression method established by ISO in 1988, with its standard version created in 1993

Design to compress
- VHS quality raw digital video
- CD audio down to $1.5 Mbits$

```ad-info
VHS was 352x240 (NTSC)
```

MPEG allowed CD video to exist, though it didn't really work
## Compression
Since JPEG performs image compression, it can be used as **spatial compression (intraframe)**, while temporal compression (interframe) is handled by MPEG

## Encoding pipeline
![[T2 - MPEG y MPEG2.pptx.pdf#page=32&rect=79,33,611,317|T2 - MPEG y MPEG2.pptx, p.32]]
### Workflow
![[T2 - MPEG y MPEG2.pptx.pdf#page=35&rect=6,160,706,248|T2 - MPEG y MPEG2.pptx, p.35]]
- **Reduction of resolution**: Video downsized and turned into *YUV* (YCbCr)

#### Chroma subsampling 
It’s the practice of encoding images by implementing less resolution for chroma information than for luma information, taking advantage of the human visual system's lower acuity for color differences than for luminance.

*Since we have more rod cells (luminance) than cone cells, we can distinguish more information about light and dark than colors* - THUS WE CAN ALLOCATE MORE DATA TO BRIGHTNESS RATHER THAN COLOR:
![[T2 - MPEG y MPEG2.pptx.pdf#page=49&rect=21,121,698,364|T2 - MPEG y MPEG2.pptx, p.49]]
![[T2 - MPEG y MPEG2.pptx.pdf#page=50&rect=34,88,698,337|T2 - MPEG y MPEG2.pptx, p.50]]
	Y:U:V
	If all numbers are equal, no compression

# Motion Estimation
## I Frame (Intra frame)
These are keyframes, regular frames that are rendered as plain images

## P Frame (predicted)
A P-frame takes advantage of the fact that almost always the current picture can be rendered using the previous frame
- Used when the difference with the previous frame is really small

## B Frame (Bi-directional predicted frame)
Like the P frame, but also uses the next frame in addition to the previous frame
- We can create the one in the middle based on interpolation (kind of)

 ```ad-tldr
 **THIS IS WHAT CREATES COMPRESSION**
 ![[T2 - MPEG y MPEG2.pptx.pdf#page=60&rect=88,19,652,358|T2 - MPEG y MPEG2.pptx, p.60]]
 ```
 ![[T2 - MPEG y MPEG2.pptx.pdf#page=62&rect=90,24,660,355|T2 - MPEG y MPEG2.pptx, p.62]]
 We are only using the full picture in the intraframe
```ad-caution
Of course, being a full frame, it is also rendered and compressed as regular JPEG
While the rest depend on the other frames
- B frames are cheapest since they rely on "interpolation" between two frames
```

## Information loss
If the $I$ frame is lost, **the rest cannot be rendered if they're $B$ or $P$, resulting in artifacts in place of those frames**
![[T2 - MPEG y MPEG2.pptx.pdf#page=68&rect=3,20,722,368|T2 - MPEG y MPEG2.pptx, p.68]]

---
Applying **motion estimation**
- Vectors indicating frame motion appear when encoding rather than decoding (decoder only consumes the motion vector data)

```ad-danger
Motion compensation is the use of the motion estimation information to achieve compression. If you can describe the motion, then you only have to describe the changes that occur after compensating for that motion.
```
![[T2 - MPEG y MPEG2.pptx.pdf#page=75&rect=132,24,603,348|T2 - MPEG y MPEG2.pptx, p.75]]

# Motion compensation
Present frame is predicted by using estimated motion vectors and the previous frame. The prediction error is then calculated
![[T2 - MPEG y MPEG2.pptx.pdf#page=81&rect=147,20,588,333|T2 - MPEG y MPEG2.pptx, p.81]]
## Blockmatching 
- Different search algorithms are used
- Don't worry about all the algorithms and how each one is different
- Sub-pel - Boring ahh

---
**Then the coding is the same as in JPEG, we apply compression with DCT, quantization, run length encoding and huffman, but applied to the vectors**

```ad-info
Encode harder, decode easier
```

# Audio
Codec based on psychoacoustics
![[T2 - MPEG y MPEG2.pptx.pdf#page=100&rect=26,84,701,341|T2 - MPEG y MPEG2.pptx, p.100]]

# MPEG 2
![[T2 - MPEG y MPEG2.pptx.pdf#page=104&rect=79,32,627,347|T2 - MPEG y MPEG2.pptx, p.104]]

- Field/frame prediction modes for supporting the interlaced video input: Boring ahh
![[T2 - MPEG y MPEG2.pptx.pdf#page=109&rect=43,81,673,339|T2 - MPEG y MPEG2.pptx, p.109]]

## Scalability extension
![[T2 - MPEG y MPEG2.pptx.pdf#page=111&rect=11,84,707,294|T2 - MPEG y MPEG2.pptx, p.111]]
- From 1 input, 2 outputs

## Non compression enhancements
- DIsplay flags indicating chromatiity, subcarrier amplitude, phase (NTSC, PAL, SECAM)

 ## AUDIO
 **AAC**: Really awful

  # DVD (Digital Versatile Disc)
  - Allowed several resolutions and aspect ratios
  - PS2 uses it
