# Pulse-Code-Modulation
# Aim
Write a simple Python program for the modulation and demodulation of PCM, and DM.
# Tools required
Google Colab
# Program
# PCM
```
import numpy as np
import matplotlib.pyplot as plt

# Time axis
t = np.linspace(0, 0.1, 1000)

# Message signal
fm = 50
msg = np.sin(2 * np.pi * fm * t)

# Sampling
fs = 1000
ts = np.arange(0, 0.1, 1/fs)
sampled = np.sin(2 * np.pi * fm * ts)

# Quantization
levels = 16
q_signal = np.round(sampled * (levels/2)) / (levels/2)

# Demodulated signal
demod = q_signal

# Clock signal
clock = np.sign(np.sin(2 * np.pi * 200 * t))

# Plotting
plt.figure(figsize=(10,8))

plt.subplot(4,1,1)
plt.plot(t, msg, 'b')
plt.title("Message Signal (Analog)")
plt.grid()

plt.subplot(4,1,2)
plt.plot(t, clock, 'g')
plt.title("Clock Signal")
plt.grid()

plt.subplot(4,1,3)
plt.step(ts, q_signal, 'r')
plt.title("PCM Modulated Signal")
plt.grid()

plt.subplot(4,1,4)
plt.plot(ts, demod, '--m')
plt.title("PCM Demodulated Signal")
plt.grid()

plt.tight_layout()
plt.show()
```
# DM
```
import numpy as np
import matplotlib.pyplot as plt

# Time axis
t = np.linspace(0, 1, 1000)

# Original signal
fm = 10
x = np.sin(2 * np.pi * fm * t)

# Delta Modulation
step = 0.1
dm = np.zeros(len(x))
demod = np.zeros(len(x))

for i in range(1, len(x)):
    
    if x[i] > demod[i-1]:
        dm[i] = 1
        demod[i] = demod[i-1] + step
    else:
        dm[i] = -1
        demod[i] = demod[i-1] - step

# Plotting
plt.figure(figsize=(10,7))

plt.subplot(3,1,1)
plt.plot(t, x)
plt.title("Original Signal")
plt.grid()

plt.subplot(3,1,2)
plt.step(t, demod)
plt.title("Delta Modulated Signal")
plt.grid()

plt.subplot(3,1,3)
plt.plot(t, demod, ':')
plt.title("Demodulated Signal")
plt.grid()

plt.tight_layout()
plt.show()
```
# Output Waveform
# PCM:
<img width="1265" height="992" alt="WhatsApp Image 2026-05-16 at 10 27 44" src="https://github.com/user-attachments/assets/895964d1-d0f8-4621-9f31-bb4f7626c2aa" />

# DM:
<img width="1261" height="862" alt="WhatsApp Image 2026-05-16 at 10 31 21" src="https://github.com/user-attachments/assets/e2156193-d006-4b81-b4d4-082f92744ff5" />

# Results
Thus, The output waveform of PCM and DM is verfied successfully.
