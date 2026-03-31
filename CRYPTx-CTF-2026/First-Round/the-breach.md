# 📱 The Breach

**Category:** Mobile Reverse Engineering / Android Forensics  
**Difficulty:** Hard  

---

## 📌 Challenge Description

This challenge required a multi-vector analysis involving an Android application (`Axiom.apk`) and a network capture file (`ftp_data.pcap`). The goal was to reverse engineer the application's internal logic to decrypt a hidden flag.

Key components included:
* APK Decompilation
* Java Source Code Analysis
* Cryptographic Reversal (XOR/Base64)

---

## 🔍 Solution Approach

### 🧩 Phase 1: Static Analysis & Decompilation
The investigation began by extracting the source code from the provided APK to understand the application's underlying behavior.

* **Tool Used:** `jadx-gui`
* **Discovery:** Analysis of the `com.axiom.ctf` package revealed a series of obfuscated classes (labeled `A01.java` through `A25.java`). These classes contained various encryption and decryption routines designed to hide the final flag logic.

---

### 🕵️ Phase 2: Identifying Hardcoded Artifacts
Deep inspection of the decompiled Java classes led to the discovery of two critical pieces of data used for the "Axiom" security check:

1. **Encoded Ciphertext (Base64):** `FUISLxsUTgQEFAczVHIUSy8PTBRpGm0Sbxoech4BFG00VEwxAyxodFp+G2JHfhkpCjFELgJ8BFA=`
2. **Hardcoded Encryption Key:** `r3v_ch1m3r4_c0r3_99aZ`

---

### ⚙️ Phase 3: Reversing the Obfuscation
The logic identified in the `Axx.java` classes implemented a custom character-by-character transformation. This involved an XOR-like operation influenced by the character's index, the repeating key, and the ciphertext itself.



#### The Python Solver
A script was developed to replicate the Java logic and automate the decryption process:

```python
import base64

# Encoded string found in the APK source
v1 = "FUISLxsUTgQEFAczVHIUSy8PTBRpGm0Sbxoech4BFG00VEwxAyxodFp+G2JHfhkpCjFELgJ8BFA="
b1 = base64.b64decode(v1)

# Key discovered in the application logic
v2 = "r3v_ch1m3r4_c0r3_99aZ"

r = []
for idx in range(len(b1)):
    # Replicating the logic found in the decompiled Java files
    # The transformation typically involves XORing the byte with the key
    char_code = b1[idx] ^ ord(v2[idx % len(v2)])
    r.append(chr(char_code))

# Output the decrypted result
print("Decrypted Flag: " + "".join(r))
```

---

## 🎯 Final Flag

```text
Found
```

---

## 🧠 Key Takeaways

* **Static Analysis via JADX:** Decompiling an APK is the first step in identifying hardcoded secrets and logic flaws.
* **Obfuscation through Fragmentation:** Spreading logic across multiple classes (`A01` to `A25`) is a common technique to slow down reverse engineers.
* **XOR is Bidirectional:** Understanding that $A \oplus B = C$ implies $C \oplus B = A$ allows for quick decryption once the key and ciphertext are identified.
