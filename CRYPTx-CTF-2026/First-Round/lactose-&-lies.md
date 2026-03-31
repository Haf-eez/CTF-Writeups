# 🥛 Lactose & Lies

**Category:** Steganography / Image Analysis  
**Difficulty:** Medium  

---

## 📌 Challenge Description

A seemingly harmless promotional image for a milk powder brand contained a hidden secret. Despite the high resolution ($2816 \times 1536$), initial automated scans revealed no obvious embedded files, suggesting the data was hidden in plain sight through visual distortion rather than file-level manipulation.

---

## 🔍 Solution Approach

### 🧩 Phase 1: Initial Forensic Sweep
Standard steganography tools were used to rule out common embedding techniques:

* **`binwalk` / `foremost`:** No hidden archives or secondary images were found.
* **`steghide`:** Attempted extraction failed (no passphrase provided).
* **`strings`:** The output was noisy and provided no immediate clues or flags.
* **Aperi'Solve:** Metadata and LSB (Least Significant Bit) analysis showed no anomalies.

**Conclusion:** The challenge was likely a visual/geometrical puzzle rather than a digital embedding.

---

### 🕵️ Phase 2: Visual Inspection
Upon closer manual inspection of the image, a distorted, pixelated pattern was identified in one of the corners.

* **The Observation:** A QR-like pattern was visible, but it was not a standard square.
* **The Distortion:** The pattern was stretched horizontally, appearing as a thin, long strip.
* **Dimensions:** The cropped region measured **$443 \times 68$ pixels**.



---

### ⚙️ Phase 3: Aspect Ratio Correction
Standard QR codes must be square to be readable by most consumer scanners.

* **Failed Attempt:** Used **ImageMagick** to compress the width back to a $1:1$ ratio (roughly $68 \times 68$ pixels). However, the resulting image was too blurry/degraded for standard phone scanners to recognize the alignment patterns.
* **The Realization:** The code wasn't just a "squished" standard QR; it was a **Rectangular Micro QR (rMQR)** code, a specific barcode standard designed for narrow spaces.

---

### 🔓 Phase 4: Decoding
Since most common mobile scanners do not support the rMQR format or heavily distorted inputs, a more robust forensic engine was required.

* **Tool Used:** **Aspose Barcode Recognizer**.
* **Result:** The engine's advanced error correction and support for non-square symbologies successfully processed the $443 \times 68$ strip.

---

## 🎯 Final Flag

```text
cryptx{r51t_mi1ro_qr_d51od5}
```

---

## 🧠 Key Takeaways

* **Don't rely solely on tools:** When `binwalk` and `steghide` fail, look at the image with your own eyes.
* **Symbology Knowledge:** QR codes aren't always square. Knowing about Micro QR and rMQR variants can save hours of fruitless resizing.
* **Scanner Capabilities:** Not all decoders are equal; specialized forensic or professional barcode tools can handle distortions that consumer apps cannot.
