
# # Substitution1 – picoCTF Write-up

---

## Description
A second message has come in the mail, and it seems almost identical to the first one. Maybe the same thing will work again.

> Download the message here: `message (1).txt`

---

## Challenge Type
Cryptography

---

## Provided
- A `.txt` file containing a ciphertext.
- The **first line** of the file contains the **substitution key**: `ZWDGJXTKFLCPVEUNYMBSHOQAZR`
- The remaining content is the encrypted message including a flag.

---

## Objective
Decrypt the message using a monoalphabetic substitution cipher with the provided key.

---

## Solution

### Step 1: Understand the Cipher
The first line is a 26-letter string that maps the **alphabet** to a substitution cipher. Specifically:
- A -> Z
- B -> W
- C -> D
- D -> G
- E -> J
- ...
- Z -> R

To decrypt, we reverse this mapping.

### Step 2: Extract the Key and Ciphertext
From `message (1).txt`:
```
ZWDGJXTKFLCPVEUNYMBSHOQAZR
cbzjZWD{DF3LP3VZS_4774ZN5_4F3_Z001_4871X6DT}
```

### Step 3: Implement Decryption
We created a Python script that:
1. Reverses the substitution mapping
2. Applies it to the ciphertext
3. Prints the plaintext

### Python Script
```python
def build_reverse_substitution_map(key):
    alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    return {key[i]: alphabet[i] for i in range(26)}

def decrypt_substitution(text, mapping):
    result = ""
    for char in text:
        if char.upper() in mapping:
            decrypted = mapping[char.upper()]
            result += decrypted if char.isupper() else decrypted.lower()
        else:
            result += char
    return result

key = "ZWDGJXTKFLCPVEUNYMBSHOQAZR"
cipher_text = "cbzjZWD{DF3LP3VZS_4774ZN5_4F3_Z001_4871X6DT}"

reverse_map = build_reverse_substitution_map(key)
print(decrypt_substitution(cipher_text, reverse_map))
```

### Output:
```
picoCTF{FR3QU3NCY_4774CK5_4R3_C001_4871E6FB}
```

---

## Flag
```
picoCTF{FR3QU3NCY_4774CK5_4R3_C001_4871E6FB}
```


