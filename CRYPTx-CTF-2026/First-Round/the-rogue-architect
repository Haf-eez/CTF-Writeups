# 🏗️ The Rogue Architect

**Category:** OSINT / Audio Steganography  
**Difficulty:** Hard  

---

## 📌 Challenge Description

The objective was to track down a rogue architect named **Kenji Tanaka**, recover his deleted deployment notes, locate a hidden decentralized portfolio, and extract a hidden flag from an encrypted audio file.

This challenge required a deep dive into:
* Digital archeology (Wayback Machine)
* GitHub forensics (Gists and Commit history)
* Audio signal processing (Phase inversion)
* Spectrogram analysis

---

## 🔍 Solution Approach

### 🧩 Phase 1: Digital Footprint Analysis
The investigation started with the alias `@kenjitanaka512`.

* **GitHub Profile:** Found `github.com/kenjitanaka512`. The README was wiped, claiming the "central servers are compromised."
* **Commit History:** Cloned the repo and checked `git log --all`. Only two commits existed, revealing no hidden files, but providing a crucial email: `kenji.tanaka@cryptx.lk`.
* **Dead Ends:** Multiple standard portfolio platforms (Fleek, Netlify, Vercel, Surge) and social media handles were checked but appeared empty or deleted.

---

### ⏳ Phase 2: Traveling Through Time
Since the developer mentioned wiping notes, the **Wayback Machine (web.archive.org)** was used to find "ghost" data.

* **The Gist Discovery:** Searching `gist.github.com/kenjitanaka512` in the archives revealed a deleted entry: `Chimera_V2_Deployment.md`.
* **The Clue:** The archived Gist contained Kenji’s manifesto. He refused to provide a "backdoor" and moved his portfolio to a hidden node.
* **Hidden URL:** `kenjit-dev.vercel.app`

---

### 🔊 Phase 3: Audio Steganography
Visiting the secret portfolio led to the discovery of a password-protected audio file: `EVIDENCE_RECORDING_404.wav` (identified as **Signal_Part2**).

#### 1. Decryption
The password discovered on the portfolio (`v4ult_0v3rr1d3_x7`) was used to unlock the file.

#### 2. Phase Inversion (Signal Cleaning)
The challenge required clearing "distortion" by combining two signals. Using Python, **Signal_Part2** was subtracted from **Signal_Part1** to cancel out the noise (Phase Cancellation).

```python
import numpy as np
import wave

# Load signals and convert to int32 to prevent overflow during subtraction
# Result = Signal_Part1 - Signal_Part2
result = frames1[:min_len] - frames2[:min_len]

# Normalize and save
result = np.clip(result, -32768, 32767).astype(np.int16)
```

---

### 🕵️ Phase 4: Spectrogram Extraction
The resulting "cleaned" audio still sounded like noise to the human ear. A **spectrogram** was generated to visualize the frequencies.

* **Tool:** Python `matplotlib.pyplot.specgram`.
* **Visualization:** By plotting the frequency over time, the flag appeared as clear, handwritten text within the image.



---

## 🎯 Final Flag

```text
cryptx{m4rg4d_ch7nn9ls_d04snt_14}
```

---

## 🧠 Key Takeaways

* **The Web Never Forgets:** The Wayback Machine is a primary tool for OSINT when a target attempts to "wipe" their history.
* **Phase Cancellation:** Destructive interference can be used in steganography to hide a clean signal inside two noisy ones.
* **Visualizing Sound:** Spectrograms are a common way to hide data in audio; if a file sounds like "static," always check the frequencies.
