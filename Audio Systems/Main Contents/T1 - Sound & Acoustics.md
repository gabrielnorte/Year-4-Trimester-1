# Sound generation & propagation
It propagates in a longitudinal wave (same direction as the movement of vibration)
![[Lwave-v8.gif]]

In some other instruments, like drums, we can find **transversal propagation** instead, where the movement is perpendicular to the membrane

The **speed of sound** can be denoted as $\text{sound speed} = \sqrt{ \frac{\text{stiffnes}}{mass density} }$
- In gas, *depends on gas density*
- Temperature might affect as well

## Distance to source influence 
Following the inverse square law
$$I = \frac{QW}{4\pi r^2}$$
	$4\pi r²$: Omnidirectional radiation of sound
	

```ad-info
Doubling the distance: Reduces $I$ by 4, sound pressure by 2,  $-6 dB$
Doubling acoustic power: Multiplies $I$ by 2, soud pressure by $1.41$ = + 3dB
```

![[AES_T1_Sound_and_Acoustics_26-27.pdf#page=6&rect=35,91,678,426|AES_T1_Sound_and_Acoustics_26-27, p.6]]

See [[Spherical vs Cylindrical Radiation]]

# dB types clarification
## SPL vs SIL
**S**ound **P**ressure **L**evel indicates how lound a sound is in terms of **air pressure**. When using dBs, it is based on the minimum hearing level of 20 micropascals (SPL unit)
- Based on pressure reference point (20 $\mu P$)
**S**ound **I**ntensity **L**evel it's a logarithmic measure of sound intensity *in decibels*, computed through
- Based on intensity reference point ($10^{-12} W$)
$$SIL (dB)= 10\log_{10}\left( \frac{I}{I_{0}} \right)$$
Where $I_{0}$ is $10^{-12} W$, as the threshold of human hearing

```ad-danger
Note that log use in SIL. IT DOESN'T USE $20\log_{10}$, that corresponds to the conversion between volts and dB, this is different
```
```ad-info
$dB$ always correspond to a ratio, be it pressure or sound intensity. What changes is the log scale, if it squared or not, and the units it corresponds to
```
## dBx types
dB's a relative measure that depends on the original unit that was transformed in db.
- $dBV$: From volts to decibels $\to dBV = 20\log_{10}(V)$
	- Voltage needs squaring, leading to $10\log_{10}(V)^2$
- $dBW$: From watts to decibels $\to dBW = 10\log_{10}(W)$
- $dBu$: Similar to $dBV$ but the reference is  $7.75 Vrms$ instead of $1V$ $\to dBu = 20\log_{10}\left( \frac{V_{rms}}{0.775} \right)$
- $dBFS$: Digital measure, with maximum value $0 dBFS$ before it clips
	- Exclusively used digitally, and depending on the model. 0dBFS can mean different things
		- In SMPTE, it's 24 dB

```ad-caution
$V_{rms} = 0.707·V = \frac{V}{\sqrt{2}}$
SO  0.707 IS USED FOR THE CONVERSION WHILE 7.75 IS USED AS PART OF THE SCALING FACTOR IN LOG
```

```ad-important
On a fader, the dB gain or reduction can simply be added or reduced on any dBx unit, as they all share voltage units
```

![[T1 - Sound & Acoustics-1792488564404.webp]]
![[AES_T0_Basic_Concepts_26-27.pdf#page=7&rect=417,64,701,478|AES_T0_Basic_Concepts_26-27, p.7|350]]
## Sound field definitions
![[AES_T1_Sound_and_Acoustics_26-27.pdf#page=8&rect=29,14,684,453|AES_T1_Sound_and_Acoustics_26-27, p.8]]
The reason why pas the diffuse part is constant is because we assume that the room is closed, and even if we get far, we're still inside the room

## [Equal loudness test](https://www.phys.unsw.edu.au/jw/hearing.html)
How some frequencies, at the same volume, can be heard more or less than others. It follows the following curve
![[AES_T1_Sound_and_Acoustics_26-27.pdf#page=9&rect=24,47,441,282|AES_T1_Sound_and_Acoustics_26-27, p.9]]

# Weighted Levels
![[AES_T0_Basic_Concepts_26-27.pdf#page=6&rect=16,14,710,520|AES_T0_Basic_Concepts_26-27, p.6]]
- dBA correspond to sound measures that imitate the human hear
- dBB as the midpoint between A and C
- dBC has a flatter response and includes more low frequencies
- dBZ doesn't apply any filter

# Masking
![[AES_T1_Sound_and_Acoustics_26-27.pdf#page=11&rect=28,197,678,452|AES_T1_Sound_and_Acoustics_26-27, p.11]]
## Frequency Masking
Outside the masking range, when they're really close, we can hear frequencies as **beats**, with the beat frequency being $F_{1}-F_{2}$

On reaper, using a **goniometer** helps visualizing different sinewaves, *also including panning data*
- Beats can be visualized as a grid
![[AES_T1_Sound_and_Acoustics_26-27.pdf#page=11&rect=45,28,387,186|AES_T1_Sound_and_Acoustics_26-27, p.11]]

## Temporal Masking

# Goniometer / Vectorscope
- Out of phase sinewaves will form a circle

![[AES_T1_Sound_and_Acoustics_26-27.pdf#page=22&rect=111,152,604,451|AES_T1_Sound_and_Acoustics_26-27, p.22]]

# Comb filter
Slightly delaying the same signal we can essentially filter the signal due to phase cancellations
![[AES_T1_Sound_and_Acoustics_26-27.pdf#page=14&rect=75,32,643,432|AES_T1_Sound_and_Acoustics_26-27, p.14]]
- The dips indicate where the resulting filter suppresses the signal.
- The comb filter is just the combination of both signals slightly shifted in time

```ad-important
THIS IS THE SAME AS A FLANGER, IT DELAYS THE SIGNAL IN A SWEEPING WAY TO OBTAIN THE EFFECT
**Flanger:** Changes delay
**Phaser**: Changes phase
```
## Hass, Franssen and cocktail party effect
**Comb filtering**: When the delay is between 10 ms and 50 ms
**Hass effect**: Threshold of eco, signals delayed by >50ms create echo effect
**Franssen effect**
**Cocktail effect**: Spatial and spectral filtering allow intelligibility in noisy environments

```ad-tldr
title: Why echo happens past a threshold
Even though delaying the signal just a bit can be considered echo, some of these echoes will still cancel some frequencies, leading to comb filtering rather than the Hass effect.
With a delay of $50 ms = 0.05 s$ (which would be cancelling all frequencies with double the frequency $f = \frac{1}{0.05} = 20 Hz$, that is, $40 Hz$), which is already unhearable. Thus, past this delay, all the frequencies that get cancelled will be below 40 Hz, so instead of a cancellation, comb filtering effect, we would get a Hass effect
```

# Adding Levels
![[AES_T0_Basic_Concepts_26-27.pdf#page=8&rect=26,21,706,437|AES_T0_Basic_Concepts_26-27, p.8]]
The reason why simple addition doesn't work for coherent sources is due to the **log scale**
- Doubling will result  
# Absorbption, reflection, refraction and diffraction
For diffraction, some microphones count with a structure that doesn't let specific frequencies past

# Spatial treatments
## Room modes
Depending on the room size and dimensions, reflections are prone to occur in many different manners. That means, **we can find an infinite amount of frequencies whose wavelength match the dimensions of the room** - STATIONARY WAVELENGTH
- High pressure close to the walls

## Acoustic materials
- Perforated panels
- Helmholtz resonators
- Absorbers


## [QUIZ](https://docs.google.com/forms/d/e/1FAIpQLSciYVTAJnJEQrUc__rKA5IxUJ14__S9i5IvTATJSciTMJcFgw/viewform)
