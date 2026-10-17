We will use an **omnidirectional** condenser microphone
- Can be sort of deduced by the shape
- BEING A CONDENSER, WE NEED TO PRESS THE 48V button

---

Sweep level is just the volume of the sweep

```ad-info
For calibration, only align input and loopback, output can be another level
- Check levels is just to check this
- Start calibration actually starts the sweep
```

## Delay compensations
Once a measurement is made, it indicates a delay. TO fix this delay, on the measurements menu we then set that *timing offset*
- This flattens the reponse and stabilizes the phase
- 
(Calibration is just a measurement but with less info (both still do sweeps), and it fixes the instability in the magnitude so that measurements done after are flat)

```ad-summary
Calibration always done before measurements to obtain all the magnitude irregularities. We then subtract those irregularities to obtain a flat response in a measurement.

1. Check levels (for volumes)
2. Calibration (will check irregularities)
3. Save calibration file
4. Start measurement with calibration file
```

Phase artifacts in Task 2's microphone recording are more due to the device rather than the setup



**Proximity efffects are more prominent in directional microphones (Gradient)**
