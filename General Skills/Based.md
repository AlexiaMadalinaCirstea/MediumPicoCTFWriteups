
# Based – picoCTF Write-up

---

## Description

> To get truly 1337, you must understand different data encodings, such as hexadecimal or binary. Can you get the flag from this program to prove you are on the way to becoming 1337?  
>
> Connect with `nc jupiter.challenges.picoctf.org 15130`.

---

## Solution

This is an interactive challenge where the server presents data encoded in different formats (binary, octal, hex, decimal ASCII, base64, etc.). You must decode the string and respond correctly within a time limit.

---

### Step-by-step

#### 1. Connect to the challenge:
```bash
nc jupiter.challenges.picoctf.org 15130
```

#### 2. Example prompts and decoding methods:

---

**Binary Example**  
Prompt:
```
Please give the 01100011 01101111 01101101 01110000 01110101 01110100 01100101 01110010 as a word.
```

Python:
```python
''.join([chr(int(b, 2)) for b in "01100011 01101111 01101101 01110000 01110101 01110100 01100101 01110010".split()])
# Output: 'computer'
```

---

**Octal Example**  
Prompt:
```
Please give me the  146 141 154 143 157 156 as a word.
```

Python:
```python
''.join([chr(int(n, 8)) for n in "146 141 154 143 157 156".split()])
# Output: 'falcon'
```

---

**Hex Example**  
Prompt:
```
Please give me the 636f6d7075746572 as a word.
```

Python:
```python
bytes.fromhex("636f6d7075746572").decode()
# Output: 'computer'
```

---

Repeat this decoding process until you finish all questions. The formats will vary, but the key is to recognize the base and decode accordingly.

---

## Final Flag

Once you complete all the decoding steps correctly, the server returns:

```
picoCTF{learning_about_converting_values_02167de8}
```


---

## Takeaway

This challenge reinforces core skills in data representation and encoding. Knowing how to identify and decode binary, hex, octal, and base64 is essential in CTFs and real-world cybersecurity tasks.
