#!/usr/bin/env python3
"""
Advanced Password Strength Checker
------------------------------------
Terminal-based tool. Checks entropy, common patterns, dictionary words,
and estimates crack time under different attack scenarios.

Usage:
    python password_checker.py
    python password_checker.py --password "MyP@ssw0rd123"
    python password_checker.py --file passwords.txt
"""

import argparse
import getpass
import math
import re
import sys
from datetime import datetime

# ---------------------------------------------------------------------------
# Data: common passwords + keyboard patterns
# ---------------------------------------------------------------------------

COMMON_PASSWORDS = {
    "password", "123456", "123456789", "12345678", "12345", "1234567",
    "qwerty", "abc123", "password1", "admin", "welcome", "letmein",
    "monkey", "football", "iloveyou", "000000", "111111", "123123",
    "dragon", "master", "sunshine", "princess", "qwerty123", "1q2w3e4r",
    "passw0rd", "trustno1", "superman", "hello", "charlie", "aa123456",
    "1234", "google", "access", "shadow", "michael", "jennifer", "2000",
    "696969", "batman", "donald", "666666", "7777777", "121212",
    "freedom", "whatever", "ninja", "azerty", "liverpool", "asdfgh",
    "starwars", "121212", "flower", "hottie", "loveme", "zaq1zaq1",
}

KEYBOARD_ROWS = ["qwertyuiop", "asdfghjkl", "zxcvbnm", "1234567890"]
SEQUENCES = ["abcdefghijklmnopqrstuvwxyz", "0123456789"]

# A small built-in wordlist for a lightweight "dictionary word" check.
# (Not exhaustive — just common English words/names people build passwords from.)
COMMON_WORDS = {
    "love", "hate", "money", "dragon", "shadow", "master", "hunter",
    "killer", "summer", "winter", "spring", "autumn", "computer",
    "internet", "baseball", "basketball", "soccer", "hockey", "cricket",
    "welcome", "freedom", "happy", "angel", "devil", "ninja", "pirate",
    "wizard", "dream", "family", "friend", "forever", "always", "never",
    "phoenix", "thunder", "diamond", "silver", "golden", "purple",
    "orange", "yellow", "trust", "secret", "secure", "system", "server",
    "admin", "administrator", "root", "user", "guest", "test",
}

# ---------------------------------------------------------------------------
# Analysis
# ---------------------------------------------------------------------------

def has_sequential(pwd: str) -> bool:
    low = pwd.lower()
    for seq in SEQUENCES:
        for i in range(len(seq) - 2):
            fwd = seq[i:i + 3]
            rev = fwd[::-1]
            if fwd in low or rev in low:
                return True
    return False


def has_keyboard_walk(pwd: str) -> bool:
    low = pwd.lower()
    for row in KEYBOARD_ROWS:
        for i in range(len(row) - 2):
            fwd = row[i:i + 3]
            rev = fwd[::-1]
            if fwd in low or rev in low:
                return True
    return False


def has_repeats(pwd: str) -> bool:
    return bool(re.search(r"(.)\1\1", pwd))


def has_date_like(pwd: str) -> bool:
    return bool(re.search(r"(19|20)\d{2}", pwd)) or bool(re.search(r"\b\d{1,2}[/\-]\d{1,2}\b", pwd))


def contains_dictionary_word(pwd: str) -> str | None:
    low = pwd.lower()
    for word in COMMON_WORDS:
        if len(word) >= 4 and word in low:
            return word
    return None


def char_pool_size(pwd: str) -> tuple[int, dict]:
    has_lower = bool(re.search(r"[a-z]", pwd))
    has_upper = bool(re.search(r"[A-Z]", pwd))
    has_digit = bool(re.search(r"[0-9]", pwd))
    has_symbol = bool(re.search(r"[^a-zA-Z0-9]", pwd))

    pool = 0
    if has_lower:
        pool += 26
    if has_upper:
        pool += 26
    if has_digit:
        pool += 10
    if has_symbol:
        pool += 32

    return pool or 1, {
        "lower": has_lower,
        "upper": has_upper,
        "digit": has_digit,
        "symbol": has_symbol,
    }


