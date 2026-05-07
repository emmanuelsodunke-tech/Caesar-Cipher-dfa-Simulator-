# Caesar Cipher DFA Simulator

## Design and Analysis of Caesar Cipher Using Deterministic Finite Automata (DFA)

**Course:** Theory of Computation (TOC)  
**Project Type:** Educational Cryptography & Automata Theory  
**Technologies:** HTML5, CSS3, JavaScript (ES6), HTML5 Canvas API

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Features](#features)
3. [Live Demo](#live-demo)
4. [DFA Formal Definition](#dfa-formal-definition)
5. [Mathematical Foundation](#mathematical-foundation)
6. [Installation & Usage](#installation--usage)
7. [How It Works](#how-it-works)
8. [Screenshots](#screenshots)
9. [Project Structure](#project-structure)
10. [Educational Value](#educational-value)
11. [Limitations](#limitations)
12. [Future Enhancements](#future-enhancements)
13. [References](#references)
14. [License](#license)
15. [Acknowledgments](#acknowledgments)

---

## Project Overview

This project presents an **interactive web-based simulator** that demonstrates the classical **Caesar Cipher** encryption technique modeled as a **Deterministic Finite Automaton (DFA)**. The simulator bridges classical cryptography with formal automata theory, providing both theoretical insight and hands-on experimentation.

The Caesar Cipher, attributed to Julius Caesar (100 BCE), is one of the earliest known substitution ciphers. It shifts each letter in the plaintext by a fixed number of positions in the alphabet. While historically significant, its simplicity makes it vulnerable to modern attacks. However, its deterministic structure provides an excellent framework for understanding the intersection of cryptography and formal language theory.

### Why DFA?

The Caesar Cipher is **purely deterministic**—given the same plaintext and key, it always produces the same ciphertext. This deterministic nature aligns perfectly with DFA theory, where each state-input pair leads to exactly one next state. By modeling the cipher as a DFA, we create a rigorous mathematical framework that:

- Formalizes encryption as state transitions
- Demonstrates deterministic computational processes
- Provides visual intuition for abstract automata concepts
- Bridges theory (TOC) with practice (Cryptography)

---

## Features

### Core Functionality
- **Interactive Encryption:** Input plaintext, select shift value k (0-25), and instantly generate ciphertext
- **Interactive Decryption:** Recover original plaintext from ciphertext using the correct key
- **Real-time Visualization:** Circular DFA diagram showing all 26 letter states and transition arrows
- **Step-by-Step Trace:** See each character transformation as a DFA state transition

### Cryptanalysis Tools
- **Brute-Force Attack:** Automatically test all 25 possible shift values to break the cipher
- **Frequency Analysis:** Display letter frequency distribution in ciphertext to identify patterns

### User Experience
- **Responsive Design:** Dark theme interface optimized for readability
- **Dynamic Updates:** All visualizations update in real-time as you adjust the shift value
- **No Installation Required:** Runs entirely in the browser—no server or dependencies needed

---

## Live Demo

**Open `index.html` in any modern web browser:**

```bash
# Simply double-click the file, or:
open index.html        # macOS
start index.html       # Windows
xdg-open index.html    # Linux
```

**Supported Browsers:** Chrome, Firefox, Edge, Safari (latest versions)

---

## DFA Formal Definition

### 26-State DFA Model (Alphabet Cycle)

**M = (Q, Σ, δ, q₀, F)**

| Component | Definition |
|-----------|------------|
| **Q** | {A, B, C, ..., Z} — 26 states (one per alphabet letter) |
| **Σ** | {A, B, C, ..., Z} — input alphabet |
| **q₀** | A — initial state (position 0) |
| **F** | Q — all states are accepting |
| **δ(q, a)** | (position(q) + k) mod 26 — transition function |

### Compact 2-State FSM Model (Mealy Machine)

**M = (Q, Σ, K, δ, q₀, F)**

| Component | Definition |
|-----------|------------|
| **Q** | {q₀, q₁} — processing state and final state |
| **Σ** | {a, b, c, ..., z} — lowercase input alphabet |
| **K** | {1, 2, ..., 25} — set of possible shift keys |
| **q₀** | Starting state |
| **F** | {q₁} — final state |
| **δ(q₀, x, k)** | q₀ with output shift(x, +k) — transition with output |
| **δ(q₀, ε)** | q₁ — end of input transition |

---

## Mathematical Foundation

### Encryption Formula
For a plaintext letter at position x (0-indexed: A=0, B=1, ..., Z=25) and shift key k:

```
E(x) = (x + k) mod 26
```

### Decryption Formula
For a ciphertext letter at position y:

```
D(y) = (y - k) mod 26 = (y + (26 - k)) mod 26
```

### Example (k = 3)
```
Plaintext:  H(7)  E(4)  L(11) L(11) O(14)
              ↓     ↓      ↓      ↓     ↓
Ciphertext: K(10) H(7)  O(14) O(14) R(17)

Result: HELLO → KHOOR
```

---

## Installation & Usage

### Method 1: Direct Download
1. Download `index.html` from this repository
2. Double-click to open in your browser
3. Start encrypting!

### Method 2: Clone Repository
```bash
git clone https://github.com/[your-username]/caesar-cipher-dfa-simulator.git
cd caesar-cipher-dfa-simulator
open index.html
```

### How to Use the Simulator

1. **Enter Text:** Type your message in the input field (supports uppercase, lowercase, spaces, punctuation)
2. **Select Shift:** Drag the slider to choose k (0-25). Watch the circular diagram update in real-time!
3. **Encrypt/Decrypt:** Click the buttons to transform your text
4. **View DFA Trace:** See step-by-step character transformations in the "Step-by-Step DFA" section
5. **Analyze:** Use Brute Force or Frequency Analysis tools to test cipher security

---

## How It Works

### Core Algorithm (JavaScript)

```javascript
function caesar(text, k, mode) {
    let result = "";

    for (let i = 0; i < text.length; i++) {
        let c = text[i];

        if (c.match(/[a-z]/i)) {
            // Determine ASCII base (65 for uppercase, 97 for lowercase)
            let base = (c === c.toUpperCase()) ? 65 : 97;

            // Apply shift (+k for encrypt, -k for decrypt)
            let shift = (mode === "encrypt") ? k : -k;

            // Modular arithmetic with wraparound
            let transformed = String.fromCharCode(
                (c.charCodeAt(0) - base + shift + 26) % 26 + base
            );

            result += transformed;
        } else {
            // Non-alphabetic characters remain unchanged
            result += c;
        }
    }

    return result;
}
```

### DFA Visualization (Canvas API)

The circular diagram renders:
- **26 nodes** arranged in a circle (radius: 150px, center: 200,200)
- **26 arrows** connecting each letter to its ciphertext counterpart
- **Real-time updates** when shift value changes
- **Color coding:** Dark nodes (#1e293b) with green arrows (#22c55e)

---

## Screenshots

*(Add screenshots here showing:)*
1. *Main interface with encryption result*
2. *Circular DFA diagram for k=3*
3. *Brute-force attack results*
4. *Frequency analysis display*

---

## Project Structure

```
caesar-cipher-dfa-simulator/
│
├── index.html              # Main simulator (HTML + CSS + JS)
├── README.md               # This file
├── LICENSE                 # Open-source license
│
├── docs/                   # Documentation
│   ├── project-report.docx # Complete project report
│   └── dfa-diagrams/       # DFA state diagrams
│
└── assets/                 # Images and resources
    ├── screenshots/
    └── diagrams/
```

---

## Educational Value

This project serves as a **pedagogical bridge** between:

| Theory of Computation | Cryptography |
|----------------------|--------------|
| States (Q) | Alphabet positions |
| Transitions (δ) | Character shifts |
| Determinism | Fixed key encryption |
| Accepting states | Completed encryption |
| Regular languages | Substitution patterns |

### Learning Outcomes
- Understand how abstract machines model real algorithms
- Visualize deterministic processes through state transitions
- Appreciate the mathematical foundations of cryptography
- Recognize why simple ciphers are vulnerable to attacks
- Connect historical methods with modern computational theory

---

## Limitations

### Caesar Cipher Weaknesses
1. **Small Key Space:** Only 25 valid keys (k=0 produces no encryption)
2. **Brute-Force Vulnerability:** All keys can be tested in seconds
3. **Frequency Analysis:** Letter patterns are preserved, just shifted
4. **No Diffusion:** Changing one plaintext letter changes only one ciphertext letter
5. **Known-Plaintext Attack:** If any plaintext-ciphertext pair is known, the key is immediately revealed

### DFA Model Limitations
- The 26-state DFA is specific to the English alphabet
- Does not model modern encryption (AES, RSA) which require more complex automata
- Serves educational purposes rather than security applications

---

## Future Enhancements

1. **Vigenère Cipher:** Extend to polyalphabetic substitution using keyword-based multiple shifts
2. **Block Cipher Mode:** Model processing of fixed-size blocks rather than individual characters
3. **Unicode Support:** Handle non-English alphabets and special characters
4. **Automated Cryptanalysis:** Implement chi-square frequency matching and dictionary-based plaintext recognition
5. **Step-by-Step Animation:** Animate DFA state transitions for each input character
6. **Export Functionality:** Save encrypted messages and DFA diagrams as images
7. **Mobile Responsive:** Optimize interface for smartphones and tablets
8. **Formal Verification:** Prove correctness using theorem provers (Coq/Isabelle)

---

## References

1. Hopcroft, J. E., & Ullman, J. D. (1979). *Introduction to Automata Theory, Languages, and Computation*. Addison-Wesley.
2. Stallings, W. (2017). *Cryptography and Network Security: Principles and Practice* (7th ed.). Pearson.
3. Singh, S. (1999). *The Code Book: The Science of Secrecy from Ancient Egypt to Quantum Cryptography*. Anchor Books.
4. Shannon, C. E. (1949). Communication Theory of Secrecy Systems. *Bell System Technical Journal*, 28(4), 656-715.
5. Cohen, D. I. A. (1996). *Introduction to Computer Theory* (2nd ed.). John Wiley & Sons.
6. Paar, C., & Pelzl, J. (2010). *Understanding Cryptography: A Textbook for Students and Practitioners*. Springer.
7. Turing, A. M. (1936). On Computable Numbers, with an Application to the Entscheidungsproblem. *Proceedings of the London Mathematical Society*, 42(2), 230-265.
8. Lecture Notes on Automata Theory and Formal Languages, Department of Computer Science.

---

## License

This project is licensed under the **MIT License** — see [LICENSE](LICENSE) file for details.

You are free to:
- ✅ Use for educational purposes
- ✅ Modify and distribute
- ✅ Use in your own projects

Requirements:
- Include original copyright notice
- Include license text

---

## Acknowledgments

- **Theory of Computation Course** — for providing the theoretical framework
- **Julius Caesar** — for the original cipher (even if he didn't know about DFAs!)
- **Modern Cryptography Pioneers** — Shannon, Diffie, Hellman, Rivest, Shamir, Adleman
- **Open Source Community** — for web technologies that make this possible

---

## Contact & Feedback

**For questions, suggestions, or collaboration:**

- Open an [Issue](../../issues) on GitHub
- Email: emmanuelsodunke@gmail.com


**If you use this project for your coursework, please cite it appropriately!**

---

<p align="center">
  <b>Built with 💻 + 📚 + 🔢 for the love of computation theory</b><br>
  <i>"Cryptography is nothing more than a mathematical framework for discussing the implications of various paranoid delusions." — Don Alvarez</i>
</p>
