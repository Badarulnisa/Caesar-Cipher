# Caesar Cipher Tool

![C++](https://img.shields.io/badge/Language-C%2B%2B-00599C?style=flat-square&logo=cplusplus&logoColor=white)
![Platform](https://img.shields.io/badge/Platform-Cross--Platform-informational?style=flat-square)
![Category](https://img.shields.io/badge/Category-Cryptography%20%7C%20CTF%20Tool-darkred?style=flat-square)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-yellow?style=flat-square)

A command-line Caesar Cipher toolkit built in C++ that supports text encryption and decryption, brute-force cryptanalysis, file-level cipher operations, random key generation, and custom wordlist creation. Developed as a hands-on exercise in classical cryptography and foundational security tooling.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Motivation](#motivation)
- [Cybersecurity Relevance](#cybersecurity-relevance)
- [Features](#features)
- [Technologies Used](#technologies-used)
- [System Architecture and Workflow](#system-architecture-and-workflow)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Key Components](#key-components)
- [Security Considerations](#security-considerations)
- [Future Improvements](#future-improvements)
- [Learning Outcomes](#learning-outcomes)
- [Challenges Faced](#challenges-faced)
- [Conclusion](#conclusion)
- [License](#license)

---

## Project Overview

The Caesar Cipher Tool is a multi-function, menu-driven C++ application implementing the classical Caesar (shift) cipher, one of the oldest and most widely studied substitution ciphers in cryptography. The tool provides both offensive and defensive capabilities: it can encrypt and decrypt messages, perform exhaustive brute-force key recovery across all 25 possible shifts, process entire text files, generate and persist cryptographic keys to disk, and produce custom wordlists from user-supplied personal data for use in password auditing or CTF challenges.

The project is intentionally designed to be educational, practical, and extensible, making it suitable as a portfolio demonstration of cryptographic fundamentals, secure C++ programming practices, and CLI tool development.

---

## Problem Statement

Classical cryptography is the foundation upon which modern encryption standards are built. Yet many developers and security students encounter cryptographic concepts in isolation, without working implementations that demonstrate the full lifecycle: key generation, encryption, decryption, and cryptanalysis.

Additionally, in Capture the Flag (CTF) competitions and penetration testing contexts, analysts frequently encounter Caesar-encrypted strings in challenges, legacy systems, or obfuscated data. There is a practical need for a lightweight, offline tool that can rapidly process such ciphertext without relying on web-based platforms, which may not be available in air-gapped or restricted lab environments.

This project addresses both gaps: providing a self-contained, educational implementation of Caesar cipher operations and a practical toolkit for cryptographic analysis.

---

## Motivation

This project was developed to:

- Build a concrete understanding of substitution ciphers and their inherent weaknesses from first principles.
- Practice C++ programming concepts including modular function design, file I/O, input validation, and control flow.
- Create a practical utility applicable to CTF competitions, particularly in the Cryptography and OSINT categories.
- Demonstrate that even classical ciphers, when understood deeply, provide insight into why modern cryptographic standards were necessary.
- Establish a foundation for extending into more complex cipher implementations such as Vigenere, ROT13, XOR, and polyalphabetic substitution.

---

## Cybersecurity Relevance

### Why a Cybersecurity Student Would Build This

Caesar cipher analysis is a rite of passage in cryptography education and appears regularly in CTF competitions, security certifications (such as CompTIA Security+), and cryptanalysis coursework. Building this tool from scratch, rather than using a pre-built library, forces a developer to internalize the mathematical operations that underpin all substitution-based cryptography.

### Cybersecurity Concepts Involved

| Concept | Application in This Project |
|---|---|
| **Symmetric Encryption** | Caesar cipher uses the same key for both encryption and decryption |
| **Cryptanalysis** | Brute-force attack over the full keyspace (shifts 1-25) |
| **Key Management** | Key file generation and secure storage awareness |
| **Cipher Text Attack** | Brute-force function attacks ciphertext without knowledge of the key |
| **OSINT / Password Analysis** | Wordlist generator creates targeted password candidates from personal data |
| **File Security** | File-level encryption and decryption of plaintext documents |
| **Input Validation** | Defensive programming against malformed or malicious input |

### How This Tool Fits Cybersecurity Environments

- **CTF Competitions**: Instantly brute-forces Caesar-encrypted flags across all 25 shifts, saving significant manual effort during timed challenges.
- **Security Awareness Training**: Demonstrates to non-technical audiences why simple ciphers offer no meaningful protection, supporting the case for modern encryption.
- **Cryptography Education**: Serves as a reference implementation for understanding shift ciphers before progressing to AES, RSA, or elliptic curve cryptography.
- **Wordlist Generation**: Produces targeted wordlists combining personal identifiers (name, date of birth, pet name, age), useful for authorized password auditing against weak credential policies.

---

## Features

| # | Feature | Description |
|---|---|---|
| 1 | **Text Encryption** | Encrypts user-supplied plaintext using a manually specified shift key (1-25), preserving case and non-alphabetic characters |
| 2 | **Text Decryption** | Decrypts Caesar ciphertext using a known shift key |
| 3 | **Brute-Force Cryptanalysis** | Iterates all 25 possible shift keys and outputs every candidate decryption, enabling rapid manual identification of correct plaintext |
| 4 | **Random Key Encryption** | Generates a cryptographically seeded random shift key using `srand(time(0))`, encrypts input text, and displays the key for later use |
| 5 | **Random Key Decryption** | Decrypts text using a previously saved random key |
| 6 | **File Encryption** | Reads a plaintext file line-by-line, encrypts its contents, and writes the result to a new output file |
| 7 | **File Decryption** | Reads an encrypted file and restores the original plaintext to a specified output file |
| 8 | **Key File Generation** | Generates a random key and saves it to a named file for offline key distribution or storage |
| 9 | **Custom Wordlist Generator** | Builds a targeted wordlist from personal data inputs (name, date of birth, pet name, age) and writes combinations to a file |
| 10 | **Input Validation** | Handles malformed input, empty strings, out-of-range keys, and stream errors throughout all operations |

---

## Technologies Used

| Component | Detail |
|---|---|
| **Language** | C++ (Standard: C++11 compatible) |
| **Standard Libraries** | `<iostream>`, `<string>`, `<fstream>`, `<cstdlib>`, `<ctime>` |
| **Build System** | Any standard C++ compiler (g++, clang++, MSVC) |
| **I/O** | Console-based CLI with `cin`/`cout` and file streams (`ifstream`, `ofstream`) |
| **Randomness** | Pseudo-random number generation via `rand()` seeded with `time(0)` |
| **Platform** | Cross-platform (Windows, Linux, macOS) |

No external dependencies or third-party libraries are required.

---

## System Architecture and Workflow

The application follows a modular, function-based architecture. All cipher logic is encapsulated in dedicated functions, invoked through a central menu loop in `main()`.

### High-Level Workflow

```
┌─────────────────────────────────────────────────────┐
│                   Program Start                      │
│              srand(time(0)) — seed RNG               │
└────────────────────────┬────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────┐
│                  Main Menu Loop                      │
│          Displays options 1-10 to user               │
│       Reads integer choice with error handling       │
└────────────────────────┬────────────────────────────┘
                         │
              ┌──────────┼──────────┐
              ▼          ▼          ▼
        ┌──────────┐ ┌────────┐ ┌──────────────┐
        │ Encrypt  │ │Decrypt │ │  Brute Force │
        │  Text    │ │  Text  │ │  (Keys 1-25) │
        └──────────┘ └────────┘ └──────────────┘
              │          │          │
              ▼          ▼          ▼
        ┌──────────┐ ┌────────┐ ┌──────────────┐
        │ Random   │ │ File   │ │  Wordlist    │
        │Key Enc.  │ │  I/O   │ │  Generator   │
        └──────────┘ └────────┘ └──────────────┘
```

### Encryption Logic (Character Level)

```
Uppercase:  cipher[i] = ( (plain[i] - 'A') + key ) % 26 + 'A'
Lowercase:  cipher[i] = ( (plain[i] - 'a') + key ) % 26 + 'a'
Other:      cipher[i] = plain[i]   (spaces, digits, symbols preserved)
```

### Decryption Logic (Character Level)

```
Uppercase:  plain[i] = ( (cipher[i] - 'A') - key + 26 ) % 26 + 'A'
Lowercase:  plain[i] = ( (cipher[i] - 'a') - key + 26 ) % 26 + 'a'
Other:      plain[i] = cipher[i]
```

The `+ 26` offset in decryption prevents negative modulo results, which would produce incorrect character values in C++.

---

## Installation

### Prerequisites

- A C++ compiler supporting C++11 or later
  - Linux/macOS: `g++` (GCC) or `clang++`
  - Windows: MinGW-w64, MSVC, or WSL with g++

### Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/caesar-cipher-tool.git
cd caesar-cipher-tool
```

### Compile

**Linux / macOS**
```bash
g++ -o caesar_tool caeser_code.cpp
```

**Windows (MinGW)**
```bash
g++ -o caesar_tool.exe caeser_code.cpp
```

**With optimization flag (recommended)**
```bash
g++ -O2 -o caesar_tool caeser_code.cpp
```

### Run

```bash
# Linux / macOS
./caesar_tool

# Windows
caesar_tool.exe
```

---

## Usage

Upon launching, the program presents an interactive menu:

```
====== Caesar Cipher Tool ======
1.  Encrypt
2.  Decrypt
3.  Caesar Brute Force
4.  Random Key Encrypt
5.  Random Key Decrypt
6.  File Encrypt
7.  File Decrypt
8.  Generate Key File
9.  Generate Custom Wordlist
10. Exit

Enter your choice:
```

### Example: Encrypting Text

```
Enter your choice: 1

Enter text to encrypt: Hello World
Enter shift key (1-25): 13

Original Text : Hello World
Shift Key     : 13
Encrypted Text: Uryyb Jbeyq
```

### Example: Brute-Force Decryption

```
Enter your choice: 3

Enter encrypted text: Khoor Zruog

===== All Possible Decryptions =====
Key 1 : Jgnnq Yqtnf
Key 2 : Ifmmp Xpsme
Key 3 : Hello World    <-- Correct plaintext identified
Key 4 : Gdkkn Vnqkc
...
Key 25: Lipps Asvph
```

### Example: File Encryption

```
Enter your choice: 6

Enter input filename: report.txt
Enter output filename: report_encrypted.txt
Enter shift key (1-25): 7

File encrypted successfully.
Output saved in: report_encrypted.txt
```

### Example: Wordlist Generation

```
Enter your choice: 9

Enter Name: Alice
Enter Date of Birth: 1990
Enter Pet Name: Fluffy
Enter Age: 34
Enter output filename: wordlist.txt

Wordlist generated successfully.
Saved in: wordlist.txt
```

**Generated wordlist content:**
```
Alice
Alice123
Alice786
Alice1990
AliceFluffy
Alice34
Fluffy123
Fluffy34
Alice1990Fluffy
Alice34Fluffy
```

---

## Project Structure

```
caesar-cipher-tool/
│
├── caeser_code.cpp        # Main source file — all logic and entry point
└── README.md              # Project documentation
```

> Note: The project is currently single-file. See Future Improvements for a proposed modular refactor.

---

## Key Components

### `main()`
Entry point and menu controller. Seeds the random number generator using `srand(time(0))`. Runs a `while` loop until the user selects Exit (option 10). Handles non-integer input via `cin.fail()` detection with stream clearing and recovery.

### `encrypt()`
Accepts plaintext and a user-defined shift key. Processes each character using modular arithmetic, preserving case and passing through non-alphabetic characters unchanged. Validates that the key is within the 1-25 range.

### `decrypt()`
Reverses the encryption formula using the same shift key. Applies the `+26` offset to prevent negative modulo values — a common off-by-one error in naive Caesar implementations.

### `caesarBruteForce()`
Iterates keys 1 through 25, applying the decryption formula for each, and prints all 25 candidate plaintexts. Enables rapid visual identification of the correct decryption without requiring prior knowledge of the key.

### `randomKeyEncrypt()` / `randomKeyDecrypt()`
Uses `rand() % 25 + 1` to generate a random shift key in range [1, 25]. Displays the generated key to the user and prompts them to save it for later decryption.

### `fileEncrypt()` / `fileDecrypt()`
Performs line-by-line read and write using `ifstream` and `ofstream`. Encrypts or decrypts each line and writes the result to a specified output file. Handles file open failures gracefully.

### `generateKeyFile()`
Generates a random key and writes it to a named text file in a human-readable format. Simulates a basic key distribution mechanism.

### `generateWordlist()`
Accepts personal data fields (name, date of birth, pet name, age) and writes a set of common password combinations to a text file. Intended for authorized CTF and security audit use only.

---

## Security Considerations

### Strengths

- **Input validation** is consistently applied across all functions, preventing crashes from invalid key input or empty strings.
- **Stream error recovery** using `cin.fail()`, `cin.clear()`, and `cin.ignore()` ensures the program remains stable across malformed inputs.
- **Case and character preservation** in cipher logic correctly handles mixed-case text and non-alphabetic characters.
- **File error handling** checks for failed file open operations before processing, preventing undefined behavior.

### Weaknesses and Risks

| Issue | Detail | Risk Level |
|---|---|---|
| **Weak randomness** | `rand()` seeded with `time(0)` is not cryptographically secure (CSPRNG). An attacker who knows the approximate program start time can predict the generated key. | Medium |
| **Caesar cipher is not secure** | The keyspace of 25 shifts is trivially exhausted. This cipher should never be used for real data protection. | High (by design) |
| **No key encryption** | Key files are saved as plaintext integers. Anyone with filesystem access can read the key. | Medium |
| **Path traversal** | File input/output accepts arbitrary user-specified filenames without sanitization, which could allow unintended writes to sensitive paths if deployed in a shared environment. | Medium |
| **No authentication** | The tool provides no access control or usage logging. | Low (local tool) |
| **Wordlist content** | The wordlist generator stores personal data in plaintext files. Users should be aware of the sensitivity of generated files. | Medium |

### Recommendations

- Replace `rand()` with `<random>` (C++11 Mersenne Twister) or platform CSPRNG (`/dev/urandom` on Linux) for any security-sensitive random key generation.
- Add filename sanitization or restrict file operations to a working directory.
- For production use, replace Caesar cipher logic with AES-256 via OpenSSL or libsodium.
- Add a disclaimer in the tool reminding users that wordlist generation must only be used for authorized security testing.

---

## Future Improvements

### 1. Modular File Structure
**What**: Split the single `.cpp` file into a header (`caesar.h`) and implementation file (`caesar.cpp`).  
**Why**: Improves code maintainability, enables unit testing, and follows industry-standard C++ project organization.  
**Impact**: Scalability, readability, and professional code quality.

### 2. Frequency Analysis for Cryptanalysis
**What**: Implement English letter frequency analysis (E, T, A, O, I, N...) to automatically identify the most probable correct decryption from brute-force output.  
**Why**: Eliminates the need for manual inspection of 25 candidates during CTF challenges.  
**Impact**: Dramatically improves practical utility as a cryptanalysis tool.

### 3. CSPRNG Key Generation
**What**: Replace `rand()`/`srand()` with `std::random_device` and `std::mt19937` (C++11), or read from `/dev/urandom`.  
**Why**: The current PRNG is predictable. Cryptographic key generation requires entropy sources that cannot be reproduced by an attacker.  
**Impact**: Security.

### 4. Vigenere and ROT13 Cipher Support
**What**: Extend the menu with Vigenere (polyalphabetic) and ROT13 cipher modes.  
**Why**: ROT13 appears frequently in CTF challenges; Vigenere provides a natural progression from Caesar in cryptography education.  
**Impact**: Feature coverage, educational value, CTF utility.

### 5. Advanced Wordlist Automation
**What**: Add leet-speak substitutions, capitalization variations, common suffixes (!, @, #, 01), and year appending to the wordlist generator.  
**Why**: Real-world password patterns include these transformations. The current implementation notes this as a planned feature.  
**Impact**: Significantly improves usefulness for authorized password auditing.

### 6. Encrypted Key File
**What**: Protect generated key files with a passphrase before writing to disk.  
**Why**: A plaintext key file negates the security of encrypting a message if both exist in the same directory.  
**Impact**: Security, realistic key management simulation.

### 7. Command-Line Argument Mode
**What**: Support direct CLI invocation such as `./caesar_tool --encrypt --key 13 --input plain.txt --output cipher.txt`.  
**Why**: Enables scripting, automation, and integration into CTF pipelines or shell scripts.  
**Impact**: Usability, automation, professional tooling standard.

### 8. Unit Tests
**What**: Add a test suite (using a lightweight framework or manual assertions) verifying encrypt/decrypt round-trips, edge cases (key=1, key=25), and brute-force correctness.  
**Why**: Ensures correctness after any code modifications and demonstrates software engineering discipline.  
**Impact**: Code reliability, professional credibility.

---

## Learning Outcomes

Through developing this project, the following skills and concepts were reinforced:

- **Classical Cryptography**: Deep understanding of substitution cipher mathematics, including modular arithmetic, keyspace enumeration, and cipher inversion.
- **C++ File I/O**: Practical use of `ifstream` and `ofstream` for reading and writing files across multiple functions.
- **Defensive Programming**: Consistent input validation, stream error handling, and graceful failure across all user-facing operations.
- **Modular Design**: Separation of concerns using function prototyping, keeping `main()` as a clean dispatcher.
- **Brute-Force Methodology**: Implementation of exhaustive key search, foundational to understanding both symmetric cryptanalysis and password cracking.
- **Pseudorandom Number Generation**: Understanding of PRNG seeding and its implications for security-sensitive applications.
- **CTF Tool Development**: Experience building purpose-built tools for cryptographic challenge environments.

---

## Challenges Faced

### Negative Modulo in Decryption
C++ does not guarantee positive results from the `%` operator when operands are negative. Decrypting with a naive `(char - key) % 26` formula produces incorrect results for characters early in the alphabet. The `+26` offset (`(char - key + 26) % 26`) resolves this without branching.

### cin Buffer Contamination
Mixing `cin >>` (for integers) and `getline()` (for strings) in the same input session causes the `getline()` to immediately consume the leftover newline from the previous `cin >>` call, reading an empty string. This was resolved by inserting `cin.ignore(1000, '\n')` at the start of each function that reads string input following a menu selection.

### File Access Failures
On certain operating systems or permission configurations, files may fail to open without meaningful error messages. Explicit `is_open()` checks with user-facing error messages were added to handle this gracefully.

### Keeping the Menu Stable Across Invalid Input
A non-integer input to the menu (e.g., entering "abc") puts `cin` into a fail state, causing the loop to spin indefinitely. The `cin.fail()` detection block with `cin.clear()` and `cin.ignore()` resolves this and restores normal input behavior.

---

## Conclusion

The Caesar Cipher Tool is a complete, functional, and professionally structured command-line application demonstrating foundational cryptography, defensive C++ programming, and practical security tooling. It covers the full lifecycle of a symmetric cipher: key generation, encryption, decryption, cryptanalysis, and key management, while also including an auxiliary utility directly applicable to CTF competition workflows.

Although the Caesar cipher itself offers no modern security guarantees, the implementation decisions made in this project, such as input validation, error handling, file I/O safety, and modular function design, reflect engineering practices that transfer directly to developing robust security tools. The identified limitations and proposed future improvements chart a clear path toward a more capable and production-ready cryptographic toolkit.

This project demonstrates applied knowledge of cryptography fundamentals, practical C++ development, and an understanding of why classical ciphers were superseded by modern standards, all of which are core competencies for a cybersecurity professional.

---

## License

This project is licensed under the **MIT License**.

```
MIT License

Copyright (c) 2025 Badarulnisa

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

> **Disclaimer**: The wordlist generation feature is intended solely for authorized security testing, CTF competitions, and educational purposes. Unauthorized use of generated wordlists against systems or accounts you do not own or have explicit permission to test is illegal and unethical.

---

*C++ | Cryptography | CTF Tooling | Cybersecurity*
