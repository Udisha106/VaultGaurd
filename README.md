# VaultGuard

**A personal cybersecurity toolkit with a modern dark GUI, built with Python and Tkinter.**

## About

VaultGuard bundles three everyday security tools into one desktop app: a password strength tester and generator, a file encryption vault, and a phishing link scanner. Everything runs locally on your device. No accounts, no cloud, and no network calls.

The project focuses on two things: practical security habits (cryptographically secure randomness, authenticated encryption, never storing the passwords you test) and a polished, custom-drawn interface that goes beyond default Tkinter styling.

## Features

### Password Lab
- **Live strength tester**: analyses a password as you type and shows a 5-segment strength meter.
- **Entropy and crack-time estimate**: shows approximate bits of entropy and the estimated time for an offline attack.
- **Checklist**: length, upper/lower case, numbers, symbols and common-password check.
- **Pattern warnings**: detects repeated characters, predictable sequences and very common passwords.
- **Secure generator**: 8 to 64 characters, with toggles for uppercase, lowercase, digits and symbols, plus an option to avoid look-alike characters (O/0, l/1).
- **Safe clipboard**: copied passwords are wiped from the clipboard after 30 seconds.
- **Privacy**: tested passwords are never stored. Only the result label (e.g. "Strong") is saved to history.

### File Vault
- **Encrypt any file** into an `.enc` file with a separately saved `.key` file.
- **Decrypt** by selecting the `.enc` file and its matching `.key` file.
- **Tamper detection**: a wrong key or a modified file is reported instead of producing corrupted output.
- **Overwrite protection**: the output can never overwrite the original file.

### Link Scanner
- **Offline phishing checks**: the site is never opened.
- Detects:
  - missing HTTPS
  - `@` tricks that hide the real destination
  - raw IP addresses
  - punycode (look-alike) domains
  - non-standard ports
  - link shorteners
  - suspicious domain endings
  - excessive hyphens or subdomains
  - heavy URL encoding
  - bait words such as "login", "verify" and "prize"
  - fake or look-alike brand domains (PayPal, Google, Amazon and more)
- **Risk gauge and severity tags** (High / Medium / Low / OK) with a clear verdict.
- **Recent scans table** for quick reference.

### Home Dashboard
- Time-aware greeting, date and a random security tip.
- Total checks counter and per-tool counters.
- Recent activity feed and a donut chart showing the activity mix.
- One-click history clearing.

## Technologies Used

| Technology | Purpose |
|---|---|
| Python 3.8+ | Core language |
| Tkinter / ttk | GUI framework (custom canvas-drawn buttons, chips, charts) |
| `cryptography` (Fernet) | Authenticated symmetric file encryption |
| `secrets` | Cryptographically secure password generation |
| SQLite (`sqlite3`) | Local activity history |
| `urllib`, `ipaddress`, `re`, `math` | URL parsing, IP checks, pattern matching, entropy maths |

## Getting Started

### Prerequisites
- Python 3.8 or newer
- Tkinter (included with the standard Python installer on Windows and macOS; on Linux install `python3-tk`)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/Udisha106/VaultGaurd.git
   cd VaultGaurd
   ```

2. **(Optional) Create a virtual environment**
   ```bash
   python -m venv venv
   venv\Scripts\activate        # Windows
   source venv/bin/activate     # macOS / Linux
   ```

3. **Install dependencies**
   ```bash
   python -m pip install -r requirements.txt
   ```

4. **Run the app**
   ```bash
   python main.py
   ```

> If `cryptography` is not installed, the app still opens, but File Vault will ask you to install it before encrypting or decrypting.

## Project Structure

```
VaultGuard/
├── main.py            # Entire application
│                      #   - Logic: assess_password, generate_password, scan_url
│                      #   - Custom widgets: Pill, Chip, card helpers
│                      #   - App shell: VaultGuard (sidebar, navigation, database)
│                      #   - Pages: HomePage, PasswordPage, FilePage, LinkPage
├── requirements.txt   # Python dependencies
├── README.md          # Project documentation
├── .gitignore         # Keeps personal data and keys out of git
└── vaultguard.db      # Created automatically on first run (not committed)
```

## Data Storage

- All data stays on your computer. VaultGuard makes no network requests.
- Activity history is stored in a local **SQLite** file, `vaultguard.db`, created next to `main.py`.
- Each record holds only a timestamp, a category (Password / File / URL), a short item label and the result (e.g. "Strong", "Encrypted", "High risk").
- **Passwords are never saved.** Only the strength label is recorded.
- Encrypted files (`.enc`) and key files (`.key`) are saved wherever you choose. Store them in **different locations**: anyone with both can decrypt the file, and without the key the file cannot be recovered.
- `vaultguard.db`, `*.key` and `*.enc` are listed in `.gitignore` so they are never uploaded to GitHub.

## Future Enhancements

- **Encrypted password vault**: store site, username and password entries protected by a master password.
- **Breach check**: look up passwords with the HaveIBeenPwned k-anonymity API (only a partial hash leaves the device).
- **Password-based file encryption**: derive the key from a passphrase instead of a separate `.key` file.
- **Threaded encryption with a progress bar**, plus chunked reading for large files.
- **Passphrase generator** (random-word passwords such as `maple-river-ocean-tiger`).
- **File integrity checker** using SHA-256 hashes.
- **TOTP two-factor code generator**.
- **QR code checker** that extracts a URL from an image and scans it.
- **Email / message phishing analyser**.
- **History export to CSV** and filtering.
- **Light/dark theme toggle** and keyboard shortcuts.
- **Drag-and-drop** file support.


## Team Members
Project: VaultGuard – Making Everyday Cybersecurity Simple
1. Udisha  – RA2511003011714
2. Shreyas – RA2511003011699
3. Sritam – RA2511003011682


## Disclaimer

The Link Scanner and password strength estimates are heuristic tools meant to support good habits. They are not a guarantee that a site or password is safe.
