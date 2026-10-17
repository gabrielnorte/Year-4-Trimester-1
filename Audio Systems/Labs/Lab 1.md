 ![[Lab 1-1791477711906.webp]]
	 **Preamps** are the volume knobs at the input (controlling input volume)
	 **Amp** are the volume knobs at the output, usually connected to external hardware with their own volume knobs
	 **Inst** button just adapts impedance so that the input is appropiate for an instrument sound

After the firmware (a software that indicates how the device works internally), *data gets turned from analog to digital*

==🔵Firmware is inside the device, driver is inside the PC, translating what the firmware does  to the PC==

```ad-info
The sub channel is just an additional "master" channel,. Multiple tracks can be sent into sub, though they're sent to master by default
```

# Transfer Function - Frequency Response
![[Lab 1-1791478826799.webp]]
An input passed by the output goes through a transfer function, and its frequency response is the steady-state response of a system to sinusoidal inputs of varying frequencies

$$H(w) = \frac{Y(w)}{X(w)}$$
The frequency response is the "change" in frequency added to the frequency distribution of the input $X(w)$ so it becomes the output $Y(w)$

---
# REW
![[Lab 1-1791479677892.webp]]
Timing reference set to $L$ (the first one)
- Will indicate the arrival time of the signal

```ad-info
Loopback refers to how we connect the output of the focusrite to its own input. This is to measure the "clean" signal with no distortion aside from the one introduced by the interface.
This cable setup can be done internally but also externally, and it should match with REW's L & R settings
```
