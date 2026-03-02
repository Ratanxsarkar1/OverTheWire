
---

# OverTheWire – Natas (Level 0–20)

## Overview

**Natas** is a web security wargame from [OverTheWire](https://overthewire.org) designed to teach the fundamentals of **server-side web security**.

Each level consists of a vulnerable web application. Your objective is to analyze the application, identify the vulnerability, and extract the password for the next level.

Unlike other OverTheWire challenges, **Natas does not provide SSH access**. All interaction happens via the web.

---

## How Natas Works

Each level is hosted at:

```
http://natasX.natas.labs.overthewire.org
```

Where `X` is the level number.

Example:

```
Level 0 → http://natas0.natas.labs.overthewire.org
```

Authentication is done via **HTTP Basic Authentication**.

Example starting credentials:

```
Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org
```

---

## Goal of Each Level

- Log in to the current level.
    
- Identify the vulnerability.
    
- Retrieve the password for the next level.
    
- Use that password to access the next level.


Each level’s password is stored on the server in:

```
/etc/natas_webpass/natasX
```
---
## Repository Structure

```
natas/
│
├── README.md
├── Level_0–10.md
...
└── level_X-34.md
```

### Levels Covered

- ✅ Level 0 – 10 (Basic Web Vulnerabilities)
---

## Skills Learned (Level 0–10)

- Viewing HTML source
- Client-side vs server-side security
- Directory enumeration
- robots.txt abuse
- HTTP header manipulation
- Cookie tampering
- Source code disclosure
- Local File Inclusion (LFI)
- Encoding/decoding logic reversal
- Command injection
- Blacklist bypass techniques

---

## Recommended Tools

During these levels, the following tools are useful:

- Browser Developer Tools
- curl
- Burp Suite
- Gobuster
- ffuf
- base64 / xxd
- Python (for encoding/decoding)
- grep
---

## Methodology Used

For each level, documentation includes:

- Concept explanation
    
- Step-by-step walkthrough
    
- Commands used
    
- Screenshot evidence
    
- Hidden password section (collapsible)
---

## Important Notes

- Do not skip levels.
- Do not brute-force.
- Focus on understanding the vulnerability.
- Document your learning process.


The goal is not just to retrieve passwords, but to understand **why the vulnerability exists** and how to prevent it.

---

## Starting Point

```
Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org
```

---

## Final Thoughts

Natas is one of the best beginner-to-intermediate web exploitation paths available. It builds strong fundamentals in:

- Web architecture
- HTTP mechanics
- Backend vulnerabilities
- Secure development awareness

---
## 🧑‍💻 Author

Ghost -  Cyber-security Learner & CTF Player
