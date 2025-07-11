# PW Crack 4 – picoCTF Write-up

---

## Description

> Can you crack the password to get the flag?
>
> You're given a password checker script, an encrypted flag, and a binary hash file. Only 1 of the 100 possible passwords is correct.

---

## Files Provided

- `level4.py`: Password checker script with encryption logic
- `level4.flag.txt.enc`: The encrypted flag
- `level4.hash.bin`: The correct password hash to match against

---

## Objective

- Match the correct password from a provided list using hash comparison.
- Decrypt the flag using the correct password.

---

## Analysis

The script provides:
- A list of 100 possible passwords (`pos_pw_list`)
- A hashing function:
```python
def hash_pw(pw_str):
    m = hashlib.md5()
    m.update(pw_str.encode())
    return m.digest()
```
- The correct password’s MD5 hash is stored in `level4.hash.bin`
- The encrypted flag is XOR'd with the correct password using:
```python
def str_xor(secret, key):
    while len(new_key) < len(secret):
        new_key += key[i % len(key)]
    return ''.join([chr(ord(s) ^ ord(k)) for s, k in zip(secret, new_key)])
```

---

## Solution Steps

1. Load all possible passwords from the script.
2. Compute the MD5 hash for each and compare with the hash in `level4.hash.bin`.
3. Identify the password that matches.
4. Use `str_xor()` to decrypt the flag using the correct password.

---

## Result

The correct password found was:

```
8b95
```

Using this password, the flag decrypted as:

```
picoCTF{fl45h_5pr1ng1ng_cf341ff1}
```

---
