# 🧅 Magic Peeler

**Category:** Forensics / Archive Analysis  
**Difficulty:** Medium

---

## 📌 Challenge Description

"Looks simple on the surface, but there's more beneath. Keep peeling."

We were provided with a single file named `Archive`. The hint suggested that the file contained multiple nested layers, similar to an onion. Each time a layer was extracted, another compressed file was found inside, requiring a repetitive or automated extraction process.

---

## 🔍 Solution Approach

### 🧩 Phase 1: Manual Inspection

Initial analysis was required to understand the structure of the nested layers and the types of compression used.

#### 1. Identify the file type
Even without an extension, the `file` command reveals the true nature of the data.
```bash
file Archive
# Output: Archive: gzip compressed data, last modified: ...
```

#### 2. Initial Extraction
Renaming and decompressing the first few layers manually:
```bash
mv Archive Archive.gz
gunzip Archive.gz
file Archive
# Output: POSIX tar archive

tar -xf Archive
ls
# Result: flag.txt (Fake!), data
```

#### 3. Identifying the Loop
Upon checking the `data` file, it was another `Zip archive`. Further extraction revealed even more layers (bzip2, lzip, xz). At this point, it became clear that manual extraction was inefficient due to the sheer number of "fake" flags and layers.

---

### ⚙️ Phase 2: Automation (The Script)

To "peel" the archive to its core, a Bash script was written to detect the file type and apply the correct extraction command automatically in a loop.

```bash
#!/bin/bash
# Automation script to peel the onion layers

while true; do
    TYPE=$(file data_work | awk '{print $2}')
    echo "Current Layer Type: $TYPE"

    case $TYPE in
        gzip)
            mv data_work data_work.gz && gunzip data_work.gz ;;
        bzip2)
            mv data_work data_work.bz2 && bunzip2 data_work.bz2 ;;
        POSIX)
            tar -xf data_work && rm data_work && mv data data_work ;;
        Zip)
            mv data_work data_work.zip && unzip -o data_work.zip && rm data_work.zip && mv data data_work ;;
        lzip)
            mv data_work data_work.lz && xz -d data_work.lz ;;
        ASCII)
            echo "=== FINAL FLAG FOUND ==="
            cat data_work
            break ;;
        *)
            echo "Unknown format: $TYPE"
            break ;;
    esac
done
```

---

## 🎯 Final Flag

After bypassing several fake flags (e.g., `cryptx{keep_digging_deeper}`), the script reached the base layer:

```text
cryptx{7h3_0n1on_h45_b33n_p33l3d_f0r_r34l}
```

---

## 🧠 Key Takeaways

* **The `file` command is essential:** Extensions can be misleading or missing; always verify the magic bytes.
* **Automation is King:** For "Matryoshka" style challenges (nested files), writing a quick parser script saves time and prevents manual errors.
* **Diversified Compression:** Handled multiple formats including `gzip`, `bzip2`, `tar`, `zip`, and `lzip/xz`.
* **Sift through the Noise:** CTF creators often use "fake flags" to discourage manual solvers.
