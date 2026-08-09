# Password Strength Checker

A tool that calculates password entropy, detects weak patterns (sequential
characters, keyboard walks, repeated characters, common passwords), and
estimates crack time under different attack scenarios. Everything runs
locally — no data is ever sent anywhere.

Comes in two versions:

| File | Type | Use it when... |
|---|---|---|
| `password-vault-analyzer.html` | GUI (browser) | you want a visual check — just open the file in any browser |
| `password_checker.py` | CLI (terminal) | you want to run it from the terminal, script it, or bulk-check a file of passwords |

Both use the same underlying logic — just different interfaces.

## Features

- Entropy calculation based on character pool (lowercase/uppercase/digits/symbols)
- Weak pattern detection: common passwords, sequential characters, keyboard
  walks, repeated characters, date/year patterns
- Crack-time estimate for 3 attack scenarios: online (throttled), offline
  (bcrypt), offline (GPU rig)
- 0–100 strength score and verdict
- Strong password generator

## Usage

### GUI version
Just open `password-vault-analyzer.html` in a browser. Type a password and
everything updates live.

### CLI version
Requires Python 3.10+, no external packages.

```bash
# Interactive — password hidden while typing
python3 password_checker.py

# Pass the password directly
python3 password_checker.py -p "MyP@ssw0rd123"

# Generate a strong password
python3 password_checker.py -g --length 20

# Bulk check from a file (one password per line)
python3 password_checker.py -f passwords.txt

# Mask the password in the printed report
python3 password_checker.py -p "MyP@ssw0rd123" --mask
```

## Limitations

- Not a cryptographic-grade audit tool — a heuristic-based estimate for
  general and educational use.
- The common-password and dictionary word lists are small and built-in; no
  check against large breach databases (e.g. HaveIBeenPwned).
- Crack-time numbers are approximate and depend on the attacker's actual
  hardware and algorithm.
