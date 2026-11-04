# Autoencoder

The whole process is simplified to making the **output** of a chain similar to the **input**
- The *stride* indicates how much a downsampling will be applied

In normal compression, we would separate the signal into different band pass filters and then downsampled individually. With CNN now, we apply FIR filters to the signal (which are changed through learning) and then downsampled by the stride

In a CNN architecture, we visualize it by the signal being convolved with x number of FIR filters and then downsampled by the stride.  **To extract higher level features, we applt more filters with different latent channels (amount of signals after conv)**

```ad-important
Between convolutions, signals are not reversible
```

**THE LATENT SPACE IS THE SIGNAL THAT IS THE MOST COMPRESSED**

For now, the autoencoder and previous tests did not perform any quantization
(To update the EPOCHS, two cells have to be ran before running the actual output cell, one that changes the EPOCHS and one that trains the model with those epochs)
# EnCodec and RVQ (Residual Vector Quantization)
- Doesn't work well with white noise and high frequency content

From one latent representation, it gets quantized with a single vector using the RVQ
- Codebooks $\approx$ 10 bits

`.ecdc`is enCodec format
