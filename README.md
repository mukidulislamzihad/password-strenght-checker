# Password Strength Checker

একটা advanced, terminal-based (no GUI) পাসওয়ার্ড স্ট্রেংথ চেকার — শুধু Python standard library দিয়ে বানানো, কোনো এক্সট্রা ডিপেন্ডেন্সি লাগে না, ইন্টারনেটে কিছু পাঠায় না।

## ফিচার

- **Entropy calculation** — ক্যারেক্টার পুল (lower/upper/digit/symbol) অনুযায়ী bits হিসাব করে
- **Pattern detection**
  - Common password list (`password`, `123456`, `qwerty` ইত্যাদি)
  - Sequential characters (`abc`, `123`)
  - Keyboard-walk patterns (`qwerty`, `asdf`)
  - রিপিটেড ক্যারেক্টার (`aaa`, `111`)
  - Date/year প্যাটার্ন (`1998`, `12/25`)
  - Common dictionary word ম্যাচ
- **Crack-time estimate** — তিন ধরনের আক্রমণ সিনারিওতে:
  - Online (থ্রটলড, ~100 guess/hour)
  - Offline slow hash — bcrypt (~10k guess/sec)
  - Offline fast — GPU rig (~10B guess/sec)
- **Score + verdict** — 0–100 স্কোর এবং ASCII bar দিয়ে ভিজুয়াল
- **Strong password generator**
- **Bulk check** — ফাইল থেকে একসাথে অনেক পাসওয়ার্ড চেক করা যায়
- **Hidden input mode** — টাইপ করার সময় স্ক্রিনে দেখা যায় না (`getpass`)

## Requirements

- Python 3.10+ (শুধু `X | Y` টাইপ হিন্ট সিনট্যাক্সের জন্য; পুরনো ভার্সনে চালাতে চাইলে টাইপ হিন্ট বাদ দিলেই চলবে)
- কোনো external package লাগে না

## ব্যবহার

```bash
# Interactive — টাইপ করার সময় পাসওয়ার্ড দেখা যাবে না
python3 password_checker.py

# সরাসরি পাসওয়ার্ড দিয়ে (শেল হিস্ট্রিতে থেকে যাবে, তাই সাবধান)
python3 password_checker.py --password "MyP@ssw0rd123"
python3 password_checker.py -p "MyP@ssw0rd123"

# স্ট্রং পাসওয়ার্ড জেনারেট করা (ডিফল্ট length 16)
python3 password_checker.py --generate
python3 password_checker.py -g --length 20

# ফাইল থেকে একসাথে অনেকগুলো পাসওয়ার্ড চেক (এক লাইনে একটা করে)
python3 password_checker.py --file passwords.txt

# রিপোর্টে পাসওয়ার্ড masked (****) দেখাতে চাইলে
python3 password_checker.py -p "MyP@ssw0rd123" --mask
```

## Sample Output

```
==============================================================
 PASSWORD STRENGTH REPORT   2026-08-09 07:56:03
==============================================================
 Password tested : 'Tr0ub4dor&3Xk9!qLm'
 Length          : 18
 Character pool  : 94
 Unique chars    : 17 / 18
 Entropy         : 118.0 bits

 Verdict         : VERY STRONG  (score 100/100)
 [████████████████████████████████████████]

 Composition:
   lowercase (a-z) : yes
   UPPERCASE (A-Z) : yes
   digits    (0-9) : yes
   symbols   (!@#) : yes

 Estimated crack time:
   Online (throttled, ~100/hr)       : longer than the age of the universe
   Offline slow hash (bcrypt, ~10k/s): longer than the age of the universe
   Offline fast (GPU rig, ~10B/s)    : longer than the age of the universe

 Findings: no common weak patterns detected.
==============================================================
```

## কীভাবে কাজ করে (সংক্ষেপে)

1. পাসওয়ার্ডে কোন কোন ক্যারেক্টার সেট আছে (lower/upper/digit/symbol) দেখে **pool size** বের করা হয়।
2. `entropy = length × log2(pool)` দিয়ে raw entropy হিসাব করা হয়।
3. পরিচিত দুর্বল প্যাটার্ন (common password, sequential, keyboard walk, repeats, dictionary word) পাওয়া গেলে entropy-তে পেনাল্টি বসানো হয় — কারণ এগুলো raw math-এর চেয়ে বাস্তবে অনেক দ্রুত গেস করা যায়।
4. চূড়ান্ত entropy থেকে score (0–100) ও verdict বের করা হয়।
5. Average guesses (`2^entropy / 2`) কে বিভিন্ন attack speed দিয়ে ভাগ করে crack-time বের করা হয়।

## সীমাবদ্ধতা

- এটা কোনো ক্রিপ্টোগ্রাফিক-গ্রেড অডিট টুল না — শিক্ষামূলক ও সাধারণ ব্যবহারের জন্য একটা heuristic-ভিত্তিক এস্টিমেট।
- Dictionary word list ও common password list ছোট, বিল্ট-ইন — কোনো বড় breach ডেটাবেসের সাথে চেক করে না (যেমন HaveIBeenPwned)।
- Crack-time এর সংখ্যাগুলো approximate; আসল আক্রমণকারীর হার্ডওয়্যার/অ্যালগরিদম অনুযায়ী কমবেশি হতে পারে।

## ফাইল

- `password_checker.py` — মূল স্ক্রিপ্ট, dependency-free
