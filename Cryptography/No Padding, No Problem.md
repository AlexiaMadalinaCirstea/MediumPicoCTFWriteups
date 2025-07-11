# No Padding, No Problem – picoCTF Write-up

---

## Description

> Oracles can be your best friend, they will decrypt anything, except the flag's ciphertext. How will you break it?
> 
> Connect with `nc mercury.picoctf.net 60368`

## Challenge Summary

You're given:
- RSA modulus `n`
- Public exponent `e`
- A ciphertext `c`

The server will **decrypt any ciphertext** you submit **except the one matching the original encrypted flag**. However, it does reveal the plaintext if you trick it into thinking the ciphertext is different.

---

## Solution

### Key Insight:

In RSA:

```
(c + n)^d mod n == c^d mod n
```

Because:
```
(c + k*n)^d mod n ≡ c^d mod n
```

So, if the server is blocking exactly one ciphertext (`c`), then sending `c + n` will give you **the same plaintext**, bypassing the filter.

---

## Step-by-Step

### Step 1: Use the given values

```python
n = 131686352391973916658207299185394656543101094897022208742633102841081224841600706121562562241308481365796004945526588710743631163178644115777727835148863881283395196196732005291750988245372407622085435975007801389378779172237218772999563891226152449897259605289871450346323296355247453177918772507463563741811

ciphertext = 112804001031309304002025291636141380615160176064774815259814008475691402461011947625059065832958071876473967344200561585067064986192325164900998396425714393326505719176853515483384347660545842396602642909732341809974952827075466276674271508467259443005604311802505280608461621547597387301641072298382383236556
```

### Step 2: Bypass the restriction

```python
fake_cipher = ciphertext + n
print(fake_cipher)
```

Submit this number to the server.

### Step 3: Convert the output

The server returns a large number (plaintext). Use this to get the flag:

```python
from Crypto.Util.number import long_to_bytes

m_c = 290275030195850039473456618367455885069965748851278076756743720446703314517401359267322769037469251445384569347680788099965
print(long_to_bytes(m_c))
```

### Output:

```
b'picoCTF{m4yb3_Th0se_m3s54g3s_4r3_difurrent_3279013}'
```

---

## Final Flag

```
picoCTF{m4yb3_Th0se_m3s54g3s_4r3_difurrent_3279013}
```
