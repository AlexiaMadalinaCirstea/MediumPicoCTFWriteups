# PW Crack 3 – picoCTF Write-up

---

## Description

> Can you crack the password to get the flag?  
>
> Download the password checker script and ensure the `level3.flag.txt.enc` and `level3.hash.bin` files are in the same directory.  
>
> There are 7 potential passwords, and only 1 is correct. You must identify it by examining the script.

---

## Solution

This is a **reverse engineering and decryption** challenge. The task involves finding the correct password from a provided list, verifying it using an MD5 hash, and then decrypting an encrypted flag using a custom XOR function.

---

### Step-by-step

#### 1. Inspect the Python script

The file `level3.py` contains the following components:

- A custom XOR function `str_xor(secret, key)`
- A hardcoded list of 7 possible passwords:
  ```python
  pos_pw_list = ["f09e", "4dcf", "87ab", "dba8", "752e", "3961", "f159"]
  ```
- The password verification uses MD5:
  ```python
  def hash_pw(pw_str):
      m = hashlib.md5()
      m.update(pw_str.encode())
      return m.digest()
  ```
- The flag is decrypted only if the password's hash matches the stored hash in `level3.hash.bin`.

---

#### 2. Determine the correct password

We iterate through the `pos_pw_list`, hashing each with MD5 and comparing it to the contents of `level3.hash.bin`.

Python code:
```python
import hashlib

with open("level3.hash.bin", "rb") as f:
    correct_pw_hash = f.read()

pos_pw_list = ["f09e", "4dcf", "87ab", "dba8", "752e", "3961", "f159"]

def hash_pw(pw_str):
    m = hashlib.md5()
    m.update(pw_str.encode())
    return m.digest()

for pw in pos_pw_list:
    if hash_pw(pw) == correct_pw_hash:
        print(f"Correct password: {pw}")
        break
```

This reveals the correct password is:

```
87ab
```

---

#### 3. Decrypt the flag

Use the provided XOR function to decrypt `level3.flag.txt.enc` using the correct password:

```python
def str_xor(secret, key):
    new_key = key
    i = 0
    while len(new_key) < len(secret):
        new_key = new_key + key[i]
        i = (i + 1) % len(key)        
    return "".join([chr(ord(secret_c) ^ ord(new_key_c)) for (secret_c, new_key_c) in zip(secret, new_key)])

with open("level3.flag.txt.enc", "rb") as f:
    flag_enc = f.read()

flag = str_xor(flag_enc.decode(), "87ab")
print("Flag:", flag)
```

---

## Final Flag

```
picoCTF{m45h_fl1ng1ng_cd6ed2eb}
```

---

## Takeaway

This challenge demonstrates how to inspect a script for embedded logic, recognize password hashing, and decrypt XOR-based ciphers. Reverse engineering small Python challenges like this is a great way to build skills for larger CTFs.