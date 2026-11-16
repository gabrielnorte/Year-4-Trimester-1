# Audio Transmission
We want to achieve the best signal fidelity at each step (input, preamp, mixer, ...). On a higher level:
- *Low level*: Input & Input gain 
- *Line level*: EQ, channel level, mixer output
- *Power level:* Speaker

## Noise sources
- Inherent Noise in the Audio Signal
- Noise from Analog Equipment
- Noise from Power Amplifier Gain
- Poor Wiring
- Ground Loops
- AC Line Noise
- Radio Frequency Interference
- Computer Noise
- Transformer Noise

```ad-note
Noises can be classified based on their sound:
- **Hum**: Steady low freq sound (50Hz-60Hz) without significant harmonics
- **Buzz**: Steady-state noise with many harmonics (Touching jack tip when plugged to amp)
- **Hash**: Pulsating buzz type noise
- **Hiss**: Similar to white noise but higher pitch, often like steam or rain or a rooftop
``` 

# Conductor cables
Conductor cables are the simplest elements in a circuit, though they can introduce response problems at the frequency extremes due to their *design, length, and the circuitry to which it's connected*

See [[Connection Setups - Balanced and Unbalanced]]

## Treating noise
Denoting *electrical noise and electromagnetic interference* as *EMI*, we combat it with a **SHIELD** on the cables.
The shield surrounds the inner signal
- Reflects energy
- Conducts noise to ground
![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=16&rect=53,61,683,292|AES_T5 - Audio Transmission and Impedance Matchin, p.16]]

**Shielding can have a negative impact on the cable though**, as it increases the capacitance.
- Cables have both inductance and capacitance (around $40pF / 30 cm$)
![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=19&rect=39,40,669,275|AES_T5 - Audio Transmission and Impedance Matchin, p.19]]

```ad-info
![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=17&rect=49,16,664,443|AES_T5 - Audio Transmission and Impedance Matchin, p.17]]
```

## Twisted Pair
Another possible cable that is often used are twisted pair cables. They're two conductors on a single circuit that are twisted for improved electromagnetic compatibility
*It reduces electromagnetic radiation from the pair and crosstalk between neighbouring pairs and improves rejection of external electromagnetic interference.*

```ad-info
Without twisted pairs, nearby conductors can cross-talk and create interferences with each other
```

## Balanced and unbalanced cables
**Unbalanced cables** (RCA, TS)
- Susceptible to interference and signal loss 
- Keep under 6.1 m (20 feet)
**Balanced cables** (XLR, TRS)
- Counteract interference
- Can run much longer without signal loss
- Usually good under 30.5 m (100 ft)
- ==🟢Can provide phantom power==
**Speaker cables**: The length can play a role, especially regarding resistance. The more resistance is introduced, the thinner the cable and the longer the run. This is why it’s essential to choose thicker gauge cables for longer runs. No interference issues for the voltage range in loudspeaker signals.
	Based on $R = \frac{KL}{d^2}$
# Connectors
**Single ended / Assymetrical / Unbalanced (Consumer use)**
- RCA
- Tip Sleeve (*TS*)

**Differential / Symmetrical / Balanced (Professional use)**
- XLR
- Tip-Ring-Sleeve (TRS)

```ad-info
A single TRS cable can carry stereo information, as it is formed by 2 TS cables
- Each TS cable carries mono information from each channel
- Each TS is separated from each other
- All mixed into a single TRS cable, creating TS1-TRS and TS2-TRS connections
  
https://www.instagram.com/reel/DEs_3u2gh0_/?igsh=MWxjenFiaWI2Y21kdQ%3D%3D
```

Given that both XLR and TRS use 3 pins, they are related as follows

| XLR   | TRS    | Signal | Wire   |
| ----- | ------ | ------ | ------ |
| Pin 1 | Sleeve | Ground | Shield |
| Pin 2 | Tip    | +      | Red    |
| Pin 3 | Ring   | -      | Black  |
```ad-caution
Remember unbalanced circuits, that sent the seignal with inverse polarity, that's the + and - signal above (sent by tip and ring respectively ¡)
```
# Ground
Ground is a shared reference node between all parts of a circuit
- No voltage difference unless $\underline{Z_{g}}$ is considered
![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=23&rect=55,22,675,357|AES_T5 - Audio Transmission and Impedance Matchin, p.23]]

