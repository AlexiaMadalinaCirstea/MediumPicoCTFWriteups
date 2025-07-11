# mus1c – picoCTF Write-up

---

## Description

> I wrote you a song. Put it in the picoCTF{} flag format.
>
> Do you think you can master Rockstar?

---

## Solution

This was a **creative and code-based challenge** where the goal was to interpret symbolic Rockstar language lyrics and extract a flag. The Rockstar language is designed to be both poetic and functional, making this challenge a blend of programming and art.

---

### Step-by-step

#### 1. Understand the Lyrics

The lyrics mimic Rockstar syntax:

- `Put X into Y` → variable assignment
- `shout X` → output
- `Knock X down` → decrement
- `Build X up` → increment

These metaphorical constructs map directly to logic and memory manipulation.

---

#### 2. Interpret the Rockstar Output

When running the Rockstar code inspired by the lyrics, in the Rockstar programming language, the program outputs:

```
114 114 114 111 99 107 110 114 110 48 49 49 51 114
```

These are ASCII codes. Converting them:

```python
''.join(chr(c) for c in [114,114,114,111,99,107,110,114,110,48,49,49,51,114])
# Output: 'rrrocknrn0113r'
```

---

#### 3. Format as a Flag

Based on the output, we form the valid flag:

```
picoCTF{rrrocknrn0113r}
```

---

## Final Flag

```
picoCTF{rrrocknrn0113r}
```

---

