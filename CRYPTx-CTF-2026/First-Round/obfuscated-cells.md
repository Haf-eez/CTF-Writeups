# 🧠 Obfuscated Cells

**Category:** Cryptography / Esoteric Language  
**Difficulty:** Easy  

---

## 📌 Challenge Description

We were given an encoded text and a hint suggesting that it needed to be decrypted using a **Brainfuck decoder**.

---

## 🔍 Solution Approach

### 🧩 Identifying the Encoding

The challenge name **"Obfuscated Cells"** hinted at memory-based operations.  
This strongly suggested the use of **Brainfuck**, an esoteric programming language that operates on memory cells.

---

### ⚙️ Encoded Input

The provided encoded text was:

```brainfuck
++++++++++[>+>+++>+++++++>++++++++++<<<<-]>>>>-.+++++++++++++++.+++++++.---------.++++.++++.+++.-------------------------.++++++++++++++++.<------------------.---.>----.--------.+++++++++++++++.<++++++++.>----------.------------.++++++++++++++.<-----.>++++++.+.<-.>--.-------------------.++++++++++++++++.---------.-------.++++++++++++++.<.>.<++++++++++++++++++++++++++++.>+++++.+++++++.<++++++++++++++++.++++.<+++++++++++++++++++++.>+++++++++..>------.++++++++++.
````

---

### 🧪 Decoding Process

To decode the message:

1. Copied the Brainfuck code
2. Used an **online Brainfuck interpreter / decoder**
3. Executed the code

The program output revealed the hidden flag.

---

## 🎯 Final Flag

```
cryptx{br41nfu9k_m4st3r_of_m3mOry_c3lls}
```

---

## 🧠 Key Takeaways

* Recognizing patterns related to **Brainfuck encoding**
* Understanding how Brainfuck uses **memory cells and pointers**
* Using online interpreters to decode esoteric languages quickly
