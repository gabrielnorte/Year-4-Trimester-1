### Single ended / Unbalanced / Assymetrical
- One wire carries a varying voltage (AC)
	*ANALOG HIGH (+)*
- Other wire connected to ground (reference voltage, usually $0$)
	*GND (-)*

All inputs must share these connections

## Differential / Balanced / Symmetrical
Sends the same signal as a differential pair of signals
- One wire carries a voltage signal
- One wire carries the same signal with opposite polarity (same magnitude)

The receiving circuit responds to the difference between the two signals, resulting in a **twice as large signal**
	(Also requires a shared GND)


![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=12&rect=47,26,682,427|AES_T5 - Audio Transmission and Impedance Matchin, p.12]]
	Single ended (**Everything sent to input +, then GND is shared**)
	Differential (Two pairs of +- inputs for each channel, GND is shared)


### Advantages
- Doubled signal voltage between the differential pair (6dB of extra headroom) (2 times the voltage)
- Common-mode and RF noise is easily rejected by a differential receiver, thanks to the electrostatic shielding.
- Longer cable runs are possible due to this increased noise immunity and 6 dB extra headroom
# Balanced and unbalanced circuits
In circuits, the concept of balance and unbalanced is clearer
![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=14&rect=112,17,609,449|AES_T5 - Audio Transmission and Impedance Matchin, p.14]]