# 🔐 Brute... Brute...

**Category:** Forensics / Password Cracking / Steganography  
**Difficulty:** Medium  

---

## 📌 Challenge Description

We were given a password-protected ZIP file named `protected.zip`.  
Direct extraction was not possible without the correct password.

The objective was to:
1. Crack the ZIP password  
2. Analyze the extracted contents  
3. Retrieve the hidden flag  

---

## 🔍 Solution Approach

### 🧩 Phase 1: Breaking the Archive

Since the ZIP file was password protected, we first needed to extract its hash and perform a brute-force attack.

#### 1. Extract ZIP hash

```bash
zip2john protected.zip > hash.txt
````

#### 2. Crack the password

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

✅ **Password found:** `tsu132009`

---

### 🧪 Phase 2: File Analysis

With the password, we extracted the contents of the archive:

```bash
unzip protected.zip
```

Inside the archive, we found:

* `unknown.jpg`

#### Metadata inspection

```bash
exiftool unknown.jpg
```

The metadata appeared normal, with no hidden clues in fields like comments or author.

---

### 🕵️ Phase 3: Steganographic Extraction

Since metadata analysis did not reveal anything useful, we suspected hidden data within the image.

#### Extract hidden data

```bash
steghide extract -sf unknown.jpg
```

This successfully extracted:

* `flag.txt`

#### Read the flag

```bash
cat flag.txt
```

---

## 🎯 Final Flag

```
cryptx{darkc1cle_tw1ce_2st3p7_h1dden_lay3r}
```

---

## 🧠 Key Takeaways

* Used `zip2john` + **John the Ripper** for password cracking
* Verified file metadata using `exiftool`
* Extracted hidden data using `steghide`
* Learned to check multiple layers (archive → file → embedded data)
