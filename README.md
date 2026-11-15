# VaultGuard – Personal Cybersecurity Toolkit

A four-page desktop mini-project built with Python Tkinter.

## Pages
1. **Home** – greeting, stats, activity chart and recent history.
2. **Password Lab** – live strength meter (entropy + crack-time estimate) and a secure generator.
3. **File Vault** – Encrypt / Decrypt tabs with step-by-step flow (Fernet via `cryptography`).
4. **Link Scanner** – offline URL heuristics with a risk gauge and severity-tagged findings.

## Run
```bash
python -m pip install cryptography
python main.py
```
Python 3.9+; Tkinter ships with Python (Linux: `sudo apt install python3-tk`).

## Notes
- Encryption produces a `.enc` file and a separate `.key` file. Lose the key and the file is unrecoverable.
- Typed passwords are analysed in memory and never stored; only the rating is saved.
- Link scanning is heuristic and educational; it does not contact the internet.
- History is stored in `vaultguard.db` (created automatically next to `main.py`).
