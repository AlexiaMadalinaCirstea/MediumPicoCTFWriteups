# rotation – picoCTF Write-up

---

## Description

> You will find the flag after decrypting this file.  
> Encrypted string provided:
```
xqkwKBN{z0bib1wv_l3kzgxb3l_429in00n}
```
> Hint: "Sometimes rotation is right"

---

## Category

General Skills

---

## Challenge Type

This is a classic **Caesar cipher** or **ROT-n** cipher where each alphabetical character is rotated by a fixed amount in the alphabet.

---

## Strategy

We are given an encrypted flag and a hint that implies a rotation cipher, likely **ROT13** or a Caesar cipher. To decode the flag:

1. Write a Caesar cipher decryption function
2. Brute-force all 26 possible shifts
3. Look for the one that gives a readable flag starting with `picoCTF{`

---

## Script

We used this Python script to test all 26 Caesar shifts:

```python
def caesar_decrypt(ciphertext, shift):
    result = ""
    for char in ciphertext:
        if char.isalpha():
            base = ord('A') if char.isupper() else ord('a')
            result += chr((ord(char) - base - shift) % 26 + base)
        else:
            result += char
    return result

def brute_force_caesar(ciphertext):
    print("Trying all Caesar cipher shifts:\n")
    for shift in range(26):
        decrypted = caesar_decrypt(ciphertext, shift)
        print(f"Shift {shift:2d}: {decrypted}")

ciphertext = "xqkwKBN{z0bib1wv_l3kzgxb3l_429in00n}"
brute_force_caesar(ciphertext)
```

---

## Output

After running the script, we find this output among the shifts:

```
Shift  8: picoCTF{r0tat1on_d3crypt3d_429af00f}
```

---

## Final Flag

```
picoCTF{r0tat1on_d3crypt3d_429af00f}
```

---

