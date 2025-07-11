# PW Crack 5 – picoCTF Write-up

---

## Description

> Can you crack the password to get the flag?
>
> You're given a password checker script, an encrypted flag, a hash file, and a **dictionary** of possible passwords.

---

## Files Provided

- `level5.py`: The script with encryption and hashing logic
- `level5.flag.txt.enc`: The encrypted flag file
- `level5.hash.bin`: The hash of the correct password
- `dictionary.txt`: A list of all potential passwords

---

## Objective

1. Find the password that matches the hash in `level5.hash.bin`
2. Use the password to decrypt the encrypted flag using the XOR function from the script

---

## Analysis

The code includes:
- A custom XOR decryption function:
```python
def str_xor(secret, key):
    while len(key) < len(secret):
        key += key[i % len(key)]
    return ''.join([chr(ord(s) ^ ord(k)) for s, k in zip(secret, key)])
```

- The hash comparison uses:
```python
def hash_pw(pw_str):
    pw_bytes = bytearray()
    pw_bytes.extend(pw_str.encode())
    m = hashlib.md5()
    m.update(pw_bytes)
    return m.digest()
```

- We simply iterate through all passwords in `dictionary.txt` and find the one whose MD5 hash matches `level5.hash.bin`.

---

## Solution

1. Load the hash from `level5.hash.bin`
2. Load and iterate through each password in `dictionary.txt`
3. Hash each one and compare to the stored hash
4. When a match is found, use `str_xor()` to decrypt `level5.flag.txt.enc`

---

## Result

The correct password was:

```
eee0
```

And the decrypted flag is:

```
picoCTF{h45h_sl1ng1ng_fffcda23}
```

---
