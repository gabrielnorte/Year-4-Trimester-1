Microphones can be classified in **acoustic terms**:
![[AES_T3_Sound_Capturing_and_Microphones_26-27.pdf#page=3&rect=94,153,601,230|AES_T3_Sound_Capturing_and_Microphones_26-27, p.3]]

By the transduction principle, we can also consider
- Electrodynamic microphones (passive)
- Electrostatic microphones (active)
- Piezoelectric microphones (active or passive)

```ad-info
Part of a microphone is a transducer, as it converts (sound) energy into (electrical) energy
```

# Electrodynamic microphones
## Moving Coil Transduction
The energy gets absorbed by the *diaphragm* of the microphone as waves, and then transferred through a magnet through a *voice coil*
- Reliable and strong
- Support over pressure
- Colored / Selective frequency response
- No phantom power (passive)
- Low output impedance

As cons however:
- Transients slow response - SEE [[Transient Response]]
- Low sensitivity
- Non flat tailored response
- Not the best frequency response - NOT TAILRED FOR RECORDING

*So, since it can support pressure better, we can scream more into the mic and the audio won't clip, which matches well with the fact that the microphone has a low sensitivity*

## Ribbon microphones
![[AES_T3_Sound_Capturing_and_Microphones_26-27.pdf#page=6&rect=56,137,636,378|AES_T3_Sound_Capturing_and_Microphones_26-27, p.6]]
## Ribbon Transduction
Due to the small and **light** membrane, the sensitivity is improved compare to the previous case

```ad-danger
Due to the small corrugated ribbon, loud soud can easily break it even without being connecteds
```
# Piezoelectric transduction
Used in acoustic guitar pickups, contact microphones or even violin bridges
They're just a material that generates a voltage when flexed or deformed
# Electrostatic Microphones
## Condenser microphones

---
![[AES_T3_Sound_Capturing_and_Microphones_26-27.pdf#page=13&rect=21,29,711,437|AES_T3_Sound_Capturing_and_Microphones_26-27, p.13]]


```ad-info
Different microphones provide different frequency responses, which means that, to obtain the voltage of the microhphone given a dBSPL input, we need to take into account
1. Frequency response
2. Microphone sensitivity
```

---
# Propagation shapes
```ad-important
For different frequencies, the cardiod shape can change
![[T3 - Sound and Capturing microphones-1792085169277.webp]]
	SM58
```
We will denote that
- **Gradient pressure microphones**: Directional microphones
- **Pressure microphones**: Omnidirectional microphones

These propagation types can also vary with the frequency, and microphones like the **AKG P420** have a switch to change it manually

## Distance and directivity factors
![[AES_T3_Sound_Capturing_and_Microphones_26-27.pdf#page=18&rect=80,88,651,460|AES_T3_Sound_Capturing_and_Microphones_26-27, p.18]]

## Proximity effect
For directional microphones, getting close to the object that emits sound will create a large increase on the low end. This is not present on omnidirectional microphones, which present a full band increase

# Characterizing freq. response with microphone types
All of the previous can be characterized through the frequency response
- Different frequency responses on the low end depending on distance - *DIRECTIONAL (GRADIENT PRESSURE)*
- 
```ad-important
Lab: Smaller echo delay for impulsive sound
```


# Dual diaphragm microphones
Using microphones with two different capsules, we can mix their cardiods and add them up
![[AES_T3_Sound_Capturing_and_Microphones_26-27.pdf#page=21&rect=48,30,707,401|AES_T3_Sound_Capturing_and_Microphones_26-27, p.21]]

See [[Special Applications]]

# Multichannel capturing
Using multiple microphones (or different capsules inside one microphone) going to one same input


# Inverse Square law and Relative Humidity
![[AES_T3_Sound_Capturing_and_Microphones_26-27.pdf#page=33&rect=171,123,553,452|AES_T3_Sound_Capturing_and_Microphones_26-27, p.33]]
The more humid the air


# Phantom power
Only for condenser microphones

**Unbalanced / Assymetric connection**, phantom power needs a balanced connection

*It's necessary to avoid external power getting through and affecting the PA power*


# Sensitivity measures
- Always done with 1 Pascal of pressure
- 1 m away
- At 1000 Hz

*For exercises, we will modify the sensitivity to adjust to the new values*
- Knowing the Pressure needed to obtain $x V$ if the sensitivity is $S_{V} = yV$: $\to yV·Pres = xV$  

```ad-example
![[T3 - Sound and Capturing microphones-1793830467259.webp]]
```
```ad-caution
ALL OF THIS OPERATIONS WON'T BE DONE WITH $dB's$ since we need linear units. If we really wanted to do it we would need to turn everything into $dB$ with log
```


See comparisons and such on [[T3.5 - Electro Acoustic Analogies]]