L```python
def display_spectrum(sound_array, hop_size=256, fft_size=512, sampling_rate=44100)
```
- Treats fft size as window size (**window size = fft size**)


```ad-tip
title: Remember
- Smaller window: Higher time resolution, less frequency resolution (less samples)
- Bigger window: Lower time resolution (covering more space), higher frequency resolution (more samples )
```
