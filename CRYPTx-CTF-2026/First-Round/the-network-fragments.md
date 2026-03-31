# 🛰️ The Network Fragments

**Category:** Digital Forensics / Network Analysis  
**Difficulty:** Easy/Medium

---

## 📌 Challenge Description

The challenge provided a PCAP file (`traffic.pcap`) containing captured network traffic. The objective was to perform deep packet inspection to identify and reconstruct a hidden flag fragmented across multiple network transmissions.

---

## 🔍 Solution Approach

### 🧩 Phase 1: Traffic Analysis
Initial inspection was conducted using **Wireshark** to identify the protocol distribution and look for anomalies in the traffic stream.

* **Observation:** A high volume of **ICMP (Ping)** packets was detected.
* **Anomaly:** Standard ICMP Echo requests usually contain a static padding pattern. However, these packets contained varying data payloads in the hexadecimal field.
* **Pattern:** Examining the hex representation of these payloads revealed what appeared to be hex-encoded ASCII characters.

---

### ⚙️ Phase 2: Automated Extraction
Since manual extraction of hex data from hundreds of packets is inefficient, a **Python** script was used to interface with `tshark` (the command-line version of Wireshark) to pull the data fields automatically.

#### 1. The Extraction Script
The script filters for ICMP traffic, extracts the data field, and attempts to decode the hex into readable UTF-8 text.

```python
import subprocess

# Run tshark to extract the 'data' field from all ICMP packets
result = subprocess.run([
    "tshark", 
    "-r", "traffic.pcap", 
    "-Y", "icmp", 
    "-T", "fields", 
    "-e", "data"
], capture_output=True, text=True)

# Decode each line of hex data
for line in result.stdout.splitlines():
    line = line.strip()
    if not line:
        continue
    try:
        # Convert hex to bytes and then to a string
        decoded = bytes.fromhex(line).decode('utf-8', errors='ignore')
        
        # Search for the flag format
        if 'cryptx' in decoded.lower():
            print(f"Flag found: {decoded}")
    except Exception:
        pass
```

---

### 🔓 Phase 3: Flag Reconstruction
By running the script, the fragmented data across the ICMP payloads was reassembled into a clear string, bypassing the "noise" of the network traffic.

---

## 🎯 Final Flag

```text
cryptx{1cmp_p4ck37_f0r3n51c5_5ucc355}
```

---

## 🧠 Key Takeaways

* **ICMP Tunneling/Exfiltration:** ICMP is a common protocol used for data exfiltration because it is often overlooked by basic firewalls.
* **`tshark` is powerful:** Learning to use `tshark` with the `-T fields` and `-e` flags allows for rapid data extraction from large capture files.
* **Payload Inspection:** Always check the "Data" or "Padding" sections of common protocols (ICMP, DNS, HTTP headers) for hidden information.
