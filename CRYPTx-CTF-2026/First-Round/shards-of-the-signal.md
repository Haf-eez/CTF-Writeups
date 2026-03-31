# 🧩 Shards of the Signal

**Category:** Cryptography / Data Manipulation  
**Difficulty:** Medium  

---

## 📌 Challenge Description

"The data is still intact, but the signal was split into small parts before it was sent. Decode it, inspect the numbers, and put each small block back in order."

The objective was to identify the encoding method, convert the data into a readable format, and apply a specific chunk-based transformation to reconstruct the flag.

---

## 🔍 Solution Approach

### 🧩 Phase 1: Encoding Identification
The provided data string consisted entirely of uppercase letters and numbers (A-Z, 2-7):
`GEZDCIBRGE2CAOJZEAYTEMBAGEYTMIBRGEZCANBZEAYTCMRAGEZDGIBV...`

* **Observation:** The character set and pattern are characteristic of **Base32** encoding.
* **Action:** Decoded the Base32 string to reveal a sequence of decimal numbers.

---

### 🔢 Phase 2: Data Conversion
The decoded output resulted in a series of integers:
`121 114 99 120 116 112 49 112 123 51 99 51 112 95 53 95 55 117 99 52 98 49 95 107 48 95 110 51 100 114 125 114`

* **Action:** Converted these decimal values into their corresponding **ASCII** characters.
* **Resulting String:** `yrcxtp1p{3c3p_5_7uc4b1_k0_n3dr}r`

---

### 🛠️ Phase 3: Signal Reconstruction
The raw ASCII string appeared scrambled. Following the hint *"split into small parts... put back in order,"* a chunking strategy was applied.

#### 1. Split into Chunks
The string was divided into 3-character blocks:
`yrc` | `xtp` | `1p{` | `3c3` | `p_5` | `_7u` | `c4b` | `1_k` | `0_n` | `3dr` | `}r`

#### 2. Reverse Each Chunk
Reversing the characters within each individual block revealed recognizable fragments:
* `yrc` → `cry`
* `xtp` → `ptx`
* `1p{` → `{p1`
* ...and so on.

#### 3. Final Assembly
Rejoining the reversed blocks formed the coherent flag:
`cry` + `ptx` + `{p1` + `3c3` + `5_p` + `u7_` + `b4c` + `k_1` + `n_0` + `rd3` + `r`

---

## 🎯 Final Flag

```text
cryptx{p13c35_pu7_b4ck_1n_0rd3r}
```

---

## 🧠 Key Takeaways

* **Base32 vs Base64:** Recognizing character sets (A-Z, 2-7) is vital for identifying Base32 without trial and error.
* **ASCII Fundamentals:** Always look for decimal sequences in the range of 32–126, as these often represent printable characters.
* **Chunking Patterns:** In "Scrambled" challenges, if the start of the string looks like a jumbled version of the flag format (e.g., `yrc` instead of `cry`), look for a repeating mathematical pattern like block-reversal.
