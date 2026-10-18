# Electric Current
The current $I$ is the rate of the flow of electrons. Thus, current is created when there's a difference of charges (potential energy) between ends of a conductor.
In a conductor:
$$i(t) = \frac{dq(t)}{dt}$$
![[AES T2 - Basic Electronics.pdf#page=10&rect=89,26,670,226|AES T2 - Basic Electronics, p.10]]

```ad-note
While mathematically we consider **instantaneous current $i(t)$**, current is usually constant in DC and AC circuits, thus we often consider $I$ in Amps instead
```

- > Current, faster charge flow
- Smaller cable cross section, faster the wire flow rate
- < Density, higher the speed

## Types of current
- **Alternating current AC**: Current that fluctuates in a sinewave (depends on power lies frequencies)
	- Can be used along transformers and capacitors
- **Direct current DC**: Constant current
	- DC can't be used on transformers as these require alternating power for induction

*Both can coexist in one same wire without issues*

See [[Electric Current vs Electro Magnetic Potential]]

# Main Components in Electronics
**Passive elements:** Can only receive energy, which it can either dissipate or absorb. Their controlling function is linear.
- Resistor
- Capacitor
- Inductor
- Transformer
- Diode
**Active elements**: Supply energy to a circuit, and hence has the ability to electrically control the flow of charge. Their controlling function is nonlinear.
	(Need energy to function properly, like some microphones. *Their usability is not only limited to consumption, but using that energy for something, enabled by the input current*)
- Vacuum tube
- Transistor
- Operational Amplifiers
## Resistors 
*Opposes the passage of electric current by transforming it into heat without phase shifts*
- Friction causes voltage difference, though current is kept, just that its speed gets regulated

![[AES T2 - Basic Electronics.pdf#page=17&rect=268,33,483,248|AES T2 - Basic Electronics, p.17|300]]
## Capacitors
*Polarized component, stores potential energy from one side and then releases it (charge/discharge process)*
- Two conductors separated by a dielectric $\varepsilon$
- Capacitance $C$ in Faradays
$$C = \varepsilon_{0}\varepsilon_{r}· \frac{A}{d} = \frac{Q}{V}$$
- Capacitor tends to an open circuit due to charge/discharge
![[CapacitorCircuit.gif|300]]

$\tau$ is used to denote the charge and discharge time constant, defined by $\tau = RC$ on a circuit with just a resistor and a capacitor (as resistive and reactive components). 
![[AES T2 - Basic Electronics.pdf#page=18&rect=25,19,720,460|AES T2 - Basic Electronics, p.18]]
*Charging a capacitor*: + Voltage, - Current (current decays until circuit stops)
$$V_{\text{C}}(t)=V_{0}\cdot (1-e^{-t/\tau }) \quad \quad I(t) = I_{0}(e^{-t/\tau})$$

*Discharging a capacitor*: - Voltage, + Current (current goes back to normal as voltage is released)
$$V_{\text{C}}(t)=V_{0}\cdot (e^{-t/\tau }) \quad \quad I(t)=I_{0}\cdot (1-e^{-t/\tau })$$

$\tau$ indicates when charging variable is at 63.2% and discharging variable is at 36.8%
$V_{C}(t)$ and $I_{C}(t)$ have a $\frac{\pi}{2}$ phase shift

```ad-hint
Will be seen later, but due to the filter behavior of these circuits in audio, the time constant can also be defined in terms of the cutoff frequency
$$\tau = RC = \frac{1}{2\pi f_c}$$
```

## Inductors
*Due to the flow of electric charges, a proportional magnetic field appears and opposes the change of electric current in the circuit*
- When the battery is turned on, the inductor opposes the rapid change. Due to this, current changes slowly and the opposing magnetic force reduces (fade in current)
- When the battery is turned off, the inductor opposes the rapid change by adding more. Thus current changes more slowly and reduces slowly (fade out current)
[Simulation](https://www.falstad.com/circuit/circuitjs.html)


- Measured in $H$, **inductance** is $L = \frac{B}{A}$
- $\tau$ indicates the speed of response of the device (how fast it reacts to current change), and $\tau = \frac{L}{R}$
![[AES T2 - Basic Electronics.pdf#page=21&rect=23,27,710,297|AES T2 - Basic Electronics, p.21]]

Thus, the curves correspond to the circuits current fading in or out and the magnetic charge opposing the force with more or less intensity

# Series and parallel
![[AES T2 - Basic Electronics.pdf#page=23&rect=53,36,696,395|AES T2 - Basic Electronics, p.23]]

```ad-important
An **LC** circuit will present oscillatory behavior:
- Capacitor releases charges, current suddenly increases so gets slowed down by inductor. Once current fully passes, it gets stored and released from the other side of the capacitor, and the suddent release is also faded by the inductor
```
# Induction
Refers to how an electric current can be induced in any conductor when there's a change in the magnetic flux and viceversa. It also occurs when the conductor changes with respect to a constant magnetic flux

```ad-example
### Transformer
Works by mutual induction process
$$W_P = V_PI_P = W_S = V_S I_S$$

Energy is induced between the primary and secondary coils (separated, induction through air medium)
- DC since a constant current will not induce a magnetic current

Power ratio is then determined between the **number of wires in each coil**, which affects the **voltage, resistance and current ratio**
![[AES T2 - Basic Electronics.pdf#page=28&rect=23,39,712,447|AES T2 - Basic Electronics, p.28]]
```
# AC Signal
## Impedance $Z$
$$Z = R+jX_{t}$$
$$|Z| = \sqrt{ R²+X_{t}^2 }$$
- $R$: Sum of resistors in the circuit
- $X_{t}$: Reactance of the circuit (equivalent to the sum of inductance $X_{I}$ and capacitance $X_{C}$)
![[AES T2 - Basic Electronics.pdf#page=32&rect=30,29,678,443|AES T2 - Basic Electronics, p.32]]

```ad-info
### Reactance
Reactance is the equivalent sum of inductors and capacitors in series or parallel.
- Series: Inductors sum as resistances / Capacitors sum as in parallel
- Parallel: Inductors sum as resistances / Capacitors sum as in series
```

# Passive Filters
The filter order is defined by the amount of *reactive* (L or C) elements. And the slope is:
- 1st order: 6dB / oct
- 2nd order: 12 dB / oct
- ...
*Quality factor (Q) defines the bandwidth of the filter and is expressed as the ratio between the reactance and the resistance of the filter*

```ad-info
For any filter, the cutoff starts once it goes down -3dB from the normal pass 
```

## RC Circuits
![[AES T2 - Basic Electronics.pdf#page=37&rect=81,27,671,447|AES T2 - Basic Electronics, p.37]]

## RL Circuits
![[AES T2 - Basic Electronics.pdf#page=38&rect=79,30,682,450|AES T2 - Basic Electronics, p.38]]

# LC / RLC Circuits
## LC Circuit $\approx$ Resonator 
A circuit that creates resonance at a specific frequency with an inductor $L$ and a capacitor $C$
As said before, this circuits oscillates, and it's oscillation frequency depends on both $L$ and $C$, and depending on the quality factor, this can ressemble a band pass or a narrow peak

## Passive Filters
![[AES T2 - Basic Electronics.pdf#page=42&rect=82,5,687,447|AES T2 - Basic Electronics, p.42]]
![[AES T2 - Basic Electronics.pdf#page=43&rect=74,14,688,450|AES T2 - Basic Electronics, p.43]]
```ad-important
$f_r$ stands for the resonance frequency. Thus, even though it's a bandpass, the cutoff frequencies for HPF and LPF are not specifieid
```

# Transformers
A component separated by a primary (input) and secondary coil (output), both with a voltage. Transformers essentially transform the input voltage $V_{P}$ to output voltage $V_{s}$, which can be higher or lower depending on the number of wire loops.
- With the number of wire loops being constant, **it can be adjusted through taps**
```ad-info
Taps exist to avoid changes in the output (secondary coil) when $V_p$ changes.
Taps change the effective number of turns in a transformer winding, not the physical number of turns that have been wound.
```

We find:
$$\frac{V_{P}}{N_{P}} = \frac{V_{S}}{N_{S}}\quad \quad \frac{I_{S}}{N_{P}} =\frac{I_{P}}{N_{S}} \quad \quad Z_{S} = \left( \frac{N_{S}}{N_{P}} \right)^2Z_{P}$$
$\frac{V}{N}$ is often denoted as Volts / turn

On the most simple cases, the ratio is denoted by:
$$x_{1}:x_{2}$$
- $x_{1}:$ Original voltage (primary coil)
- $x_{2}$: Voltage at the output (secondary coil)

