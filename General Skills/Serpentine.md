# serpentine – picoCTF Write-up

---

## Description

> Welcome to the serpentine encourager! A Python script gives motivational messages and hides the flag behind a disguised function. You're given the source code to explore.

---

## Challenge Overview

You're presented with a Python script that runs a simple menu:

```text
a) Print encouragement
b) Print flag
c) Quit
```

Choosing option `b` doesn't print the flag — it says:
```
Oops! I must have misplaced the print_flag function! Check my source code!
```

We're told directly to look into the source.

---

## Solution

Upon examining the source code, we find this function:

```python
def print_flag():
  flag = str_xor(flag_enc, 'enkidu')
  print(flag)
```

But it's never called in the main program. Instead, we can extract `flag_enc` and `str_xor`, and manually decrypt it ourselves.

### XOR Decryption

The function:
```python
def str_xor(secret, key):
    while len(key) < len(secret):
        key += key[i % len(key)]
    return ''.join([chr(ord(s) ^ ord(k)) for s, k in zip(secret, key)])
```

The key used is `'enkidu'`.

### Encrypted Flag

```python
flag_enc = [0x15, 0x07, 0x08, ..., 0x14]  # total of 40 bytes
```

We decode and XOR each byte against the repeated `'enkidu'` key.

---

## Final Flag

```
picoCTF{7h3_r04d_l355_7r4v3l3d_ae0b80bd}
```

---
