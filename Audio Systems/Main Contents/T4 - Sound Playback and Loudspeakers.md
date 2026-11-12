# Loudspeaker classification
## Moving-coil cone radiator
![[T4_Sound Playback and Loudspeakers_26-27.pdf#page=3&rect=125,144,649,458|AES_T4_Sound Playback and Loudspeakers_26-27, p.3]]
The area above and under the coil are polarized, and around the center coil there's a magnetic field rotating
	Dust cap: Not only avoids dust, but also directs the sound in a convex manner
![[T4_Sound Playback and Loudspeakers_26-27.pdf#page=4&rect=63,14,697,454|T4_Sound Playback and Loudspeakers_26-27, p.4]]
- The triangle going from small to big helps waves 

## Ribbon drivers
Just as in microphones, there are dynamic microphones that use ribbons
- Inducing a magnetic field on the two magnets moves the coil and creates the sound

This type of speakers provide a slope that is first -3dB/oct and then -6dB/oct


## Heil Transformers (Air Motion Transfers)
![[T4_Sound Playback and Loudspeakers_26-27.pdf#page=6&rect=37,38,678,432|T4_Sound Playback and Loudspeakers_26-27, p.6]]
It uses an "accordion" type system in which motion caused by the audio signal goes through the accordion, creating distortions.

```ad-info
title: Ribbon vs Heil
Ribbon: Membrane movement between magnetic waves
Heil: Movement through accordion membrane causing deformations between magnetic waves
```

## Planar Magnetic radiators
Emitting on a plane membrane

## Electrostatic radiators 
Full range radiation, works through air compression and others

## Distributed Mode Loudspeakers
The entire surface of the DML panel vibrates
- Different exciters generate different modes of vibration

## Piezoelectric Radiators
Sound based on acoustic impedance and the surface of the piece itself

## Horns
They're just amplifiers (through impedance matching) that also direct sound 
- They can be coupled with speakers to increase sound power
![[T4_Sound Playback and Loudspeakers_26-27.pdf#page=15&rect=42,25,687,458|T4_Sound Playback and Loudspeakers_26-27, p.15]]
```ad-info
Even with a lot of power, only between 1% and 5% of it comes out as sound on a speaker, making horns a lot more useful
```

Since destructive interference happen, the sound will get amplified but the sound will be worse, hence the following frequency response
![[T4_Sound Playback and Loudspeakers_26-27.pdf#page=16&rect=24,11,706,474|T4_Sound Playback and Loudspeakers_26-27, p.16]]

## Frequency range classification
![[T4_Sound Playback and Loudspeakers_26-27.pdf#page=17&rect=33,8,667,449|T4_Sound Playback and Loudspeakers_26-27, p.17]]

## Mounting influence
The way the speaker is mounted (not the enclosure) also affects the output
- Free air = dipole effect (cancellation occurs due to opposite sides radiating opposite power)
# Loudspeaker enclosure
![[T4_Sound Playback and Loudspeakers_26-27.pdf#page=19&rect=13,8,693,456|T4_Sound Playback and Loudspeakers_26-27, p.19]]
## Bass reflex enclosures
![[T4 - Sound Playback and Loudspeakers-1794394304811.webp]]
They're enclosures with a dedicated opening for specific frequencies
![[T4 - Sound Playback and Loudspeakers-1793647351620.webp]]
```ad-question
What's the sense behind resonances happening on both maximum and minimum impedances?
It would make sense for resonance to occur when impedance is at its minimum, since there's less opposition
```

## Sealed box enclosure
Like the KRK speaker, it's just a speaker with no extra openings, just the output membranes

```ad-info
**For speakers, resonance is achieved when maximum impedance happens. Even though less current travels**
```

## Sealex box & Bass Reflex Plotted
![[T4 - Sound Playback and Loudspeakers-1794398665405.webp]]
**Phase**: ALWAYS CROSSES ZERO AT THE PORT RESONANCE FREQUENCY 
- Look at shape (peaks and dips) to determine if phase corresponds to bass reflex or sealed box


## Passive radiators and Band Pass enclosure
Just with the enclosure, we can obtain either radiators or band pass filters due to the enclosure shape
- Depending on the shape, the added radiance created by the enclosure depends on the wavelength and the actual enclosure bounds
# Specifications
![[T4 - Sound Playback and Loudspeakers-1793642817561.webp]]
## Sensitivity
For speakers:
- Measured at 1 m
- 1 KHZ
- 1W

The resulting SPL is the sensitivity, though it's still important to differentiate **vertical and horizontal sensitivity** - LIKE THE CARDIOD SHAPE IN MICROPHONES
- Rotating the speaker will yield different responses, just like when rotating the microphone
```ad-info
The sensitivity is always measured on-axis, so that the wavelengths look the same at that point. Even looking straight, the enclosure might direct the sound somewhere else, so on-axis means taking this into account
- Modern systems usually clarify this or make the waves in-phase when they reach a micophone on axis
```

![[T4 - Sound Playback and Loudspeakers-1793642596638.webp]]

- The angle just indicates where the sound is heard the best ($\approx$ same frequency response)
- It doesn't have to do with horizontal sensitivity

## Horizontal / Vertical Directivity
What was said before, not all speakers handle directivity the same, some speakers can direct on a wider range than others
- It can be controlled with **horns**


# Crossovers
They arise from the need to separate audios into different bands to send them to different channels (Tweeter, bass, ...)
- Passive crossovers - *After amp*
	- Capacitor, resistors, inductors, ...
- Active Crossovers  - *Before amp*
	- Separate with an active two way filter, then sent to a power amplifier with different drivers

They are both circuits, but one uses passive components and the other active ones, so the only differences is in the setup:
![[T4 - Sound Playback and Loudspeakers-1793643675804.webp]]
	Due to the high amount of impedance components on the passive circuits, there's a lot of power consumption
# Subwoofer alignment
Aligning subwoofers is important for various acoustic and physical reasons
- Radiation should usually go to the public, while minimizing to the stage to avoid unnecessary rumbling
	- *STACKED* and *SEPARATED* woofers work best for this (in opposite directions with opposite phase, aligned to have same waves)

# Onstage monitoring
As said  in [[T1 - Sound & Acoustics]]]], line arrays benefit from cylindrical radiation, thus more power radiated with less distance falloff
![[T4 - Sound Playback and Loudspeakers-1793646442198.webp]]

# Loudspeaker connection
A good balance is series-parallel, as it avoids the issue of extremely high current at the cost of low impedance

For speakers:
- **Series**: Sum of impendances
- **Parallel**: $\frac{\text{Sum of Impedances}}{\text{nº speakers}}$
Parallel connections end up being less costly in terms of impedance, even with many speakers
- Thus we can obtain more $W$ while the $V$ is kept constant
- $I$ is increased to compensate and verify $W = VI$
	- THIS CAN BURN THOUGH (HIGH CURRENT)
	- Abusing parallel speakers might create **way too much current, which is a problem**



 
