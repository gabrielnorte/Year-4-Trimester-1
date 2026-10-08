- Using huffman por compression (**lossless**) - GREEDY ALGORITHM

# Theory Recap
Take a single sinusoidal period, if we quantize it
![[Lab 2-1791290880974.webp]]
The error is the difference between both

```ad-info
A square wave is a special case than can be encoded with a single bit of information
- **That doesn't mean the entropy is the same for all square waves**
```

The entropy is not only a measure of the minimum amount of bits needed to encode, but also *a measure of uncertainty*
	A square wave that goes up less will have a lower entropy since it goes up with less probability

## Huffman codes
*Based on assigning shorter codewords to higher probabiliy symbols (volume values) and longer codewords to lower probability ones*

# SNR
The bigger the better, as it indicates there's more signal that noise
- More bits, precise discretization, less noise, higher SNR 
- Fewer bits, non precise discretization, more noise, lower SNR

# PDF and Entropy
![[Lab 2-1791293014233.webp]]
With a quantization of 8 bits, we have a total of $256$ volume values (on both negative and positive part)

```ad-warning
This visualization actually multiplies elevates the bits to the power of 2 a second time. So even though there should be 256 samples in total in the x axis (-128, 128), we have 512.
**This is the convention, though not the matematically correct one**
```

Sounds with a higher entropy (uncertainty of samples) like the one above will be harder to compress, as the tree will assign longer codewords due to the high amount of symbols with similar probability

Audios centered around zero will be specially easy to compress, given that most of the samples are concentrated along zero, thus a higher probability is assigned to them and we ca use smaller codewords for them, leading to compression

![[Lab 2-1791294392214.webp]]
![[Lab 2-1791294402138.webp]]

More spread out
![[Lab 2-1791294420590.webp]]
![[Lab 2-1791294436461.webp]]
More concentrated, even if it has more peaks there's no need to compress that much info (not as broad band in terms of available amplitude values that should be compressed)