def format_time(seconds: float) -> str:
    if seconds < 1:
        return "instantly"
    minutes = seconds / 60
    if minutes < 1:
        return f"{seconds:.0f} seconds"
    hours = minutes / 60
    if hours < 1:
        return f"{minutes:.0f} minutes"
    days = hours / 24
    if days < 1:
        return f"{hours:.0f} hours"
    months = days / 30
    if months < 1:
        return f"{days:.0f} days"
    years = days / 365
    if years < 1:
        return f"{months:.0f} months"
    if years < 100:
        return f"{years:.0f} years"
    if years < 1000:
        return f"{years/100:.1f} centuries"
    if years < 1_000_000:
        return f"{years/1000:.1f} thousand years"
    if years < 1_000_000_000:
        return f"{years/1_000_000:.1f} million years"
    return "longer than the age of the universe"


def analyze_password(pwd: str) -> dict:
    length = len(pwd)
    pool, composition = char_pool_size(pwd)
    entropy = length * math.log2(pool) if length > 0 else 0.0

    warnings = []
    lower_pwd = pwd.lower()

    if pwd == "":
        warnings.append(("HIGH", "Empty password."))
        entropy = 0

    if lower_pwd in COMMON_PASSWORDS:
        warnings.append(("HIGH", "This is a well-known common password — appears in breach dictionaries."))
        entropy = min(entropy, 10)

    if has_sequential(pwd):
        warnings.append(("HIGH", 'Sequential character pattern found (e.g. "abc", "123").'))
        entropy *= 0.6

    if has_keyboard_walk(pwd):
        warnings.append(("HIGH", 'Keyboard-walk pattern found (e.g. "qwerty", "asdf").'))
        entropy *= 0.6

    if has_repeats(pwd):
        warnings.append(("MEDIUM", "Same character repeated 3+ times in a row."))
        entropy *= 0.8

    if has_date_like(pwd):
        warnings.append(("MEDIUM", "Looks like it contains a year or date — easy to guess."))
        entropy *= 0.9

    dict_word = contains_dictionary_word(pwd)
    if dict_word:
        warnings.append(("MEDIUM", f'Contains a common dictionary word ("{dict_word}").'))
        entropy *= 0.85

    if 0 < length < 8:
        warnings.append(("HIGH", "Length under 8 characters — crackable very quickly by brute force."))
    elif 8 <= length < 12:
        warnings.append(("MEDIUM", "Length under 12 characters — consider making it longer."))

    unique_chars = len(set(pwd))
    if length >= 6 and unique_chars < length * 0.6:
        warnings.append(("MEDIUM", "Low ratio of unique characters — more variety increases entropy."))

    if not composition["symbol"] and length > 0:
        warnings.append(("MEDIUM", "No symbols/special characters used (!@#$% etc.)."))

    if length > 0 and not (composition["upper"] and composition["lower"]):
        warnings.append(("MEDIUM", "Only one letter case used — mix upper and lower case."))

    entropy = max(0.0, entropy)
    score = min(100, round((entropy / 90) * 100))

    if score < 25:
        verdict = "VERY WEAK"
    elif score < 50:
        verdict = "WEAK"
    elif score < 75:
        verdict = "FAIR"
    elif score < 90:
        verdict = "STRONG"
    else:
        verdict = "VERY STRONG"

    # crack time: average guesses = half the keyspace
    guesses = (2 ** entropy) / 2 if entropy > 0 else 0
    crack_times = {
        "Online (throttled, ~100/hr)": format_time(guesses / (100 / 3600)) if guesses else "instantly",
        "Offline slow hash (bcrypt, ~10k/s)": format_time(guesses / 10_000) if guesses else "instantly",
        "Offline fast (GPU rig, ~10B/s)": format_time(guesses / 1e10) if guesses else "instantly",
    }

    return {
        "length": length,
        "pool": pool,
        "composition": composition,
        "unique_chars": unique_chars,
        "entropy": entropy,
        "score": score,
        "verdict": verdict,
        "warnings": warnings,
        "crack_times": crack_times,
    }


