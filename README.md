<p align="center">
  <img src="./HSTU_Logo.png" alt="HSTU Logo" width="150">
</p>

<h2 align="center"><strong>Hajee Mohammad Danesh Science and Technology University</strong></h2>

<h3 align="center">Dinajpur-5200</h3>

---

<h2 align="center" style="color:#16a085;"><strong> Course Information</strong></h2>

<p align="center">
  <strong>Course Title:</strong> Mathematical Analysis for Computer Science  
  <br>
  <strong>Course Code:</strong> CSE 361
</p>

---

<h2 align="center" style="color:#2980b9;"><strong> Algorithm Name</strong></h2>

<h1 align="center" style="color:#8e44ad;"><strong>🔐 XOR-FlexCipher</strong></h1>

---

<h2 align="center" style="color:#16a085;"><strong>🧑‍💻 Submitted By</strong></h2>

<p align="center">
  <strong>Name:</strong> Fahim Hossain Dipo 
  <br>
  <strong>Student ID:</strong> 2102004
  <br>
  <strong>Level:</strong> 3  
  <br>
  <strong>Semester:</strong> II  
  <br>
  <strong>Department:</strong> Computer Science and Engineering  
</p>

---

<h2 align="center" style="color:#16a085;"><strong>👨‍🏫 Submitted To</strong></h2>

<p align="center">
  <strong>Name:</strong> Pankaj Bhowmik  
  <br>
  <strong>Designation:</strong> Lecturer  
  <br>
  <strong>Department:</strong> Computer Science and Engineering  
</p>


---

# 🔐 Algorithm Description

## Algorithm Name: **XOR-FlexCipher**  
**(XOR-based Flexible Cipher with Offset & Modular Arithmetic)**

This is a custom cryptographic algorithm based on:
- ASCII value transformation
- Bitwise XOR operation with a key (symmetric key cipher)
- Addition offset to obfuscate patterns
- Modular arithmetic (mod 128 for ASCII compatibility)

---

## 📑 Table of Contents
- [🔒 Encryption Algorithm](#-encryption-algorithm)
- [🔓 Decryption Algorithm](#-decryption-algorithm)
- [✅ Example Test Case](#-example-test-case)
- [🧠 Flowcharts](#-flowcharts)
- [💻 C++ Source Code](#-c-source-code)

---

# 🔒 Encryption Algorithm

Let:  
- `KA` = Encryption key (an integer between 1 and 127)  
- `P[i]` = ASCII value of i-th character in the plaintext  
- `E[i]` = Encrypted ASCII value (ciphertext character)

### Formula:
```text
E[i] = (P[i] XOR KA + 7) mod 128
```

---

# 🔓 Decryption Algorithm

Let:
- `KB` = Decryption key (same as KA for symmetric ciphers)  
- `C[i]` = ASCII value of i-th ciphertext character  
- `D[i]` = Decrypted ASCII value (plaintext character)

### Formula:
```text
D[i] = ((C[i] - 7 + 128) mod 128) XOR KB
```

---

## ✅ Example Test Case

**Plaintext:** `HELLO`  
**Key (KA = KB):** 23

### Step-by-step Encryption:

| Pos | Char | ASCII | XORed with KA | +7 | %128 | Cipher Char |
|-----|------|--------|---------------|----|------|-------------|
| 0   | H    | 72     | 95            |102 | 102  | f           |
| 1   | E    | 69     | 82            | 89 |  89  | Y           |
| 2   | L    | 76     | 91            | 98 |  98  | b           |
| 3   | L    | 76     | 91            | 98 |  98  | b           |
| 4   | O    | 79     | 88            | 95 |  95  | _           |

**Ciphertext:** `fYbb_`

### Step-by-step Decryption:

| Pos | Char | ASCII | -7 | %128 | XOR with KB | Decrypted Char |
|-----|------|--------|-----|------|-------------|----------------|
| 0   | f    | 102    | 95  | 95   | 72          | H              |
| 1   | Y    | 89     | 82  | 82   | 69          | E              |
| 2   | b    | 98     | 91  | 91   | 76          | L              |
| 3   | b    | 98     | 91  | 91   | 76          | L              |
| 4   | _    | 95     | 88  | 88   | 79          | O              |

**Decrypted Text:** `HELLO`

---

## 🧠 Flowcharts

![Encryption and Decryption Flowcharts](/flowchart.png)

---

## 💻 C++ Source Code

```cpp
#include <iostream>
#include <string>
using namespace std;

string encrypt(string plaintext, int key) {
    string ciphertext = "";
    for (char c : plaintext) {
        int temp = ((c ^ key) + 7) % 128;
        ciphertext += static_cast<char>(temp);
    }
    return ciphertext;
}

string decrypt(string ciphertext, int key) {
    string plaintext = "";
    for (char c : ciphertext) {
        int temp = ((c - 7 + 128) % 128) ^ key;
        plaintext += static_cast<char>(temp);
    }
    return plaintext;
}

int main() {
    string text = "HELLO";
    int key = 23;

    string encrypted = encrypt(text, key);
    string decrypted = decrypt(encrypted, key);

    cout << "Original: " << text << endl;
    cout << "Encrypted: " << encrypted << endl;
    cout << "Decrypted: " << decrypted << endl;

    return 0;
}

