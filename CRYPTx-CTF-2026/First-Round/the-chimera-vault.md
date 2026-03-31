# 🏺 The Chimera Vault

**Category:** OSINT / Forensics / Crypto  
**Difficulty:** Medium/Hard  

---

## 📌 Challenge Description

The Chimera Vault was a multi-stage investigation tracing the digital footprint of "The Cyber Guardian." The objective was to uncover hidden artifacts across social media and version control systems to retrieve a secure archive override code.

The challenge required:
1. Social media intelligence gathering
2. Developer footprint tracking
3. Git version control analysis
4. Cipher identification and decoding

---

## 🔍 Solution Approach

### 🧩 Phase 1: The Social Media Pivot
The investigation began with a Reddit post containing a cryptic clue: *"Visit the society’s latest post… the next clue lies hidden just beneath it."*

* **Action:** Located the Society’s official Instagram page.
* **Discovery:** Inspected the comments section of the latest post.
* **Result:** Discovered the developer alias: `Guardian-Archivist`.

---

### 🖥️ Phase 2: Developer Footprint
Searching for the alias across developer platforms led to a GitHub profile.

* **Username:** `Guardian-Archivist`
* **Target Repository:** `Vault-Protocols`
* **Note:** This repository matched the description of a "dead drop" location.

---

### 🕵️ Phase 3: Git Forensics
While the repository appeared empty or "clean" at first glance, the hint *"Data is never truly gone"* suggested inspecting the **Commit History**.

* **Key Commits Found:**
    1. `feat(auth): implement secondary fallback cipher` (File added)
    2. `sec: EMERGENCY SCRUB - Remove fallback cipher` (File removed)
* **Action:** Checked the diff of the earlier commit to recover the deleted file.
* **Recovered File:** `key_directive.txt`

---

### 📜 Phase 4: Cipher Identification
The contents of `key_directive.txt` contained unusual symbols. A hint regarding *"obsidian and enchanting tables"* provided the necessary context.

* **Cipher Type:** Minecraft Enchanting Table Language.
* **Technical Term:** **Standard Galactic Alphabet**.

---

### 🔓 Phase 5: Decoding & Extraction
Using a Standard Galactic Alphabet translator, the symbols were converted into plaintext.

#### 1. Retrieve the Flag
The decoded text revealed the full flag:
`cryptx{secure_vault_pass_v4ult_0v3rr1d3_x7}`

#### 2. Extract the Override Code
The final step required identifying a specific 17-character password substring within the flag.
* **Target String:** `v4ult_0v3rr1d3_x7`

---

## 🎯 Final Answers

| Question | Answer |
| :--- | :--- |
| **Q1: Developer Alias** | `Guardian-Archivist` |
| **Q2: Repository Name** | `Vault-Protocols` |
| **Q3: Deleted File** | `key_directive.txt` |
| **Q4: Cipher Name** | `Standard Galactic Alphabet` |
| **Q5: Final Flag** | `cryptx{secure_vault_pass_v4ult_0v3rr1d3_x7}` |
| **Q6: Override Code** | `v4ult_0v3rr1d3_x7` |

---

## 🧠 Key Takeaways

* **Commit History is a Goldmine:** In forensics, "deleted" in Git only means "hidden from the current HEAD." Previous commits often contain sensitive keys or files.
* **Cross-Platform Pivoting:** Successfully linked Reddit -> Instagram -> GitHub.
* **Niche Cipher Recognition:** Recognized pop-culture references (Minecraft) to identify the Standard Galactic Alphabet.