# ---------------------------------------------------------------------------
# Display
# ---------------------------------------------------------------------------

BAR_WIDTH = 40


def render_bar(score: int) -> str:
    filled = round((score / 100) * BAR_WIDTH)
    return "█" * filled + "░" * (BAR_WIDTH - filled)


def print_report(pwd: str, result: dict, mask: bool = False):
    shown = ("*" * len(pwd)) if mask else pwd
    print("=" * 62)
    print(f" PASSWORD STRENGTH REPORT   {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}")
    print("=" * 62)
    print(f" Password tested : {shown!r}")
    print(f" Length          : {result['length']}")
    print(f" Character pool  : {result['pool']}")
    print(f" Unique chars    : {result['unique_chars']} / {result['length']}")
    print(f" Entropy         : {result['entropy']:.1f} bits")
    print()
    print(f" Verdict         : {result['verdict']}  (score {result['score']}/100)")
    print(f" [{render_bar(result['score'])}]")
    print()

    comp = result["composition"]
    def flag(v): return "yes" if v else "no"
    print(" Composition:")
    print(f"   lowercase (a-z) : {flag(comp['lower'])}")
    print(f"   UPPERCASE (A-Z) : {flag(comp['upper'])}")
    print(f"   digits    (0-9) : {flag(comp['digit'])}")
    print(f"   symbols   (!@#) : {flag(comp['symbol'])}")
    print()

    print(" Estimated crack time:")
    for label, t in result["crack_times"].items():
        print(f"   {label:<34}: {t}")
    print()

    if result["warnings"]:
        print(" Findings:")
        for level, msg in result["warnings"]:
            print(f"   [{level:<6}] {msg}")
    else:
        print(" Findings: no common weak patterns detected.")
    print("=" * 62)
    print()


def generate_strong_password(length: int = 16) -> str:
    import secrets
    import string

    lower = string.ascii_lowercase
    upper = string.ascii_uppercase
    digits = string.digits
    symbols = "!@#$%^&*()-_=+[]{}"
    all_chars = lower + upper + digits + symbols

    pwd_chars = [
        secrets.choice(lower),
        secrets.choice(upper),
        secrets.choice(digits),
        secrets.choice(symbols),
    ]
    pwd_chars += [secrets.choice(all_chars) for _ in range(length - len(pwd_chars))]
    secrets.SystemRandom().shuffle(pwd_chars)
    return "".join(pwd_chars)


# ---------------------------------------------------------------------------
# CLI
# ---------------------------------------------------------------------------

def main():
    parser = argparse.ArgumentParser(description="Advanced Password Strength Checker")
    parser.add_argument("--password", "-p", help="Password to check (visible in shell history — prefer interactive mode)")
    parser.add_argument("--file", "-f", help="Path to a text file with one password per line to check in bulk")
    parser.add_argument("--generate", "-g", action="store_true", help="Generate a strong random password instead")
    parser.add_argument("--length", "-l", type=int, default=16, help="Length for --generate (default 16)")
    parser.add_argument("--mask", "-m", action="store_true", help="Mask the password in the report output")
    args = parser.parse_args()

    if args.generate:
        pwd = generate_strong_password(args.length)
        print(f"\nGenerated password: {pwd}\n")
        print_report(pwd, analyze_password(pwd))
        return

    if args.file:
        try:
            with open(args.file, "r", encoding="utf-8") as f:
                lines = [line.strip() for line in f if line.strip()]
        except OSError as e:
            print(f"Could not read file: {e}", file=sys.stderr)
            sys.exit(1)
        for pwd in lines:
            print_report(pwd, analyze_password(pwd), mask=args.mask)
        return

    if args.password:
        pwd = args.password
    else:
        pwd = getpass.getpass("Enter password to check (input hidden): ")

    print_report(pwd, analyze_password(pwd), mask=args.mask)


if __name__ == "__main__":
    main()
