# Vigenere Cipher – picoCTF Write-up

---

## Description

> Can you decrypt this message?  
> Decrypt this message using this key: `"CYLAB"`

We are given an encrypted string that appears to follow the format of a `picoCTF{}` flag, but the contents are scrambled.

---

## Provided Ciphertext

rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_f85729e7}


We’re also given a key:

CYLAB


The hint suggests this is encoded using a **Vigenère cipher**.

---

## Vigenère Cipher?

The Vigenère cipher is a classic polyalphabetic substitution cipher. Each letter in the plaintext is shifted by a corresponding letter in the repeating key.

The cipher is symmetric, meaning the same process can be used to encrypt or decrypt.

---

## Solution

We use an online Vigenère decoder or write a quick script to decrypt the message.

### Tool Used

- [cryptii.com Vigenère Cipher Decoder](https://cryptii.com/pipes/vigenere-cipher)

### Steps:

1. Paste in the ciphertext:

rgnoDVD{O0NU_WQ3_G1G3O3T3_A1AH3S_f85729e7}


2. Set operation to **Decode**.
3. Use the key: `CYLAB`.

### Output

picoCTF{D0NT_US3_V1G3N3R3_C1PH3R_d85729g7} -> THE FLAG!