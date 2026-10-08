![[Spectrogram visualization of STFT and MDCT-1791385471316.webp]]
MDCT focalized the information in less locations, which makes it much easier to see which are the fundamental sinusoids, compared to the STFT, which includes many frequencies around it 

```ad-danger
MDCT doesn't provide more frequency resolution, the only thing is did is "clean up" the frequencies around the fundamental sinusoids
```

MDCT does have noise, but it's in the magnitude of $e^{-14}$

```ad-missing
Check audio of MDCT output, try to look for the distortion
```