| Grounding type                                                                                                                                                                    | VIsualization                                                                                                                                         |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| *Earth or signal ground*:<br>the return current path of a signal current back to its source.                                                                                      | ![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=24&rect=470,343,646,445\|AES_T5 - Audio Transmission and Impedance Matchin, p.24\|180]] |
| *Functional ground:* A ground for other purposes than electrical safety, e.g., for mitigating EMC and EMI issues                                                                  | ![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=24&rect=460,241,659,339\|AES_T5 - Audio Transmission and Impedance Matchin, p.24\|180]] |
| *Safety ground:* means the ground of an electrically conductive chassis or electric circuit, which protects humans against shock hazards and the electric circuit from ESD pulses | ![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=24&rect=463,123,656,233\|AES_T5 - Audio Transmission and Impedance Matchin, p.24\|180]] |
| *Chassis ground:* it refers to the connection that establishes an electrical link to a metallic enclosure. For instance, cable shields are usually connected to chassis ground.   | ![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=24&rect=481,29,639,118\|AES_T5 - Audio Transmission and Impedance Matchin, p.24\|180]]  |
## Ground loop
A ground loop occurs when a ground can be reached by more than one path, leading to a physical loop around the ground
This might occur due to careless layout, accidental or unexpected ground connections, or when two or more appliances are connected together

![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=25&rect=446,14,692,457|AES_T5 - Audio Transmission and Impedance Matchin, p.25|300]]

## Ground lift
Ground lift or earth lift is a technique used to reduce or eliminate ground-related noise arising from ground loops in audio cables.
Opens the connection between the equipment ground and the shielding conductor of audio cables attached to the equipment, leaving those cables grounded only at their opposite end, meaning, *each equipment will have its own ground*

Professional equipment used for balanced circuits often include a **ground lift switch**, eliminates unwanted hum and buzz by interrupting the ground loops between equipment, preventing current flow along the cable shield between two devices.

```ad-example
In XLR cables, this disconnects pin 1, but this is not the only ground source.
The cable already provides a ground, but PIN 1 creates an additional ground connection that forms a ground loop.
By activating the ground lift switch, pin 1 gets disconnected from this ground loop and the microphone then only depends on the cable ground
- We can't only depend on the cable ground though, as PIN 1 also provides a **shield**, which might reduce noise even more efficiently

If the noise is due to the ground loop, we will lift the switch, and as long as this doesn't create noise due to the lack of shield we're good. On the other case, we might have a bit more noise with the ground lift switched since we now rely on the cable ground

---
- In XLR cables, pin 1 connects the cable shield to the equipment chassis.
- However, the equipment also has its own protective earth connection.
- Connecting two pieces of equipment through pin 1 can create an additional conductive path between their chassis, potentially forming a ground loop.
- By activating the ground lift, pin 1 is disconnected at one end, interrupting this unwanted current path.
- The audio signal continues through pins 2 and 3, and the equipment retains its protective earth connection.
- However, disconnecting pin 1 can reduce the effectiveness of the cable's shielding, potentially making the audio signal more susceptible to electromagnetic interference.
  
A ground lift doesn't necessarily make the shielding ineffective. The shield remains physically around the conductors, and its connection at the other end remains intact. The actual impact depends on the equipment's grounding and shielding design.
```


# Phantom power
Phantom power is required for many microphones, especially professional condenser and active direct box types
Usually a *48 Vdc* power supply applied to both polarities of the differential input (**ONLY FOR BALANCED**) through 6.8 k polarity
![[AES_T5 - Audio Transmission and Impedance Matchin.pdf#page=32&rect=19,29,717,238|AES_T5 - Audio Transmission and Impedance Matchin, p.32]]

# Direct injection Box
A DI box (direct input or direct inject) is used to connect a high output impedance unbalanced output signal to a low-impedance, microphone level, balanced input
**Active:** Based on a preamp (NEEDS PHANTOM)
**Passive**: Transformer isolation