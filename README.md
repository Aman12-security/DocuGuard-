# 🔐 DocuGuard — Cryptographic Document Verification Bot

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Tests](https://img.shields.io/badge/Tests-26%20Passed-brightgreen)
![Cryptography](https://img.shields.io/badge/Crypto-SHA256%20%7C%20HMAC%20%7C%20SHA3-orange)
![Platform](https://img.shields.io/badge/Platform-Telegram%20Bot-blue?logo=telegram)

**A Telegram bot that uses SHA-256, HMAC-SHA256, SHA3-256, and Merkle Trees to register and verify the authenticity of documents — detecting any tampering with mathematical certainty.**

</div>

---

## 📌 Table of Contents

- [Features](#-features)
- [Cryptographic Techniques](#-cryptographic-techniques)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Installation](#-installation)
- [Configuration](#-configuration)
- [Running the Bot](#-running-the-bot)
- [Bot Commands](#-bot-commands)
- [How It Works](#-how-it-works)
- [Testing](#-testing)
- [Security](#-security)
- [Future Enhancements](#-future-enhancements)

---

## ✨ Features

| Feature | Description |
|---|---|
| 🔒 **Register Document** | Compute multi-algorithm fingerprint and store in secure vault |
| ✅ **Verify Document** | Instantly detect if a document was modified (even by 1 byte) |
| 🧾 **Certificate of Authenticity** | Generate a formatted digital certificate for any registered doc |
| 🌳 **Merkle Root** | Batch-verify multiple documents using blockchain-style Merkle tree |
| 📊 **Vault Stats** | View all documents registered by a user |
| 🛡️ **Tamper Detection** | Mathematical proof of tampering — no guesswork |

---

## 🔬 Cryptographic Techniques

```
┌──────────────────────────────────────────────────────────────┐
│                  DOCUGUARD CRYPTO PIPELINE                   │
├──────────────────────────────────────────────────────────────┤
│                                                              │
│   Your Document (PDF / DOCX / TXT / any file)               │
│          │                                                   │
│          ├──► SHA-256  ──────────────► 64-char fingerprint   │
│          │    (Industry standard, 256-bit)                   │
│          │                                                   │
│          ├──► SHA3-256 (Keccak) ─────► 64-char fingerprint   │
│          │    (Next-gen, different math design)              │
│          │                                                   │
│          ├──► HMAC-SHA256 + Secret Key ► Auth Signature      │
│          │    (Only this system can produce this)            │
│          │                                                   │
│          └──► Document ID ──────────► DG-XXXXXXXXXXXXXXXX   │
│               SHA256(hash + filename + secret)               │
│                                                              │
│   For batch documents:                                       │
│   [hash1, hash2, hash3...] ──► Merkle Tree ──► Merkle Root  │
│                                                              │
└──────────────────────────────────────────────────────────────┘
```

### Algorithm Breakdown

| Algorithm | Role | Why It's Used |
|---|---|---|
| **SHA-256** | Primary 256-bit fingerprint | Industry standard, collision-resistant, one-way |
| **HMAC-SHA256** | Authenticated MAC signature | Secret-key based — forgery-resistant without the key |
| **SHA3-256 (Keccak)** | Secondary fingerprint | Different mathematical foundation than SHA-2 |
| **Merkle Tree** | Batch document root hash | O(log n) verification — foundation of blockchains |
| **Document ID** | Unique reproducible identifier | `SHA256(hash + filename + secret)` — tied to content |

### Avalanche Effect (Why It Works)

```
Original:  "Contract v1.0"  →  SHA-256: a3f9c2e1b4d8...
Tampered:  "Contract v1.1"  →  SHA-256: 7f2e8a1c9b4d...
                                         ^^^^^^^^^^^^^^ COMPLETELY DIFFERENT
```
Even changing **one character** produces a totally different hash — making tampering instantly detectable.

---

## 🛠️ Tech Stack

| Tool / Library | Version | Purpose |
|---|---|---|
| **Python** | 3.10+ | Core language |
| **python-telegram-bot** | 21.5 | Async Telegram Bot API framework |
| **hashlib** | stdlib | SHA-256, SHA3-256 hashing |
| **hmac** | stdlib | HMAC-SHA256 keyed authentication |
| **python-dotenv** | 1.0.1 | Secure environment variable loading |
| **cryptography** | 43.0.1 | Extended cryptographic primitives |
| **Pillow** | 10.4.0 | Image processing (certificate generation) |
| **pytest** | Latest | Unit testing framework |
| **JSON** | stdlib | Flat-file document fingerprint registry |

---

## 📁 Project Structure

```
DocuGuard/
│
├── src/                          ← Source code
│   ├── bot.py                    ← 🤖 Main Telegram bot (run this)
│   ├── crypto_engine.py          ← 🔐 SHA-256, HMAC, SHA3, Merkle engine
│   ├── document_store.py         ← 💾 Fingerprint registry (JSON store)
│   └── demo_cli.py               ← 🧪 CLI demo — test without Telegram
│
├── tests/                        ← Automated tests
│   ├── __init__.py
│   └── test_crypto.py            ← ✅ 26 unit tests (all passing)
│
├── docs/                         ← Documentation
│   ├── HOW_TO_RUN.md             ← Quick run guide (3 methods)
│   └── GITHUB_UPLOAD_GUIDE.md    ← Step-by-step GitHub upload
│
├── data/                         ← Auto-created at runtime
│   └── registry.json             ← Document fingerprint database
│
├── .env.example                  ← ⚙️ Config template (copy → .env)
├── .env                          ← 🔒 YOUR secrets (never commit!)
├── .gitignore                    ← 🙈 Protects secrets from GitHub
├── requirements.txt              ← 📦 All Python dependencies
│
├── README.md                     ← 📖 This file
├── SETUP.md                      ← ⚙️ Full setup guide (Windows/Linux/Mac)
├── SECURITY.md                   ← 🛡️ Security policy & vulnerability reporting
├── CONTRIBUTORS.md               ← 👥 Author & contribution guide
├── CHANGELOG.md                  ← 📋 Version history
└── LICENSE                       ← 📜 MIT License
```

---

## 🚀 Installation

### Prerequisites

- Python 3.10 or higher
- pip (Python package manager)
- A Telegram account
- Internet connection

### Step 1 — Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/DocuGuard.git
cd DocuGuard
```

Or download the ZIP and extract it.

### Step 2 — Create Virtual Environment (Recommended)

```bash
# Linux / macOS
python3 -m venv venv
source venv/bin/activate

# Windows
python -m venv venv
venv\Scripts\activate
```

### Step 3 — Install Dependencies

```bash
pip install -r requirements.txt
```

---

## ⚙️ Configuration

### Step 4 — Create Your Telegram Bot

1. Open Telegram → search **`@BotFather`** (official, blue tick)
2. Send `/newbot`
3. Enter bot name: `DocuGuard`
4. Enter username: `docuguard_yourname_bot` (must end in `bot`)
5. **Copy the token** — looks like: `1234567890:ABCdefGHIjklMNOpqrSTUvwxYZ`

### Step 5 — Set Up Environment File

```bash
# Copy the template
cp .env.example .env        # Linux/macOS
copy .env.example .env      # Windows
```

Open `.env` and fill in your values:

```env
TELEGRAM_BOT_TOKEN=1234567890:ABCdefGHIjklMNOpqrSTUvwxYZ
SECRET_KEY=your-strong-random-key-here
```

Generate a strong secret key:

```bash
python -c "import secrets; print(secrets.token_hex(32))"
```

> ⚠️ **NEVER share or commit your `.env` file.** It is blocked by `.gitignore`.

---

## ▶️ Running the Bot

### Method 1 — CLI Demo (No Telegram Needed) ⚡

Test all cryptographic operations instantly, no bot token required:

```bash
python src/demo_cli.py
```

Expected output:
```
🔐 DOCUGUARD — Cryptographic Document Verification

📌 DEMO 1: REGISTERING A DOCUMENT
  🆔 Document ID: DG-96C568B3A93AC4093DCCAB2EFBEA17C7
  🔷 SHA-256:     f1f7b85cef2dbe50fd9f82cbe0e18f...
  🔶 HMAC-SHA256: 7cda44d99d18bab2f0e93c4a7d91b1...
  🔹 SHA3-256:    073f6c5f928814bac6e1f4c2a9b3d0...

📌 DEMO 2: VERIFYING ORIGINAL DOCUMENT
  ✅ VERIFICATION PASSED — Document is AUTHENTIC!

📌 DEMO 3: DETECTING TAMPERED DOCUMENT
  🚨 TAMPERING DETECTED! Document has been MODIFIED!

📌 DEMO 4: MERKLE ROOT (BATCH VERIFICATION)
  🌳 Merkle Root: fda5ea3fbbee5ab888c4e7f9a2d13b...
```

### Method 2 — Run Tests

```bash
pip install pytest
python -m pytest tests/ -v
```

Expected: `26 passed in 0.03s`

### Method 3 — Full Telegram Bot

```bash
python src/bot.py
```

Expected:
```
🚀 DocuGuard Bot starting...
✅ Bot is running! Press Ctrl+C to stop.
```

Then open Telegram → search your bot → send `/start`

---

## 📱 Bot Commands

| Command | Description |
|---|---|
| `/start` | Welcome screen with interactive buttons |
| `/register` | Set mode → register the next file you send |
| `/verify` | Set mode → verify the next file you send |
| `/mystats` | View all your registered documents |
| `/certificate <doc_id>` | Get a formatted authenticity certificate |
| `/help` | Full help — how cryptography works, all commands |
| `/reset` | Clear current session mode |

> **Tip:** Just send any file without a command — the bot will ask what you want to do!

---

## 🔍 How It Works

```
REGISTER FLOW:
──────────────
User sends contract.pdf
       ↓
Bot downloads file bytes
       ↓
SHA-256(bytes)     = abc123...  ← Primary fingerprint
HMAC-SHA256(bytes) = def456...  ← Authenticated signature  
SHA3-256(bytes)    = ghi789...  ← Secondary fingerprint
DocID = DG-XYZ...              ← Unique identifier
       ↓
Store fingerprints ONLY (file is NOT saved)
       ↓
Return DocID + all hashes to user ✅

──────────────────────────────────────────

VERIFY FLOW (original file):
─────────────────────────────
User sends same contract.pdf
       ↓
SHA-256(bytes) = abc123...  ← MATCHES registry!
       ↓
✅ AUTHENTIC — registered by @Aman on 2025-06-13

──────────────────────────────────────────

VERIFY FLOW (tampered file):
─────────────────────────────
User sends edited contract.pdf (1 word changed)
       ↓
SHA-256(bytes) = zzz999...  ← DOES NOT MATCH!
       ↓
🚨 TAMPERED — document has been modified!
```

---

## 🧪 Testing

The test suite covers all cryptographic functions:

```bash
python -m pytest tests/ -v
```

```
tests/test_crypto.py::TestSHA256::test_known_hash           PASSED
tests/test_crypto.py::TestSHA256::test_avalanche_effect     PASSED
tests/test_crypto.py::TestHMAC::test_wrong_key_fails        PASSED
tests/test_crypto.py::TestMerkleRoot::test_order_matters    PASSED
tests/test_crypto.py::TestDocumentStore::test_tamper_detect PASSED
... (26 tests total)

============================== 26 passed in 0.03s ==============================
```

---

## 🔒 Security

- ✅ **Document contents are NEVER stored** — only cryptographic hashes
- ✅ **HMAC** prevents hash forgery without the secret key
- ✅ **Timing-safe comparison** via `hmac.compare_digest()` — prevents timing attacks
- ✅ **One-way functions** — hashes cannot be reversed to recover the original file
- ✅ **`.env` file** is git-ignored — secrets never reach GitHub

---

## 📈 Future Enhancements

- [ ] RSA digital signatures with private/public key pairs
- [ ] PDF certificate generation with QR code
- [ ] PostgreSQL / MongoDB backend for production scale
- [ ] Blockchain anchoring (Ethereum / IPFS)
- [ ] Webhook deployment on Railway / Heroku
- [ ] Multi-user document sharing & verification
- [ ] REST API endpoint for external integrations
